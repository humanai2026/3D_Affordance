# SWM 4D Kopfbild Foundation & Universal Spatial-Cognitive Benchmark
**Repository Target:** `humanai2026 / 3D_Affrodance`  
**Architecture Level:** SWM V5.7.1 -> V6 Universal Baseline (Flash-Model & Gemini Live Ready)

---

## 1. Purpose: Zero-Drift Spatial Reasoning for Fast Synthesis & Real-Time Perception

When an AI builds an internal 3D/4D mental model ("Kopfbild") in a lightweight model (e.g., Gemini Flash) or observes a live 3D scene/video stream in real time (e.g., Gemini Live), it cannot afford to guess 50 raw coordinates and 18 independent Euler joint angles per character on every frame. Guessing raw joint angles in isolation causes the classic Semantic-to-Numeric Hallucination Gap:
- Hands slice through hips or hover centimetres away from levers (Telekinesis / IK-Gap).
- Feet slide across the floor like ice skates or cross over each other (Crab-Walk / Foot-Slip).
- Calves flip by 180 deg when crossing the vertical pole (Hemisphere Singularity).
- Walking looks robotic or toddler-like because the Center of Mass (CoM) decelerates to v = 0 at the end of every single step.

This document establishes the 5-Layer Kopfbild Protocol and the Conscious vs. Subconscious Locomotion Law so any model—whether generating 4D trajectories offline or interpreting human body language in real time—starts from an unbreakable physical and psychological baseline.

---

## 2. The 5-Layer Kopfbild Protocol (Universal Synthesis <-> Perception Stack)

| Layer | Principle | Generative Rule (Building a Scene in Flash/Pro) | Perceptual Rule (Watching a Scene in Gemini Live) |
| :--- | :--- | :--- | :--- |
| **Layer 1: Spatial Topology** | **4-Zone Concentric Hull Model** (`Core` / `Contact` / `Bypass` / `Transit`) | Never emit raw coordinates without assigning one of the 4 hull zones relative to furniture and body volumes. | Immediately flags boundary violations: Is a hand in the *Transit Zone*, *Peripersonal Bypass*, or *Tangential Contact*? |
| **Layer 2: 4D Causality** | **Strict Master-Slave Hierarchy** (`Gaze` -> `CoM` -> `End-Effectors` -> `IK Joints`) | Gaze leads by 0.30-0.40 s; CoM defines the trajectory tangent; hands/feet pin to world/object anchors; joints are solved last. | Reads intent from temporal ordering: Does gaze precede the hand (*planned action*) or snap after an event (*startle reflex*)? |
| **Layer 3: Subcortical IK** | **6 World Anchors over 18 Euler Angles** (`solve_human_limbs_from_targets`) | Never guess knee, elbow, or ankle Euler angles. Specify 6 targets (`pelvis`, `gaze`, `foot_R/L`, `wrist+palm_R/L`) and solve analytically. | Compresses a 36-node anatomical mesh into 6 high-signal 3D vectors that can be tracked in milliseconds. |
| **Layer 4: Dual Clock** | **Cortical Focus (1x) vs. Subcortical Flow (inf)** | Separate conscious single-focus manipulation from continuous subconscious background flow (breathing, passive draping, continuous CoM gait). | Distinguishes **conscious hesitation** (CoM stops between steps, sticking screw) from **subconscious routine** (continuous CoM glide). |
| **Layer 5: Empathy Tensor** | **Substrate-Isomorphic Micro-Signatures** (Delta_W, Omega, Delta_I, Delta_E_asym, Clusivity) | Translate psychological tension into concrete biomechanical overflow (Omega) and gaze-timing shifts rather than generic poses. | Acts as a **Real-Time Profiler**: Detects vulnerability, helplessness overflow, covert curiosity, or status-tension discharge. |

---

## 3. Deep Dive: The 5 Foundational Laws

### Law 1: The 4-Zone Concentric Hull Topology
Before computing any coordinate, partition the 3D space around every anatomical segment (`Pelvis_Core`, `Thorax_Core`, `Thigh`, `Calf`) and every apparatus (`Workstation_Rig`, `Support_Cradles`, `Mobile_Stool_Rig` 5-star base R = 0.245 m, `Mayo_Stand`) into four zones:
1. **Zone 0 — Forbidden Hull Interior (d < 0 mm):** Zero penetration allowed. Evaluated via bounding-radius-subtracted surface distance:
   dist(P_limb, P_object) - R_limb - R_object >= 0.04 m
2. **Zone 1 — Tangential Contact Skin (d = 0..2 mm):** Reserved strictly for active hand paddles (`Hand_Palm_Cone` + `Hand_Fingertip_Cap`) during an explicit contact window t in [t_dock, t_release] and for seated/reclined body rest surfaces. The wrist target P_wrist is placed along the outward surface normal n_out by (d_half_thickness + r_hand) and paired with a fingertip orientation target P_point (`limit_wrist_deflection <= 0.32 rad`) so the palm lies flat against the surface (e.g., outer Star Knob `Clamp_Star_Knob_R/L`, top edge of the backrest Z_local = 0.58 m, or stool crescent push-pad Z_world = 0.94 m).
3. **Zone 2 — Peripersonal Bypass Corridor (d = 5..25 cm):** Mandatory clearance arc (`eval_l_corridor`) when routing hands past the actor's own pelvis (|X - X_pelvis| >= 0.24 m, Z >= Z_pelvis + 0.12 m) or lifting a leg over the flared popliteal lip of a support cradle.
4. **Zone 3 — Free Transit Corridor (d >= 30 cm):** The collision-free floor corridor for walking trajectories (e.g., perimeter arc R_arc = 0.84 m around the support cradles or parallel track alongside the rolling stool).

