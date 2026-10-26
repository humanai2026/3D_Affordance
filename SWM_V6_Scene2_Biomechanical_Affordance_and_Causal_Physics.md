# SWM V6 — Biomechanical Affordance Coupling, Inert Matter Physics & Inverse Visual QA (Act II Learnings)

**Repository:** `humanai2026/3D_Affrodance`  
**Architectural Scope:** Level 0 (Cognitive Allocation) · Level 1 (Universal Physics & Anatomy) · Level 2 (Scene Affordance Geometry)  
**Focus:**Bidirectional spatial-temporal reasoning — **Forward Generation** (synthesizing physically and anatomically truthful 4D trajectories) and **Backward Interpretation** (auditing 3D/4D scenes for causal illusions, telekinesis bugs, and heuristic shortcuts).

---

## 1. Forward Consideration (`Vorwärtsbetrachtung`): Causal Laws for 4D Scene Generation

When an LLM synthesizes 3D/4D human-object interactions without a live physics engine, it must replace purely descriptive interpolation with **constructive, parameter-coupled causal laws**.

### 1.1 The Universal Law of Inert Matter & Kinetic Actuation (`Gesetz der toten Materie`)
Inert mechanical objects (examination chairs, backrests, headrests, articulated leg cradles, clamp screws, doors, rolling stools) possess **zero intrinsic agency**:
$$\forall\, q_{\text{furniture}} \in \mathcal{Q}_{\text{env}}: \quad \left|\frac{dq_{\text{furniture}}}{dt}\right| > 0 \implies \exists\, \vec{F}_{\text{human}}(t) > 0 \;\;\text{with}\;\; \left\|\vec{P}_{\text{effector}}(t) - \vec{P}_{\text{handle}}(t)\right\|_2 \le \epsilon_{\text{contact}}$$

1. **Purely Manual Systems:** Without direct physical contact ($\epsilon_{\text{contact}} \le 0.045\text{ m}$ in World Space) and force transmission from a human effector, **exactly zero movement occurs ($\Delta q_{\text{furniture}} \equiv 0.0000$)**.
2. **Motorized / Hydraulic Systems:** Even when an actuator drives the degree of freedom, the trajectory must be preceded and accompanied by a **visible human trigger** (e.g., finger contact on a control console or foot depression on a base pedal).
3. **Ban on Implicit Script Coupling:** Never couple a secondary manual DOF (such as a telescopic headrest slide `headrest_slide`) mathematically to a primary DOF (such as backrest inclination `chair_back_rx`) unless a hand physically grasps and slides that component.
4. **Ban on Bilateral Telekinesis:** Independent kinematic chains (such as left and right ball-jointed Göpel leg holders `Goepel_BallJoint_R/L` at $X = \mp 0.165\text{ m}$) are not geared together. Moving the right cradle while standing on the right flank leaves the left cradle strictly invariant ($\Delta \vec{\theta}_{\text{cradle},L} \equiv \vec{0}$) until the operator physically reaches across or relocates to actuate the left side.

---

### 1.2 End-Effector Offset Law: Wrist-Root vs. Distal Finger-Pad Geometry (`Handwurzel-Fingerkuppen-Offset`)
In articulated skeletal rigs, the inverse kinematics (IK) target `wrist_pos` controls the **Wrist Joint Root (`Hand_Root`)**, not the fingertips. In SWM V6:
* **Palm Length ($L_{\text{palm}}$):** $0.074\text{ m}$ along the distal forearm axis ($-Z_{\text{local}}$), thickness $0.024\text{ m}$.
* **Articulated Finger Length ($L_{\text{fingers}}$):** $0.068\text{ m}$ (`Proximal` + `Distal` phalanges).
* **Total Extended Reach beyond Wrist Root:** $0.142\text{ m}$ ($14.2\text{ cm}$); curled grasp reach $\approx 0.095\text{ m}$.

