# SWM V6 Forward Training Record 03: The Inverse Affordance Cascade & The 5-Stage Mutability Law

**Repository:** `humanai2026/3D_Affrodance`  
**Direction:** Forward Generative Staging (`Intent & Psychology -> Object Mutability -> Affordance Anchor -> Inverse Body Chain -> 4D Keyframes`)  
**Core Discovery:** Why Absolute World Coordinates Fail in Embodied AI — and How Object Affordance plus Temporal Mutability ($\mu_{\text{obj}}$) Govern Human Movement.

---

## 1. The Architectural Defect of Static Coordinate Generation

When an LLM generates 3D/4D character interactions by predicting absolute world coordinates for hands and pelvis (`wrist_R_pos = [-0.35, -0.32, 0.78]`), any geometric modification to the environment (such as shortening a seat cushion by $12\text{ cm}$ or shifting a leg-holder socket forward) immediately invalidates the interaction:
1. **Phantom Grasping:** Hands float behind backrests (`Y > Y_back`) or reach into empty space behind a Göpel shell instead of applying force along the surface normal.
2. **Obstacle Clipping:** If the actor's standing position (`pelvis_pos.xy`) is not coupled to the displaced target object, the arm stretches across solid obstacles (e.g., slicing straight through an armrest pad).
3. **Self-Intersection during Posture Shifts:** When a seated actor slides their pelvis forward while reclining their torso backward, static world hand coordinates cause the forearms to sink into the rising abdominal wall (`Abdomen` mesh collision).

---

## 2. Law I: The 4-Stage Inverse Affordance Cascade (`Object -> Hand -> Shoulder -> Step`)

In embodied physical reality, human movement is never parameterized relative to a floor tile; it is computed **inversely from the live affordance of the target object**:

$$\mathcal{P}_{\text{object}}(q_{\text{obj}}(t)) \longrightarrow \vec{P}_{\text{wrist}}(t) \longrightarrow \vec{P}_{\text{shoulder}}(t) \longrightarrow \left(\vec{P}_{\text{pelvis}}(t),\; \psi_{\text{yaw}}(t),\; \theta_{\text{torso}}(t)\right)$$

### Stage 1 — Live Object Forward Kinematics (`P_affordance(q_obj)`)
At every frame $t$, query the exact 3D world position and surface normal of the mechanical contact feature directly from the object's live degrees of freedom $q_{\text{obj}}(t)$:
- **Backrest Upper-Front Edge (`Chair_Backrest_Pad`):** Rotating around $(0, Y_{\text{piv}}, 0.60)$ by $\theta(t) = \text{chair\_back\_rx}(t) < 0$:
  $$Y_{\text{top}}(\theta) = Y_{\text{piv}} - L_{\text{pad}}\sin(\theta), \quad Z_{\text{top}}(\theta) = 0.60 + L_{\text{pad}}\cos(\theta)$$
  $$Y_{\text{front}}(\theta) = Y_{\text{top}}(\theta) - \frac{d_{\text{pad}}}{2}\cos(\theta)$$
- **Göpel Cradle & Clamp Assembly (`Goepel_Shell_R/L`, `Goepel_Clamp_R/L`):** Given socket position $\vec{P}_{\text{sock}}$, ball-joint Euler angles $(\phi, \theta, \psi)$, and rod extension $e_{\text{rod}}$:
  $$\vec{P}_{\text{shell}}(t) = \vec{P}_{\text{sock}} + \mathbf{R}(\phi,\theta,\psi)\cdot \begin{bmatrix} 0 \\ 0 \\ L_0 + e_{\text{rod}}(t) \end{bmatrix}, \quad \vec{P}_{\text{clamp}} = \vec{P}_{\text{sock}} + \begin{bmatrix} \mp 0.032 \\ 0 \\ 0 \end{bmatrix}$$

### Stage 2 — Anatomical Wrist-Root to Finger-Pad Offset (`P_wrist`)
Because the kinematic target of an arm IK solver is the **Wrist Root (`Hand_Root`)** while physical contact occurs at the **palmar surface and curled fingers** ($L_{\text{palm}} = 0.074\text{ m}$, $L_{\text{fingers}} = 0.068\text{ m}$), offset $\vec{P}_{\text{wrist}}(t)$ against the surface approach normal $\hat{n}_{\text{surface}}$:
$$\vec{P}_{\text{wrist}}(t) = \vec{P}_{\text{affordance}}(q_{\text{obj}}(t)) + d_{\text{palm}}\cdot \hat{n}_{\text{surface}} + d_{\text{grasp}}\cdot \hat{t}_{\text{edge}}$$

### Stage 3 — Comfort Reach Envelope & Corridor Clearance Check
With total upper-limb length $L_{\text{arm}} = L_{\text{upper}}(0.28\text{ m}) + L_{\text{forearm}}(0.26\text{ m}) = 0.54\text{ m}$, verify at every frame $t$:
1. **Ergonomic Reach Inequality:** $0.28\text{ m} \le \|\vec{P}_{\text{wrist}}(t) - \vec{P}_{\text{shoulder}}(t)\| \le 0.45\text{ m}$.
2. **Obstacle Line-of-Sight Clearance:** The segment $\overline{\vec{P}_{\text{shoulder}}\vec{P}_{\text{wrist}}}$ must maintain $> 0.025\text{ m}$ clearance to all rigid furniture bounding boxes (e.g., `Chair_Armrest_R`).

