# SWM V6 — Architectural & Biomechanical Learnings (2026-10-31: Klappe 4.7.3)
**Repository:** `humanai2026/3D_Affrodance`  
**Module:** Level 0 (Meta-Methodology) & Level 1 (Universal Biomechanics, Inverse Fixture Synthesis & C1 Locomotion)  
**Milestone:** Completion & Full QA Verification of Scene 2 (`Klappe 4.7.3`)

---

## Executive Summary: What an Embodied AI Must Know Before Frame 1 ("First-Shot Causal Readiness")

During the final synthesis of Scene 2 (`Klappe 4.7` to `Klappe 4.7.3`), we encountered and resolved five classic failure modes of LLM-based 3D/4D spatial reasoning:
1. **The "20-cm-Ball-in-15-cm-Hole" Optimization Trap:** Attempting to force human joint chains into arbitrary, pre-fixed furniture coordinates via iterative trial-and-error in the LLM reasoning window (resulting in ligament-breaking angles and reasoning timeouts).
2. **Rigid-Box Translation vs. Sacral-Anchor Pelvic Rolling:** Translating a seated human pelvis horizontally forward as a rigid block during backrest recline, which breaks lower-back contact with the backrest and leaves the actor sitting flat on the seat surface instead of rotating the pelvic ring.
3. **Diagonal Linear Interpolation Through Concave Obstacles:** Interpolating limb angles with a single monotonic weight $w(t)$, causing the shank to slice diagonally through the raised medial wall of a concave trough (`Goepel_Shell`) at Frame 103.
4. **1D Bottom-Point Contact vs. 2D Frustum-in-Annulus Concentric Bedding:** Aligning a tapered limb frustum (`r_knee = 48 mm`, `r_ankle = 36 mm`) to the lowest 1D floor point of a curved trough rather than its 2D center of curvature (`z_arc_center = +36.4 mm`), and failing to preserve the pitch-sum invariant ($\Delta\theta_{\text{knee}} = -\Delta\theta_{\text{thigh}}$) when raising the limb.
5. **Branch-Cut Singularity in Cone-Clamped Locomotion:** Clamping a walking actor's yaw relative to a workstation reference vector (`clamp(wrap_angle(psi_path - psi_chair))`), which triggers a discontinuous $180^\circ$ ($\pm\pi$) torso snap whenever the walking tangent crosses the antipodal direction (Frame 189).

Below are the six constructive First-Principles Laws that guarantee **First-Shot Success** without iterative coordinate patching.

---

## Law 1: The Psychology-to-Steel Inverse Fixture Design Law (`Inverses Bühnenbau-Gesetz`)

### 1.1 Root Cause of the Timeout Trap
When a 3D scene contains an articulated human interacting with a multi-DoF mechanical fixture (such as a clinical chair with ball-jointed Goepel leg supports), treating the fixture geometry (`holder_loc`) as an arbitrary constant forces the LLM into an over-constrained 6-DoF inverse kinematics search. If the fixture is mounted $10\text{ cm}$ too high or too close to the seat edge, no ligament-safe human joint configuration exists ("20-cm ball in a 15-cm hole").

### 1.2 Constructive First-Shot Algorithm (4-Stage Backward Chain)
Always synthesize the mechanical fixture **backward** from the desired psychological and anatomical end-state:
1. **Stage 1 — Define the Psychological & Anatomical Target Pose ($t = T_{\text{end}}$):**
   Specify the human's ligament-safe, expressive target joint angles first. For `Patient_A` in Scene 2 (`Frame 240`), `MTA_B` intends a wide, exposed V-abduction with posterior pelvic tilt:
   - $\mathbf{p}_{\text{pelvis}} = [0.0,\; -0.062,\; 0.672\text{ m}]$, $\mathbf{r}_{\text{pelvis}} = [-0.54,\; 0.0,\; 0.0\text{ rad}]$
   - $\mathbf{r}_{\text{thigh}, R/L} = [-1.7800,\; \pm 0.1207,\; \mp 0.5870\text{ rad}]$, $\theta_{\text{knee}, R/L} = +1.4846\text{ rad}$