#### Constructive Consequences:
1. **Preventing Thin-Shell Penetration (`Shell Poke-Through`):** Setting `wrist_pos` directly onto the center or wall of a thin curved trough (`Goepel_Shell` wall thickness $d = 0.015\text{ m}$, outer radius $R_{\text{out}} = 0.071\text{ m}$) places the wrist joint on the surface while the $14.2\text{ cm}$ palm and fingers plunge straight through the floor of the shell. To grasp an exterior rim from above/outside with $0.0\text{ mm}$ penetration, `wrist_pos` must be offset along the outward radial and vertical surface normals:
   $$\vec{P}_{\text{wrist,rim}} = \vec{P}_{\text{shell\_center}} + \left[\mp (R_{\text{out}} + 0.017\text{ m}),\; -0.020\text{ m},\; +(L_{\text{curled}} - 0.003\text{ m})\right] = \vec{P}_{\text{shell\_center}} + [\mp 0.088,\; -0.020,\; +0.092]\text{ m}$$
2. **Modeling Mechanical Breakaway Torque (`Gasfeder-Losbrechmoment & Finger-Abknicken`):** Pressing a gas-spring-damped backrest (`chair_back_rx`) is not a rigid-body translation. Real force transmission exhibits a **2-stage compliance curve**:
   * **Stage A (Contact & Pre-Load Buckling, $t \in [t_0, t_1]$):** The palm and nearly extended fingers ($\theta_{\text{curl}} = 0.26\text{ rad}$) make flush contact with the upholstery rim. As the operator applies downward-posterior force against the gas spring's breakaway torque, the fingers **visibly flex/buckle at the MCP/PIP joints ($\theta_{\text{curl}}: 0.26 \to 0.86\text{ rad}$)** while the backrest remains stationary ($\Delta\theta_{\text{backrest}} = 0$).
   * **Stage B (Damped Yielding, $t \in [t_1, t_2]$):** Once breakaway resistance is overcome, the backrest yields smoothly ($\theta_{\text{backrest}}: -0.38 \to -0.52\text{ rad}$) while the flexed hand tracks the moving arc in World Space.

---

### 1.3 Invariant Bone-Chain Affordance Coupling (`Kniekehlen-Schalen-Anker & Becken-Kanten-Shift`)
Human long bones have invariant lengths ($L_{\text{femur}} = 0.380\text{ m}$ from hip socket to knee center; $L_{\text{tibia}} = 0.370\text{ m}$ from knee center to ankle center). When a human interacts with a multi-part clinical support system (seat cushion + backrest + V-mounted Göpel leg troughs), **the proximal joint (pelvis) must be positioned so that the invariant femur length places the distal joint (popliteal fossa / `Kniekehle`) exactly at the affordance anchor of the target support**.

* **The Central-Sitting Failure Mode:** On a seat cushion spanning $Y \in [-0.20, +0.20]\text{ m}$, sitting near the center ($Y_{\text{pelvis}} = -0.02..-0.055\text{ m}$) leaves $5.5..10.0\text{ cm}$ of cushion protruding in front of the pelvis (occluding the clinical examination zone) and causes the $0.380\text{ m}$ femur to terminate prematurely at $Y \approx -0.32\text{ m}$ — dropping the **knee cap (`Knee_Sphere`) onto the shell** while the lower leg hangs unsupported in mid-air.
* **The 3-Part Coupled Lithotomy Alignment Law:**
  1. **Anterior Pelvic Scoot (`Becken-Vorrutschen`):** The pelvis translates forward to $Y_{\text{pelvis}} = -0.155\text{ m}$ so the anterior pelvic border ($Y = -0.155 - 0.045 = -0.200\text{ m}$) is **100% flush with the anterior seat cushion edge ($Y_{\text{edge}} = -0.200\text{ m}$)**.
  2. **Posterior Pelvic Tilt (`Becken-Abknicken / Retroversion`):** Rotating the pelvis posteriorly ($\theta_{\text{pelvis},x} = -0.18\text{ rad} \approx -10.3^\circ$) tilts the pelvic outlet forward-upward into the free examination plane and elevates the hip sockets, while lumbar-thoracic counter-flexion ($\theta_{\text{back},x} = -0.34\text{ rad}$) bridges the shoulders and head cleanly back onto the backrest pad and neck roll.
  3. **Popliteal-to-Proximal-Rim Locking:** From $Y_{\text{pelvis}} = -0.155\text{ m}$, flexing and abducting the $0.380\text{ m}$ femur ($\vec{\theta}_{\text{thigh}} = [-1.74, \mp 0.28, \mp 0.64577]\text{ rad}$) places the **popliteal fossa (`Kniekehle`)** at $[\mp 0.308, -0.415, 0.805]\text{ m}$ — flush against the chair-facing entry rim of the Göpel shell ($\vec{\theta}_{\text{cradle}} = [0.32, \mp 0.14, \mp 0.64577]\text{ rad}$), allowing the flexed lower leg ($\theta_{\text{knee},x} = 0.86\text{ rad}$) to rest coaxially along the full $0.25\text{ m}$ trough.

