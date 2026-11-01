# SWM-3D-010: Distal Motor Overflow (3-DOF Ankle Supination Freeze), Dual-Impulse Reverse Inference & Boundary-Handshake Sanitization (`Scene 3 / Klappe 4.8.1`)

**Date:** `2026-11-01`  
**Repository:** `humanai2026/3D_Affrodance`  
**Architectural Scope:** Level 1 (Universal Neuro-Biomechanics & 3-DOF Ankle Kinematics), Level 2 (Scene-3 Spatial Topology & Furniture Clearance), Level 3 (Subconscious Defense Hierarchy & Peripheral Magnocellular Amplification), Level 4 (`swm_v6_engine.py` & `scene-3.py` Verification Gate)

---

## 1. Executive Summary & Epistemological Goal (`Reverse Mind-Reading from Mute 4D Geometry`)

To enable future multimodal world models (`Carbon` offline reasoners and `Flash` real-time stream predictors) to **reconstruct latent human thoughts and emotional subtext purely from mute 3D/4D video trajectories without prior story context (`Backward Perceptual Inference`)**, a scene must encode subconscious defense impulses into mechanically observable distal channels whenever proximal joints are immobilized.

During the staging and visual audit of **Scene 3 (`Frame 1..240`, `Handshake_2_to_3 -> Handshake_3_to_4`)**, three foundational laws were derived and verified:
1. **LawWB-4 — Defense Shield Hierarchy & Distal Subtalar Motor Overflow (`Inhibited Closure Substitution`):** When the primary pelvic protection shield (bilateral hip adduction) is mechanically locked ($\mu_{	ext{shell}} = 0$, $\Omega_{	ext{proximal}} = 0$) and the secondary abdominal hand shield (`guard_w = 1.0`) is threatened by an optical boundary breach or a verbal unshielding command, the descending corticospinal adduction drive overflows along the medial musculature (*M. tibialis posterior*, *M. tibialis anterior*, *M. flexor hallucis longus*) into the unconstrained distal ankle joints ($\Omega_{	ext{distal}} > 0$). Because 1-DOF ankle pitch (`foot_pitch_offset`) cannot represent medial closure, the engine was upgraded to **full 3-DOF subtalar kinematics (`pitch`, `roll`, `yaw`)**, rendering **bilateral sole inversion (`foot_roll_R/L = ±0.24 rad`)** and **forefoot medial adduction (`foot_yaw_R/L = ∓0.18 rad`)** — a visible inward turning of the soles toward each other.
2. **LawWB-5 — Dual-Impulse Diagnostic Contrast for Unsupervised Causal Attribution (`Precursor Release vs. Tonic Cliffhanger Freeze`):** Embedding two temporally separated ankle supination impulses triggered by distinct external causes within the same 240-frame window allows an observer model to disentangle *optical exposure reflexes* from *social-verbal compliance traps* via their release signatures.
3. **LawWB-6 — Layered Boundary-Handshake Sanitization (`sanitize_handshake_2_to_3` & Pre-Filter Pinning Order):** Cross-scene continuity requires layering corrective topological overrides (`stool_pos = [0.65, -1.38, 0.0]`, `stool_rz = -0.35 rad`, `Doctor_C yaw = -1.5708 rad`) **on top of** the inherited `Handshake_2_to_3` state *before* Frame 1 generation, and pinning `frames[0]` **prior to** running the vestibular angular-velocity limiter (`enforce_vestibular_limit`).

---

## 2. Law WB-4: Neuro-Biomechanical Derivation of the 3-DOF Subtalar Supination Reflex

### 2.1 The Two-Tier Protection Hierarchy under Proximal Fixation ($\mu = 0$)
In the reclined workstation topology (`pelvis_pos = [0.0, -0.062, 0.672]`, `pelvis_rpy = [-0.54, 0.0, 0.0]`, `chair_back_rx = -0.68 rad`), `Patient_A`'s lower limbs are abducted and coaxially bedded inside the locked Göpel shells (`cradle_R/L_rpy = [0.2887, 0.0, ∓0.3830]`, $\mu = 0$).
- **Tier-1 Primary Shield (Blocked):** Bilateral hip adduction and internal femoral rotation ($	au_{	ext{adductor}} > 0$) are physically blocked by the rigid shell walls ($\Delta	heta_{	ext{thigh},z} \equiv 0$).
- **Tier-2 Secondary Shield (Active in Scene 3):** As proven empirically in **Discovery D7 (`02:13` Folding-Chair PoC)**, the brainstem automatically substitutes the lost primary shield by interlocking both hands tightly over the lower abdomen (`wr_R = [-0.050, -0.167, 0.772]`, `wr_L = [+0.054, -0.171, 0.775]`, `guard_w = 1.0`).