2. **Stage 2 — Evaluate Human Forward Kinematics Once:**
   Compute the exact 3D world position of the calf center ($\mathbf{p}_{\text{mid-shank}, w}$) and the unit direction vector of the shank ($\mathbf{u}_{\text{shank}, w} = \text{norm}(\mathbf{p}_{\text{ankle}, w} - \mathbf{p}_{\text{knee}, w})$).
3. **Stage 3 — Analytically Solve Coaxial Fixture Orientation & Rod Vector:**
   Set the target rotation matrix $\mathbf{R}_{\text{shell}}$ of `Goepel_Shell_R/L` so its longitudinal trough axis ($-\mathbf{y}_{\text{local}}$) is 100% collinear with $\mathbf{u}_{\text{shank}, w}$ and its upward opening ($+\mathbf{z}_{\text{local}}$) has zero lateral bank:
   $$\mathbf{y}_{\text{shell}} = -\mathbf{u}_{\text{shank}, w}, \quad \mathbf{x}_{\text{shell}} = \frac{\mathbf{y}_{\text{shell}} \times [0,0,1]^T}{\|\mathbf{y}_{\text{shell}} \times [0,0,1]^T\|}, \quad \mathbf{z}_{\text{shell}} = \mathbf{x}_{\text{shell}} \times \mathbf{y}_{\text{shell}}$$
   From $\mathbf{R}_{\text{shell}} = \mathbf{R}_{\text{cpiv}}(\text{cradle\_target\_rpy}) \cdot \mathbf{R}_x(0.52)$, extract the exact target ball-joint Euler angles:
   $$\text{cradle\_target\_rpy}_{R/L} = [0.2887,\; 0.0000,\; \mp 0.3830\text{ rad}]$$
   Then solve directly for the local support rod vector `holder_loc` so the trough's concentric bedding line lies exactly at $\mathbf{p}_{\text{mid-shank}, w}$:
   $$\text{holder\_loc}_{R/L} = [\mp 0.0860,\; -0.1860,\; +0.2427\text{ m}]$$
4. **Stage 4 — Subtract the Dramatic Actuation Delta for the Start State ($t = 0$):**
   To visually stage `MTA_B` deliberately widening the V-spread in front of `Patient_A`'s eyes, define the pre-staged ball-joint orientation at $t = 0$ by subtracting the actuation excursion $\Delta\mathbf{q}_{\text{ball}} = [0.1287,\; 0.0,\; \mp 0.1230\text{ rad}]$:
   $$\text{cradle\_start\_rpy}_{R/L} = [0.1600,\; 0.0000,\; \mp 0.2600\text{ rad}]$$

---

## Law 2: The Sacral-Anchor & Posterior Pelvic Tilt Law (`Primärer Lehnen-Anker & Becken-Aufkippung`)

### 2.1 Biomechanical Principle
When a seated person reclines as a backrest lowers from $-0.38\text{ rad}$ to $-0.68\text{ rad}$, the lower lumbar/sacral contact zone at the base of the backrest acts as a **sliding rotational pivot (`Sacral Anchor`)** under gravity. The person does **not** translate forward as a flat, rigid block (which would open an unphysical $7\text{–}8\text{ cm}$ air gap behind the back and leave the perineal/pelvic floor planted flat on the horizontal cushion).

Instead, two coupled motions occur strictly synchronized with the backrest weight $w_{\text{backrest}}(t)$:
1. **Counter-Clockwise Posterior Pelvic Tilt ($\theta_{\text{pelvis}, x}: 0.0 \to -0.54\text{ rad} \approx -31^\circ$):**
   The upper pelvis (sacrum) tips backward into the reclining backrest pad ($\text{gap}_{\text{sacrum}} = -0.7\text{ mm}$), while the anterior/inferior pelvic floor rotates **forward and upward** by $+4.0\text{ cm}$ off the seat cushion ($Z_{\text{front}} = 0.652\text{ m}$ vs. cushion surface $0.612\text{ m}$), producing the anatomically required pelvic relaxation and clinical exposure.