---

### 1.4 Coordinate-Frame Orientation & Locomotion Integrity (`Yaw-Invarianz & Flanken-Treue`)
1. **Explicit Yaw Verification:** In a coordinate system where local forward is $-Y$, the world yaw $\psi$ required for an agent at $(x_A, y_A)$ to face a target $(x_T, y_T)$ is strictly:
   $$\psi_{\text{target}} = \text{atan2}(x_T - x_A,\; -(y_T - y_A))$$
   Any generated stance must satisfy the directional alignment assertion $\cos(\psi_{\text{actor}} - \psi_{\text{target}}) \ge 0.85$ so the agent never turns their back to the interaction partner or reaches backward behind their own spine.
2. **Ban on Translational Sliding in Spot-Turn Functions:** Stationary turn functions (`eval_turn_in_place`) may only be used for spot rotations ($\Delta XY \le 0.08\text{ m}$) or single-step weight shifts ($\Delta XY \le 0.20\text{ m}$). Feeding a $0.60\text{ m}$ linear translation into a spot-turn generator produces unnatural "ice-skating" across the floor.
3. **Camera Corridor Preservation:** Secondary operators must remain on their designated lateral workspace flank ($X \in [-0.66, -0.46]\text{ m}$), utilizing forward torso pitch and natural shoulder protraction to reach across the midline rather than stepping into the primary camera sightline (`SWM_Camera` $\to$ subject).

---

## 2. Backward Consideration (`Rückwärtsbetrachtung`): Inverse Visual Audit & Diagnostic Heuristics

When a human or multimodal AI inspects a rendered 3D/4D scene (Backward Interpretation), the following diagnostic heuristics expose hidden causal and algorithmic defects:

| Visual Symptom in Rendered Scene | Underlying Mathematical / Algorithmic Root Cause | Constructive Fix Layer |
| :--- | :--- | :--- |
| **Ghostly / Telekinetic Object Motion** (e.g., headrest slides up or both cradles move while hands hover in mid-air) | Furniture DOFs driven by global time windows $w(t)$ or coupled to other DOFs instead of being gated by World-Space effector contact ($\|\vec{P}_{\text{wrist}} - \vec{P}_{\text{handle}}\| \le 0.045\text{ m}$). | **Level 1 (`Inert Matter Law`) & Level 2 (`World-Space FK Anchors`)** |
| **Reverse Agency Illusion** (subject's legs appear to push the cradles outward by themselves) | Subject's limb abduction $\theta_{\text{thigh},z}(t)$ is interpolated simultaneously with $\theta_{\text{cradle},z}(t)$ while the operator's hands are retracted. | **Level 2/3 (`Hardware-First Authority Law`: operator locks cradle first, limb follows)** |
| **Hovering Hand Gap in Side View** (hand looks aligned from front, but floats $4\text{ cm}$ short of the backrest in profile) | Perspective foreshortening hides depth error; actor stands too far from target so `clamp_ik_reach(0.465 m)` clips the wrist in mid-air. | **Level 1 (`IK-Reach Workspace Audit` + Multi-View Orthographic Check)** |
| **Palm/Fingers Poking Through Thin Trough** | `wrist_pos` (joint root) placed at surface center without subtracting palm+finger length ($0.142\text{ m}$) along the approach vector. | **Level 1 (`Wrist-Root to Finger-Pad Surface Offset Law`)** |
| **"Stomach-Shot" Torso Crunch & Neck Break** | Backrest reclined too far (`-0.74 rad`) while pelvis stays forward, creating a $18\text{ cm}$ gap behind the spine; upward gaze applied 68% to neck pitch instead of eye pitch. | **Level 1/2 (`Pelvic Tilt Bridge` + `Eye-Dominant Ceiling Gaze Split`)** |
| **Ice-Skating & Behind-the-Back Reaching** | Low-compute heuristic shortcut: passing a long translational vector into `eval_turn_in_place` with an intuited (wrong-sign) yaw angle. | **Level 0 (`High-Compute Synthesis Gate`) & Level 1 (`Yaw Sign Assert`)** |