---

### Law 2: Conscious Discrete Stepping vs. Subconscious Continuous-CoM Locomotion
A critical Uncanny Valley trigger occurs when adult walking is modeled as sequential, non-overlapping foot intervals (`smoothstep(u)` per step) where the pelvis is computed as the weighted average of the two feet. Because the derivative of `smoothstep(u)` is zero at u=0 and u=1, **the body's Center of Mass (CoM) decelerates to v = 0 after every single step**, mimicking a toddler learning to walk or a person groping in the dark.

Human locomotion must be split into two distinct biomechanical regimes:

#### A. Regime 1 — Subconscious Continuous-CoM Locomotion (Adult Transit Gait)
When an adult walks across a room or along a perimeter arc (N >= 2 steps), the brain does not issue discrete per-step start/stop commands. Locomotion is **controlled forward falling** where the **Center of Mass (Pelvis/Thorax) is the continuous Master** and the **feet are rhythmic pendular Slaves**:
1. **Continuous CoM Spline (v_CoM > 0 across all intermediate steps):**
   - The pelvis follows a smooth spatial curve P_CoM(s(t)) where s(t) accelerates once at walk initiation (t_start), maintains **strictly positive, near-constant cruise velocity** (v_CoM ~ 0.75-1.10 m/s) across all intermediate footfalls, and decelerates once at the destination (t_end).
2. **Tangent-Aligned Pelvis Heading (0% Crab-Walk):**
   - Throughout transit, the pelvis yaw tracks the forward tangent of the CoM velocity vector:
     psi_pelvis(t) = atan2(v_x(t), -v_y(t)), |psi_pelvis(t) - psi_vel(t)| <= 28 deg
3. **Overlapping Double-Support Phase (~18% Step Overlap) & CoM Lateral Pendulum:**
   - Footsteps alternate along parallel inner/outer tracks separated by hip width (2 * 0.115 m = 0.230 m, zero crossover) with a +35 mm posterior heel-to-hip-plumb offset (`stance_foot_world`).
   - While one foot is pinned to the floor (`z_ankle == 0.06 m`, Coulomb static friction v_XY = 0.0 mm/s), the swinging foot overtakes it along a sinusoidal vertical arc z_lift(u) = 0.06 + h_lift * sin(pi * u) with **continuous horizontal velocity at mid-swing** and an ~18% double-support transition window where weight transfers smoothly from trailing toe-off to leading heel-strike without halting forward CoM momentum.

#### B. Regime 2 — Conscious Discrete-Step Positioning (Precision Pivot / Hesitant Threshold)
Discrete single-step intervals where v_CoM -> 0 at the end of the step are reserved strictly for two situations:
1. **Local Workstation Repositioning (1-2 Pivot Steps):** Turning in place or stepping 15-25 cm closer to a mechanical assembly (e.g., aligning chest normal n_chest with a clamp knob or stepping from the cradle to the backrest).
2. **Psychological Threshold Hesitation (Delta_W Spike):** When `Seated_Agent_A` approaches the examination chair in Scene 1, transitioning from fluent subconscious walking (Regime 1) into 1-2 decelerated, conscious steps (Regime 2) right before sitting down makes internal boundary tension (Delta_W) immediately visible.

---

### Law 3: Subcortical 2-Bone IK, Pole-Singularity Damping & Holistic Hand/Foot Paddles
1. **Analytical 2-Bone IK (`solve_2bone_ik`):** Given root joint P_root (shoulder or hip), end target P_target (wrist or ankle), bone lengths (L1, L2) (`0.27m / 0.23m` for upper/forearm; `0.42m / 0.38m` for thigh/calf), and pole direction d_pole, compute the exact elbow/knee midpoint P_mid via the Law of Cosines and Gram-Schmidt orthogonal projection.
2. **Dual-Branch Hemisphere Selection with Pole-Singularity Damping (`vec_to_hemisphere_rpy`):** Select the continuous Euler branch [2*pi - rx, 0, rz + pi] whenever |rz - rz_ref| > pi/2, and damp azimuthal rotation near the vertical pole via `s_pole = clamp((horiz - 0.015) / 0.055, 0.0, 1.0)`.
3. **Two-Part Split Torso & 3D-Pythagoras X <-> YZ Reach-Coupling:** Modeling the torso as `Abdomen_Core` (0.225 m wide) + `Waist_Joint_Sphere` (0.172 m wide) + `Thorax_Core` (0.288 m wide) creates an anatomical 60 mm waist indentation so clasped hands remain tangentially draped on the lower abdomen during recline with 0% pelvic tunneling.

---

### Law 4: Holonomic Local-Frame Attachment & Two-Handed Mechanical Affordance
Every movable apparatus DOF obeys Contact-Gated Holonomic Actuation (dq_mech/dt = 0 outside [t_dock, t_release]), with active hands anchored in the local coordinate frame of the moving part (`shell_local_to_world`, `backrest_local_to_world`, `stool_local_to_world`).

---

### Law 5: Bidirectional Empathy Bridges for Synthesis & Real-Time Profiling
Maps internal structural tensions (`Delta_W` boundary exposure, `Omega` helplessness overflow under locked leg actuators, `Delta_I` covert curiosity with sticking-screw alibi, and `Delta_E_asym` conscious role-reversal tension discharge) bidirectionally between 4D kinematic staging and real-time observation.