2. **Flush Multi-Segment Spine & Occipital Rest:**
   With the pelvis already pitched to $-0.54\text{ rad}$, the lumbar (`abd_rx = -0.14 rad`) and thoracic (`thx_rx = 0.00 rad`) segments require minimal curvature to achieve the exact cumulative backrest angle:
   $$\theta_{\text{pelvis}, x} + \theta_{\text{abd}, x} + \theta_{\text{thx}, x} = -0.54 - 0.14 + 0.00 = -0.68\text{ rad} \equiv \theta_{\text{backrest}, x}$$
   This yields $+1.5\text{ mm}$ contact at the shoulder blades (`Thorax_Core`) and $+3.9\text{ mm}$ contact at the back of the head (`Head_Core` in `Chair_Headrest_Upper` at `headrest_slide = +0.055 m`, `nh_rx = +0.04 rad`).
3. **Parent-Child Pitch Compensation for Seated Thighs:**
   Because the thighs are children of `Pelvis`, rotating `Pelvis` by $\Delta\theta_{\text{pelvis}, x} = -0.54\text{ rad}$ would lift the resting thighs $31^\circ$ into the air during backrest recline unless compensated. The resting local thigh angle must counter-rotate by $+0.44\text{ rad}$ (`th_base_rx: -1.48 -> -1.04 rad`) so the world thigh pitch ($\theta_{\text{pelvis}, x} + \theta_{\text{thigh}, x} = -1.58\text{ rad}$) remains horizontal on the seat cushion until the active leg-lift window begins.

---

## Law 3: The 3-Phase Obstacle-Clearing Limb Placement Law (`Lift -> Abduct Over Rim -> Vertical Drop-In`)

### 3.1 Root Cause of Rim Clipping (Frame 103)
When placing a limb into a concave shell with raised side walls (`r_inner = 56 mm`, medial rim height $z_{\text{local}} = +21.9\text{ mm}$ at $x_{\text{local}} = +54.1\text{ mm}$), using a single interpolation weight $w(t)$ for both vertical lift and lateral abduction moves the calf along a diagonal secant line that slices directly through the medial shell wall. Furthermore, adding positive knee flexion (`+0.08 * w_arc`) during a hip lift drops the distal shank *downward* into the rim.

### 3.2 Constructive 3-Phase Trajectory Decomposition
To clear any concave receptacle wall cleanly:
1. **Phase-Windowed Abduction (`w_abd` nested inside `w_leg`):**
   For a leg placement window $[t_0, t_1]$ (`[0.350, 0.445]` for R, `[0.645, 0.740]` for L), delay abduction onset by $+0.022$ and complete abduction $-0.015$ *before* touchdown (`w_abd = window_weight(t, t0 + 0.022, t1 - 0.015)`).
2. **Synergistic Hip-Flexion + Knee-Extension Clearance Arc (`w_arc`):**
   Apply a strong upward clearance pulse `w_arc = pulse_weight(t, t0, t_peak, t1)` that simultaneously **flexes the hip higher** (`-0.30 * w_arc` on `th_rx`) and **extends the knee** (`-0.25 * w_arc` on `kn_rx`).
   - **Result:** The bottom surface of the calf rises to $z_{\text{local}} = +47\text{ to }+51\text{ mm}$ ($> 25\text{ mm}$ of clear air above the $+21.9\text{ mm}$ medial wall rim!) while crossing laterally over the wall, reaches $x_{\text{local}} = 0.0\text{ mm}$ above the trough center at $85\%$ of the window, and descends **purely vertically** along the centerline during the final 6 frames.

---

