# SWM-3D-011: Bidirectional Time-Arrow, Popliteal Sit-Back & Distal Fidgeting Law
**Artifact Type:** First-Principles Causal Training Record (Level 0, Level 1 & Level 3 World-Model Architecture)  
**Repository:** `humanai2026/3D_Affrodance`  
**Date:** `2026-11-02`  
**Context:** Scene 3 Synthesis (`Klappe 4.8.1` Unidirectional Keyframe Interpolation vs. `Klappe 4.8.4` Bidirectional Closed-Loop CoT & Visual Audit)

---

## 1. Executive Summary: Why LLMs Fail Physical & Social Plausibility in Their First Shot

When an LLM synthesizes a 4D multi-actor scene (`240 frames`) in a **unidirectional forward pass ($t_0 \to t_{\text{end}}$)** by interpolating isolated keyframe coordinates, five systematic world-model failures emerge:

1. **The As-the-Crow-Flies Fallacy (`Topological Blindness`):**
   - *Symptom:* The actor walks straight through a swinging door blade (`Door_Panel`) and cuts through a room partition wall (`Privacy_Partition` at $Y = -1.72\text{ m}$).
   - *Root Cause:* Checking only whether $P_{\text{start}}$ and $P_{\text{end}}$ are collision-free, treating the intermediate space as an empty Euclidean plane rather than a **topological corridor bounded by impenetrable 2D/3D line segments (walls and swept door arcs)**.
2. **Tool-Slave Affordance Inversion (`Prio 2 Overriding Prio 1`):**
   - *Symptom:* The doctor sits on the rolling stool with her **back turned to the patient** (`yaw = 0.0` instead of `yaw = +pi`), while her hands reach backward behind her spine toward the patient.
   - *Root Cause:* Enslaving the human's pelvis orientation to the unrotated stool's local backrest affordance (**Prio 2**) instead of subordinating the mobile tool to the human's primary task vector (**Prio 1: face the patient**).
3. **Coordinate-Sign & Anterior-Halfspace Blindness (`Missing Egocentric Body-Compass`) & Telekinesis:**
   - *Symptom:* Arms twist $180^\circ$ behind the torso, or a mobile cart (`Assist_Mayo_Stand`) rolls across the room while the actor's hand floats $30\text{ cm}$ away in mid-air because `clamp_ik_reach` severed the hand-to-cart contact.
   - *Root Cause:* Missing local pelvis halfspace verification (`inv_rot_euler_xyz`) and moving furniture without guaranteeing that the actor's shoulder stays within unclamped reach ($\le 0.44\text{ m}$) of the grip point throughout the motion.
4. **The Mid-Air Squat Jump vs. Stool-Through-Shin Paradox (`Missing Popliteal Rim Mechanics`):**
   - *Symptom A (Mid-Air Jump):* Flexing the hips/knees to $-1.38\text{ rad}$ before the stool arrives causes both feet to lift $19\text{ cm}$ off the floor in a comical mid-air cannonball jump.
   - *Symptom B (Stool Through Shins):* Pulling the stool directly under the standing center of mass ($Y_{\text{stool}} \approx Y_{\text{standing pelvis}}$) while the legs are vertical drives the circular seat cushion ($R = 0.188\text{ m}$) and star base ($R = 0.23\text{ m}$) straight through the standing shins.
5. **The "She Bop" Wrist-Oscillation Fallacy (`Proximal vs. Distal Nervousness`):**
   - *Symptom:* Adding $\pm 15\text{ mm}$ translational sine waves to `wrist_R_pos` / `wrist_L_pos` while the hands are shielding the lower abdomen causes the entire forearm-elbow IK chain to pump rhythmically across the lap.
   - *Root Cause:* Confusing **proximal limb translation** with **distal finger/toe micro-motor agitation**.

---

## 2. The 4-Step Pre-Code Mental Simulation Loop (`First-Shot CoT Standard`)

Every scene synthesis MUST execute this four-step mental simulation loop in its Chain-of-Thought (CoT) **before** emitting code:

