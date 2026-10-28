# SWM V6 — Architectural & Biomechanical Learnings (Session 2026-10-28)

## Executive Summary
During the visual QA audit of **Scene 2 (Klappe 4.5 $\rightarrow$ Klappe 4.6 blueprint)** and the preparation of the **Scene 3 MoCap Rehearsal Studio**, we identified and resolved five fundamental failure modes typical of LLM-driven 3D/4D spatial reasoning. Rather than applying local coordinate patches, each defect was traced to its mathematical root cause and anchored as an invariant law in the **SWM V6 5-Tier Architecture**.

---

## 1. The "Crab-Walking" Illusion: Why Procedural Gait Must Decompose Path Tangent vs. Pelvis Yaw
* **Visual Symptom (`Frame 33..58`):** While walking from the headrest (`Y = +0.22 m`) to the anterior Goepel shell (`Y = -0.38 m`), `MTA_B` kept her torso facing the chair (`+X`) while her legs scissored forward and backward into the chair frame—producing an unnatural sideways "crab-walk" with stiffly outstretched forearms.
* **Root Cause:** Standard procedural gait functions drive hip flexion (`thigh_rx`) purely as a function of step phase $\phi$, implicitly assuming the character's facing direction $\psi_{\text{pelvis}}$ equals the movement tangent $\psi_{\text{path}} = \text{atan2}(T_x, -T_y)$.
* **Constructive Law (`LAW_L1_OMNI_DIRECTIONAL_GAIT_DECOMPOSITION`):**
  1. Compute the heading offset $\Delta\psi = \text{wrap}(\psi_{\text{path}} - \psi_{\text{pelvis}})$ at every frame.
  2. Decompose leg swing into a **sagittal flexion component** ($\cos\Delta\psi \to \text{thigh\_rx}$) and a **coronal abduction/sidestep component** ($\sin\Delta\psi \to \text{thigh\_ry}$).
  3. For step distances $D_{xy} > 0.35\text{ m}$, blend `pelvis_yaw` naturally into the walking direction during mid-stride (`Turn-Walk-Turn`) while keeping the head/gaze oriented toward the patient, and drop free hands to a natural hip-side pendulum swing.

---

## 2. When Safety Assertions Cause Self-Intersection: Dynamic Task-Axis Alignment & Arm-IK Pole Vectors
* **Visual Symptom (`Frame 41` & `Frame 76`):** `MTA_B`'s right forearm tunneled straight through her own abdomen/thorax when pushing the reclining backrest (`-0.68 rad`) and when grasping the right Goepel shell.
* **Root Cause (Dual Mechanism):**
  1. **Over-Constrained Yaw Assertion:** An assertion forcing `MTA_B` to continuously face the seat center `[0.0, -0.20]` prevented her from turning her pelvis toward the upper backrest (`Y = +0.45 m`). As the backrest reclined behind her shoulder plane, her right arm had to reach backward through her own torso.
  2. **Inverted IK Pole Vector Sign:** Because SWM V6 defines `-Y` as local forward and `+Y` as posterior, an elbow pole vector of `[±0.42, +0.82, -0.38]` pushed the elbow backward (`+Y`) into the ribcage whenever the wrist reached forward-downward.
* **Constructive Law (`LAW_L1_BIMANUAL_TASK_AXIS_AND_IK_POLE_CLEARANCE`):**
  - Orientation assertions now track the **live active affordance target** $\mathbf{P}_{\text{task}}(t)$.
  - `MTA_B` steps to `[-0.48, +0.30, 0.80]` and rotates her pelvis to `yaw = +1.85..+2.02 rad` when actuating the headrest/backrest.
  - `solve_arm_ik` uses an outward lateral pole vector (`[±0.85, +0.18, -0.35]`) with a hard torso-radius repulsion clamp.

---