## Law 4: Concentric Frustum Bedding & Pitch-Sum Invariance (`Kegelstumpf-Bettung & Summenwinkel-Invarianz`)

1. **2D Center-of-Curvature Bedding (`z_local = +0.030 m`):**
   A human lower leg is a tapered frustum (`r = 48 mm` at knee, `42 mm` at mid-calf, `36 mm` at ankle) resting inside a cylindrical shell whose center of curvature lies at $z_{\text{arc\_center}} = 0.65 \cdot r_{\text{inner}} = +36.4\text{ mm}$. Placing the shank axis at $z_{\text{local}} = +22.4\text{ mm}$ (touching at the 1D bottom point for $r = 42\text{ mm}$) causes the wider proximal calf ($r = 46\text{ mm}$) and lateral frustum flanks to protrude through the curved lower/outer shell wall (Frame 180 defect). Bedding the shank axis at **$z_{\text{local}} = +30.0\text{ mm}$** (near the center of curvature) guarantees positive clearance across all 3D cross-sections from knee to ankle.
2. **Pitch-Sum Invariance ($\Delta\theta_{\text{knee}, x} = -\Delta\theta_{\text{thigh}, x}$):**
   Whenever the thigh flexion angle $\theta_{\text{thigh}, x}$ is adjusted by $\Delta\theta$ (e.g., from $-1.6554\text{ rad}$ to $-1.7800\text{ rad}$, $\Delta\theta = -0.1246\text{ rad}$) to raise the shank's elevation in the trough, the knee flexion angle $\theta_{\text{knee}, x}$ **must be incremented by $-\Delta\theta$** ($+1.3600 + 0.1246 = +1.4846\text{ rad}$) so that the global shank pitch angle $\theta_{\text{pelvis}, x} + \theta_{\text{thigh}, x} + \theta_{\text{knee}, x}$ remains invariant and parallel to the trough floor ($|x_{\text{local}}| \le 0.22\text{ mm}$).

---

## Law 5: C1 Geodesic Yaw Unwrapping Without Reference-Cone Clamping (`Geodätische Lauf-Stetigkeit`)

1. **The Antipodal Branch-Cut Trap:**
   Never clamp a walking actor's yaw to a stationary reference target via `yaw_ref + clamp(wrap_angle(path_yaw - yaw_ref), -c, +c)`. Whenever the walking trajectory circumvents an obstacle and its tangent vector `path_yaw` crosses $180^\circ$ ($\pm\pi$) relative to `yaw_ref`, `wrap_angle` jumps discontinuously from $-\pi$ to $+\pi$ in a single frame, whipping the actor's pelvis by $2c\text{ rad}$ ($> 100^\circ$).
2. **Constructive C1 Geodesic Law:**
   - Unwrap the baseline rotation strictly along the shortest great-circle arc:
     $$\psi_{\text{base}}(u) = \text{wrap}\big(\psi_{\text{start}} + u \cdot \text{wrap}(\psi_{\text{end}} - \psi_{\text{start}})\big)$$
   - For multi-step circumvention arcs ($n_{\text{cycles}} \ge 1.5$), blend smoothly into the forward walking tangent via a $C^1$ bell envelope $w_{\text{align}}(u) = \sin^{1.15}(\pi u)$:
     $$\psi_{\text{pelvis}}(u) = \text{lerp\_angle}\big(\psi_{\text{base}}(u),\; \psi_{\text{path}}(u),\; 0.72 \cdot w_{\text{align}}(u)\big)$$
   - For short clearance steps ($n_{\text{cycles}} < 1.5$), keep $\psi_{\text{pelvis}}(u) = \psi_{\text{base}}(u)$ monotonic and decompose the directional offset $\Delta\psi = \text{wrap}(\psi_{\text{path}} - \psi_{\text{pelvis}})$ into sagittal hip flexion ($\cos\Delta\psi \to \text{thigh\_rx}$) and coronal abduction ($\sin\Delta\psi \to \text{thigh\_ry}$).