### Step 1: Teleological Backward Pass ($t_{\text{end}} \to t_0$), Affordance Priority (`Prio 1 > Prio 2`) & Bent-Arm Envelope
Construct the scene **backward from the final human-to-human interaction state ($t_{\text{end}}$)**:
- **Law of Task Dominance (`Prio 1 Task-Vector > Prio 2 Tool-Affordance`):**
  - Freeze the human interaction pose first: `Doctor_C` seated at `[0.00, -0.865, 0.632]` facing `Patient_A` at $+Y \implies \text{yaw} = +\pi$.
  - Subordinate mobile tools to Prio 1: `Doctor_Rolling_Stool` arrives at `[0.00, -0.92, 0.0]` with `stool_rz = -\pi` so its backrest supports `Doctor_C` at $-Y$.
- **Bent-Arm Elbow Envelope & Distal Foot Clearance (`Law 7c`):**
  - Two adjacent actors with bent arms require **$\ge 0.72\text{ m}$ pelvis-to-pelvis distance** so elbows never collide, and standing actors must keep **$\ge 0.40\text{ m}$ 2D clearance** from the patient's feet in the Goepel shells (`[-0.38, -0.55]`).
  - Canonical Frame 240 Triad: `Doctor_C` at `[0.00, -0.865, 0.632]`, `MTA_B` at `[-0.74, -0.82, 0.80]` (`yaw = +2.38 rad`, $74.1\text{ cm}$ pelvis spacing), `Assist_Mayo_Stand` at `[-1.18, -0.52, 0.0]`.

### Step 2: Topological Corridors, Unclamped Hand Coupling & Popliteal Sit-Back ($t_0 \to t_{\text{end}}$)
- **Sightline Corridors & Shore-Line Buffers:** Maintain $\ge 0.45\text{ m}$ clearance to walls (`Privacy_Partition` at $Y = -1.72\text{ m}$) and $\ge 0.28\text{ m}$ to the inward-opening door blade (`door_rz: 0.0 -> -1.28 rad`).
- **Hard Hand-to-Furniture Coupling (`No Telekinesis`):** Before moving `Assist_Mayo_Stand` (`Frame 126..190`), `MTA_B` steps to `[-0.82, +0.02, 0.80]` and rotates her torso to `yaw = +2.68 rad` so her left shoulder is $0.402\text{ m}$ from the right tray rim (`0.01 mm` unclamped grip error throughout the pull).
- **Popliteal Rim Sit-Back Law (`Kniekehlen-Kanten-Gesetz / "Stuhl-wegzieh-Physik"`):**
  1. *Standing Stool Pull Behind Calves (`Frame 148..178`):* `Doctor_C` stops upright at `[0.00, -0.70, 0.798]` with her ankles planted at $(Y_{\text{ankle}} = -0.675\text{ m}, Z_{\text{ankle}} = 0.030\text{ m})$, pulling the stool behind her calves to `[0.00, -0.92, 0.0]`. At hip width $X = \pm 0.105\text{ m}$, the circular seat cushion ($R = 0.188\text{ m}$) has half-chord $\Delta Y = \sqrt{0.188^2 - 0.105^2} = 0.1559\text{ m}$, so its front rim sits at $Y_{\text{rim}} = -0.92 + 0.1559 = -0.7641\text{ m}$ — leaving a clean **$4.7\text{ cm}$ air gap behind her standing calves**.
  2. *Planted-Foot Diagonal Sit-Back (`Frame 178..208`):* With her ankles pinned at $(Y_{\text{ankle}} = -0.675\text{ m}, Z_{\text{ankle}} = 0.030\text{ m})$ via exact 2-link sagittal inverse kinematics (`solve_planted_foot_sit_ik`), her knees flex forward while her pelvis hinges **diagonally backward and downward** (`Y: -0.700 -> -0.865 m`, `Z: 0.798 -> 0.632 m`) over the free air gap onto the waiting cushion:
     $$d = \hypot(Y_{\text{ankle}} - Y_{\text{hip}}, Z_{\text{hip}} - Z_{\text{ankle}}), \quad \gamma = \text{atan2}(Y_{\text{ankle}} - Y_{\text{hip}}, Z_{\text{hip}} - Z_{\text{ankle}})$$
     $$\alpha = \arccos\!\left(\frac{L_{\text{th}}^2 + d^2 - L_{\text{sh}}^2}{2 L_{\text{th}} d}\right), \quad \theta_{\text{thigh,rx}} = -(\gamma + \alpha)$$