### Stage 4 — Automatic Step-Forward & Torso Alignment
Whenever Stage 3 is violated (e.g., `Goepel_Shell_R` is at $Y = -0.44\text{ m}$, anterior to the armrest at $Y \in [-0.14, +0.18]\text{ m}$), the agent MUST execute a preparatory bipedal step (`eval_patient_facing_step`) to bring $\vec{P}_{\text{pelvis}}$ alongside the target ($Y_{\text{pelvis}} = -0.38\text{ m}$) and incline the torso ($\theta_{\text{back},x} = +0.18\text{ rad}$) before grasping.

---

## 3. Law II: The 5-Stage Temporal Causality of Object Mutability ($\mu_{\text{obj}}$) & Role Asymmetry

Inanimate objects possess not only spatial affordances, but a **Mutability State $\mu_{\text{obj}}(t) \in \{0\text{ (LOCKED)}, 1\text{ (FLEXIBLE)}\}$** — the *"changeability of changeability"*. In multi-agent interactions with asymmetric roles (`Operator / MTA_B` vs. `Recipient / Patient_A`), causal validity requires five strictly ordered temporal phases:

| Phase | Causal Stage | Mechanical & Kinematic Law | Psychological / Role Meaning |
| :--- | :--- | :--- | :--- |
| **1** | **Mental Target Conception ($q_{\text{obj}}^*$)** | Operator holds desired target geometry $q_{\text{obj}}^*$ in mind (e.g., deeper backrest $-0.68\text{ rad}$, abducted cradles). | Exercises planning sovereignty over the clinical space. |
| **2** | **Pre-Modification Contact at $q_{\text{obj}}(t_0)$** | Operator steps to the object and places hands at its **current initial state** $\vec{P}_{\text{affordance}}(q_{\text{obj}}(t_0))$. | Respects physical locality; no telekinetic pre-movement. |
| **3** | **Unlocking Mutability ($\mu: 0 \to 1$) & Guided Transformation** | Left hand actuates the lock/clamp screw ($\vec{P}_{\text{clamp}}$) or headrest slide; right hand guides the component along $\mathcal{Q}_{\text{mech}}$ from $q(t_0)$ to $q^*$. | Operator actively alters the boundary conditions of the environment. |
| **4** | **Fixation / Re-Locking ($\mu: 1 \to 0$)** | Operator tightens the clamp screw / engages the gas-spring lock at $t_1$ *before* releasing hand contact ($\Delta q_{\text{obj}} \equiv 0$ for $t > t_1$). | Converts a flexible mechanism into an immutable physical law. |
| **5** | **Recipient Adaptation ($\Omega_{\text{recipient}}$)** | Recipient (`Patient_A`) cannot reach or alter $\mu_{\text{obj}}$; she must adapt her own body joints ($\Omega_{\text{pat}}$) to the fixed geometry $q_{\text{obj}}^*$. | Mechanical fixation directly manifests as psychological exposure and loss of control. |

---

## 4. Law III: Body-Relative Self-Affordance & Compensatory Protective Extension

When an agent rests their hands on their own body (e.g., clasped hands shielding the anterior pelvic triangle), the agent's own torso and pelvis act as a **moving affordance surface**:

1. **Surface-Normal Ride (`Anti-Abdominal-Clipping`):** As the pelvis slides anteriorly ($\Delta Y < 0$) and tilts posteriorly ($\theta_{\text{pelvis},x} = -0.22\text{ rad}$), the wrist roots ride in the local pelvic coordinate frame above the abdominal wall ($Z_{\text{wrist}} = Z_{\text{pelvis}} + 0.068 + 0.018 w_{\text{recline}}$).
2. **Compensatory Distal Arm Extension (`Protective Shielding`):** As the backrest reclines to $-0.68\text{ rad}$ ($\approx 39^\circ$), the shoulders retreat posteriorly ($+Y$). If elbow flexion remained constant, the hands would be pulled upward onto the chest, exposing the pelvic triangle. To preserve visual shielding under increasing exposure, the agent **actively extends the elbows**, shifting the clasped hands further distally along the pelvic midline ($\Delta Y_{\text{protective}} = -0.035\text{ m}$).
3. **Gravity-Supported Occipital Rest & Invariant Leg Compensation:**
   - **Invariant World Leg Geometry under Deeper Recline:** Because `Thigh_R/L` are child nodes of `Pelvis`, tilting the pelvis by $\Delta\theta_{\text{pelvis},x} = -0.08\text{ rad}$ (from $-0.14$ to $-0.22\text{ rad}$) requires an exact counter-rotation of local hip flexion ($\Delta\theta_{\text{thigh,local},x} = +0.08\text{ rad}$, from $-2.12$ to $-2.04\text{ rad}$) so that the world knee apex and Göpel trough contact remain $100\%$ invariant.
   - **Occipital Cushion Surrender:** With `headrest_slide` extended to $+0.065\text{ m}$, the cervical spine relaxes from tense mid-air hovering ($+0.38\text{ rad}$) into gravity-supported occipital contact ($\text{nh\_rx} = +0.16\text{ rad}$) against `Chair_Headrest_Pad`, lifting only transiently ($\Delta\text{nh\_rx} = +0.24\text{ rad}$) during brief observational check-peeks.