### 2.2 Descending Motor Overflow into the Distal Tibialis Chain
When `Doctor_C` issues the routine clinical instruction at `Frame 212` (*"Bitte mal die Hände auf die Armlehnen legen"* accompanied by an inviting bimanual gesture toward `Chair_Armrest_Pad_R/L`), `Patient_A`'s auditory-limbic circuit registers an **impending loss of the Tier-2 Secondary Shield** before her hands even move.
1. Seeking an alternative protective mode, the brainstem fires an emergency motor command back into the **Tier-1 Primary Shield** (*"Close the legs!"*).
2. Because the proximal hip and knee joints are immobilized ($\Omega_{	ext{hip,knee}} = 0$), the descending motor command overflows into the distal segments of the same medial kinetic chain that extend freely beyond the anterior rim of the Göpel shells (`Ankle_R/L` and `Toes_R/L`, $\Omega_{	ext{distal}} > 0$):
   - **Subtalar Inversion / Supination (`foot_roll_R/L` around local Y-axis):** The medial borders of both feet elevate, rotating the **plantar soles inward toward each other** (`foot_roll_R: 0.0 -> +0.24 rad` [$+13.8^\circ$], `foot_roll_L: 0.0 -> -0.24 rad` [$-13.8^\circ$]).
   - **Forefoot Medial Adduction (`foot_yaw_R/L` around local Z-axis):** Both forefeet rotate medially ("pigeon-toed") toward the body midline (`foot_yaw_R: 0.0 -> -0.18 rad` [$-10.3^\circ$], `foot_yaw_L: 0.0 -> +0.18 rad` [$+10.3^\circ$]).
   - **Tonic Digital Flexion & Tremor Damping:** The toes curl inward (`toes_r/l_rpy[0]: 0.0 -> +0.32 rad`, `spread: -0.08 rad`), while the baseline `2.1 Hz` distal micro-tremor amplitude is compressed by $50\%$ under isometric co-contraction (`tremor_amp: 0.015 -> 0.0075 rad`).

### 2.3 Peripheral Magnocellular Amplification in Triadic Space
At `Frame 210..240`, `MTA_B` stands at `[-0.50, -0.74, 0.80]` (`yaw = +0.52 rad`) directly beside the seated `Doctor_C` (`[0.0, -0.78, 0.665]`) and locks her foveal gaze onto `Patient_A`'s eyes (**Stage 1 of the Gaze Cascade: `Face-Lock`**).
- In 3D world space, `Patient_A`'s bare feet (`ankle_w ≈ [∓0.38, -0.55, 0.82]`) float only **$25	ext{--}35	ext{ cm}$ anterior to `MTA_B`'s lower ribcage**, directly inside `MTA_B`'s lower peripheral visual field.
- While `Patient_A` attempts to maintain a composed facial facade and her hands remain welded to her abdomen, `MTA_B`'s peripheral magnocellular pathway registers the cramping inward rotation of both soles in real time — exposing the futile subconscious attempt to close the immobilized legs.

---

## 3. Law WB-5: Dual-Impulse Temporal Signature for Reverse Video Inference (`Scene 3`)