### Step 3: Egocentric Body-Compass & Anterior-Halfspace Comparator (`Soll-Ist-Regelkreis`)
In the SWM V6 rig, local forward (nose, glasses, sternum) is **$-Y_{\text{local}}$**, local right shoulder is **$-X_{\text{local}}$**, and local left shoulder is **$+X_{\text{local}}$**:
$$\vec{F}(\psi) = \begin{bmatrix} +\sin(\psi) \\ -\cos(\psi) \end{bmatrix}, \quad \vec{R}(\psi) = \begin{bmatrix} -\cos(\psi) \\ -\sin(\psi) \end{bmatrix}, \quad \vec{L}(\psi) = \begin{bmatrix} +\cos(\psi) \\ +\sin(\psi) \end{bmatrix}$$

| Desired World Facing Direction | Forward Vector $\vec{F}$ | Required Pelvis `yaw` ($\psi$) | Right Shoulder Offset | Left Shoulder Offset |
| :--- | :--- | :--- | :--- | :--- |
| **South (`-Y`, away from patient)** | $(0, -1)$ | `0.0 rad` (`0°`) | $(-0.188, 0)$ | $(+0.188, 0)$ |
| **East (`+X`, from hallway into room)** | $(+1, 0)$ | **`+1.5708 rad` (`+90°`)** | $(0, -0.188)$ | $(0, +0.188)$ |
| **North-East (`+X, +Y`, MTA witness angle)** | $(+0.71, +0.71)$ | **`+2.38 rad` (`+136°`)** | $(+0.13, -0.13)$ | $(-0.13, +0.13)$ |
| **North (`+Y`, Doctor facing Patient)** | $(0, +1)$ | **`+3.1416 rad` (`+180°`)** | $(+0.188, 0)$ | $(-0.188, 0)$ |
| **West (`-X`, into hallway)** | $(-1, 0)$ | `-1.5708 rad` (`-90°`) | $(0, +0.188)$ | $(0, -0.188)$ |

- **Anterior-Halfspace Law:** Transform every world-space wrist target $\vec{w}_{R/L}$ into the actor's local pelvis frame via `inv_rot_euler_xyz(w - pelvis_pos, pelvis_rpy)`. Because $-Y_{\text{local}}$ is anterior, **`local_y` must never exceed `+0.08 m`**.

### Step 4: Distal-Only Fidgeting vs. Tonic Freeze & Cliffhanger Micro-Mimicry (`Level 3 Psychology`)
- **Anchored Shield Wrists, Distal Finger/Toe Agitation (`Law 6b`):** Keep `wrist_R_pos` and `wrist_L_pos` translationally still (`hand_dx = hand_dy = hand_dz = 0.0`) when shielding a vulnerable body zone. Express pre-freeze autonomic arousal (`Frame 1..210`) purely through distal finger kneading (`fingers_r/l_rpy`) and alternating toe-play (`toes_r/l_rpy`), then snap to `0.0` oscillation with 100% tonic flexion (`toes = +0.36 rad`, `fingers = +0.85 rad`, `foot_roll = ±0.24 rad`) at Frame 212.
- **5% Subcortical Cliffhanger Duel (`Law 6c`, Frame 210..240):**
  - `Patient_A` (`Vicky` — *Resignation*): Slight occipital press (`nh_rx = +0.06 rad`), **downward gaze drop** (`eye_rpy = [+0.22, 0.0, 0.0]`, positive `eye_rx` = down!), narrowed eyes (`eye_scale = 0.78`), downward mouth corners (`mouth_rpy = [+0.12, 0.0, 0.0]`).
  - `MTA_B` (`Hannah` — *Voyeuristic Triumph*): Locked in `Stage 1 Face-Lock`, **5% predatory eye-widening** (`eye_scale = 1.18`), minimal asymmetric judgmental smirk (`mouth_rpy = [-0.08, +0.14, +0.06]`, `nh_ry = +0.035 rad`).