## 3. Distal Limb Envelopes & Cubic 2-Control-Point Circumvention (`Frame 117` & `Frame 187`)
* **Visual Symptom:** `MTA_B` walked through `Patient_A`'s cradled right lower leg/foot both on the outbound path (`Frame 117`) and on the return path (`Frame 187`).
* **Root Cause:**
  1. The collision firewall only checked `hip_w`, `mid_thigh_w`, `knee_w`, and `shell_center`, ignoring the abducted lower leg (`Shank_Mesh`), `Ankle`, and `BareFoot`, which project out to `X = ±0.49 m, Y = -0.58 m`.
  2. A quadratic Bézier curve with a single control point cannot maintain a wide anterior clearance across *both* abducted feet simultaneously, cutting inward too early at $u \approx 0.45$.
* **Constructive Law (`LAW_L1_DISTAL_LIMB_HULL_AND_CUBIC_CIRCUMVENTION`):**
  - `get_patient_leg_chain_world` computes the full 5-point FK chain (`hip`, `knee`, `mid_shank`, `ankle`, `foot_tip`) for both legs across all 240 frames.
  - Both outbound (`Step 3`) and return (`Step 4`) walks use a **cubic 2-control-point U-arc** (`p_ctrl1 = [+0.15, -1.06, 0.80]`, `p_ctrl2 = [-0.72, -1.06, 0.80]`) that stays strictly anterior to `Y <= -0.88 m`.

---

## 4. Eliminating "IK-Truncation Telekinesis" & Ghost Hardware (`Frame 132..154`)
* **Visual Symptom:** During left shell adjustment (`Frame 132..148`), `MTA_B`'s hand hovered 10 cm short of `Goepel_Shell_L` (clipping through the patient's left forearm) while the shell rotated by itself. In `Frame 154`, a small lever (`Goepel_ScrewKnob_L`) popped out of the bottom left seat frame.
* **Root Cause:**
  1. Standing at `X = -0.06 m`, `MTA_B`'s right shoulder was `0.55 m` away from the left shell rim. `clamp_ik_reach(0.468 m)` silently truncated the wrist in mid-air!
  2. `Goepel_ClampScrew_R/L` had an asymmetric local `-Z` offset under `±72°` Y-tilt that hid the right knob inside the seat frame while exposing the left knob upon cradle rotation.
* **Constructive Law (`LAW_L1_POST_IK_CONTACT_LOCK_ASSERTION`):**
  - Removed the redundant `Goepel_ClampScrew` meshes from `swm_v6_engine.py`, eliminating both the visual artifact in `Frame 154` and the need for the second hand to reach under `Chair_Armrest_Pad_R` in `Frame 76`.
  - Moved `MTA_B`'s left work stance to `[+0.28, -0.64, 0.80]` (`yaw = -2.12 rad`, shoulder-to-shell distance $= 0.29\text{ m}$) and added a post-IK assertion verifying `v_dist(actual_wrist, rim_wrist) <= 0.012 m` whenever a shell moves.

---

## 5. End-Pose Flush Spine Identity & Single-Source Goepel Rod Extension (`Frame 240`)
* **Visual Symptom:** Side-view inspection (`Frame 240`) revealed a wedge-shaped air gap behind the upper back/occiput and a vertical gap between the calves and the Goepel shells.
* **Constructive Law (`LAW_L1_CUMULATIVE_SPINE_FLUSH_AND_ROD_EXTENSION`):**
  - **Flush Spine Identity:** `pelvis_rx (-0.22) + abd_rx (-0.34) + thx_rx (-0.12) = -0.68 rad == chair_back_rx`, paired with `nh_rx = +0.04 rad` at `headrest_slide = +0.055 m`, places the entire back, neck, and occiput flush against the upholstery ($0.0\text{ mm}$ air gap).
  - **Extended Support Rods:** `GOEPEL_HOLDER_LOC` is extended to `[lat_s * 0.092, -0.215, 0.268]` as a shared constant between `swm_v6_common.py` and `swm_v6_engine.py`, raising the shells coaxially into the calves while automatically updating all downstream hand and gaze affordances.