| Phase / Frame Window | External Spatial-Social Trigger | `Patient_A` Ocular & Cervical State | `Patient_A` 3-DOF Ankle & Toe State | Diagnostic Reverse-Inference Meaning |
| :--- | :--- | :--- | :--- | :--- |
| **Impulse 1 (Precursor)**<br>`Frame 28..68`<br>(`t = 0.115..0.285`) | `Doctor_C` opens room door (`door_rz = +1.18 rad`), pauses in frame `[-2.12, -1.40, 0.80]`, turns back toward hallway (`yaw = +0.85 rad`). | `nh_rx = -0.06 rad` (occipital press into headrest), `eye_rx = -0.28 rad` (rigid ceiling gaze avoidance). | **45% Precursor Pulse:**<br>`foot_roll_R/L = ±0.11 rad`<br>`foot_yaw_R/L = ∓0.08 rad`<br>`toe_curl = +0.18 rad` | Subconscious optical-exposure reflex triggered by hallway sightline intersecting the foot of the chair. |
| **Door-Shut Release**<br>`Frame 85..116`<br>(`t = 0.365..0.485`) | `Doctor_C` steps inside and pulls interior handle shut (`door_rz -> 0.0 rad` at `Frame 112`). | `nh_rx` relaxes to `+0.04 rad`; thoracic apnea hold persists during `Doctor_C <-> MTA_B` glance. | **Complete Release to Baseline:**<br>`foot_roll_R/L = 0.00 rad`<br>`foot_yaw_R/L = 0.00 rad`<br>`toe_curl = 0.00 rad` | Proves causally that **Impulse 1** was coupled strictly to the open corridor boundary (`door_rz > 0`). |
| **Impulse 2 (Cliffhanger Freeze)**<br>`Frame 214..240`<br>(`t = 0.890..1.000`) | Seated `Doctor_C` gestures to armrests (*"Hände auf die Armlehnen"*); `MTA_B` locks foveal gaze onto `Patient_A`'s eyes (`Face-Lock`). | Startled downward gaze shift (`nh_rx = +0.08 rad`, `eye_rx = +0.18 rad`) into `Doctor_C`/`MTA_B` phalanx. | **100% Tonic Supination Freeze:**<br>`foot_roll_R/L = ±0.24 rad`<br>`foot_yaw_R/L = ∓0.18 rad`<br>`toe_curl = +0.32 rad` (locked across `Handshake_3_to_4`). | Anticipatory shield-loss reflex: brain searches for alternative closure before hands even leave the abdomen. |

---

## 4. Law WB-6: Layered Handshake Sanitization & Vestibular Filter Ordering (`Level 2 & Level 4`)

### 4.1 Why Raw Boundary Inheritance Fails When Fixing Upstream Layout Bugs
When transitioning from Scene 2 (`Handshake_2_to_3`) to Scene 3, blindly copying `drehbuch.json["boundary_keyframes"]["Handshake_2_to_3"]` into `frames[0]` at the end of the generator script re-injects any legacy spatial defects stored in `drehbuch.json`:
1. **Cabin Wall Intersection (`Y = -1.72 m`):** The legacy stool position `[0.0, -1.72, 0.0]` sat directly inside the northern partition wall of the changing cabin (`Y = -1.72 m`).
2. **Inverted Hallway Orientation (`yaw = +1.5708 rad`):** Under our right-handed Euler convention (`+Y` forward at `yaw = 0.0`), `yaw = +1.5708 rad` ($+90^\circ$) rotates the forward vector counter-clockwise toward **`-X` (away from the room door)**. To face the room door (`+X`) from the hallway (`X = -2.68 m`), `Doctor_C` requires **`yaw = -1.5708 rad`** ($-90^\circ$).

### 4.2 The Two-Stage Sanitization & Pinning Protocol
1. **`sanitize_handshake_2_to_3(raw_b_in)` Pre-Processor:**
   - Preserves `Patient_A` and `MTA_B` 1:1 from the verified Scene 2 end-state (initializing missing `foot_roll_R/L` and `foot_yaw_R/L` keys to `0.0`).
   - Overlays the sanitized Scene 3 initial furniture and hallway actor states *before* the 240-frame loop runs:
     - `stool_pos = [0.65, -1.38, 0.0]`, `stool_rz = -0.35 rad` (clear in front of the cabin wall, backrest angled toward approaching `Doctor_C`).
     - `Doctor_C`: `pelvis_pos = [-2.68, -1.42, 0.80]`, `pelvis_rpy = [0.0, 0.0, -1.5708]`, gaze split aimed at exterior door handle `get_door_handle_world(0.0, "outside")`.
2. **Pre-Filter Pinning Order (`Pin Frame 1 BEFORE enforce_vestibular_limit`):**
   - Never overwrite `frames[0]` with `b_in` *after* calling `cm.enforce_vestibular_limit(frames, max_deg_per_frame=2.3)`, as post-filter overwriting creates an unsmoothed discontinuity between `Frame 1` and `Frame 2` (`AssertionError: Frame 2 Doctor_C Vestibular limit exceeded`).
   - Always pin `frames[0] = deepcopy(b_in)` **first**, and execute `cm.enforce_vestibular_limit(frames, max_deg_per_frame=2.3)` **second**, guaranteeing $C^1$-smooth cervical angular velocity ($\le 2.3^\circ/	ext{frame}$) out of the exact boundary state.
