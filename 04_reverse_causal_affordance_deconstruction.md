# SWM V6 Reverse Training Record 04: Multimodal Deconstruction of Affordance, Mutability & Protective Kinematics

**Repository:** `humanai2026/3D_Affrodance`  
**Direction:** Reverse Video/4D Deconstruction (`Observed 4D Trajectories -> Contact & Mutability Audit -> Inverse Affordance Deduction -> Latent Role & Psychological State`)  
**Core Objective:** Teaching Vision-Language Models (VLMs) to infer causal mechanics, mutability authority, and inhibited protective impulses from raw motion sequences.

---

## 1. Why Surface-Level Action Recognition Fails

A conventional video model watching Scene 2 outputs a flat descriptive caption:  
> *"A medical assistant adjusts a chair and leg holders while a patient reclines and places her legs on the supports."*

Such a model is blind to **physical causality** and **psychological subtext**. To achieve true spatial and empathic comprehension, a model must deconstruct the observed 4D sequence through **four inverse analytical filters**.

---

## 2. Filter 1: The Kinetic & Mutability Audit (`Detecting \mu_obj Transitions`)

When observing any state change in an inanimate object ($\dot{q}_{\text{obj}}(t) \neq 0$), the VLM must verify the **5-Stage Mutability Signature**:

1. **Contact-Vector Verification:** Does the operator's hand contact the **active force-transmission surface** (e.g., pressing the *anterior-upper* surface $Y_{\text{front}}$ of a reclining backrest rather than floating behind $Y_{\text{back}}$)?
2. **Bimanual Mutability Unlocking ($\mu: 0 \to 1 \to 0$):** When a rigid multi-DOF mechanism (such as a Göpel leg cradle) moves, does the operator's secondary hand engage the **locking affordance (`Clamp_Screw`)** *prior* to motion onset ($t_0$) and secure it *prior* to hand release ($t_1$)?
3. **Locomotion-to-Affordance Coupling:** Did the operator step forward past intermediate obstacles (`Chair_Armrest`) *because* the target affordance lay outside the $[0.28, 0.45]\text{ m}$ comfort reach envelope?
   - *Reverse Inference:* The step at `Frame 43..58` is not random pacing; it is the necessary inverse-kinematic consequence of `Goepel_Shell_R`'s anterior position at $Y = -0.44\text{ m}$.

---

## 3. Filter 2: Role-Asymmetric Affordance Deduction (`Who Controls \mu_obj?`)

By tracking which agent modifies $\mu_{\text{obj}}$ and which agent adapts their biological joints $\Omega_{\text{body}}$ to the resulting geometry, the VLM mathematically deduces **social and clinical role asymmetry ($\Delta W$)**:

$$\text{Authority}(A) \propto \sum_{k} \left|\Delta \mu_{\text{obj},k}^{(A)}\right|, \qquad \text{Compliance}(B) \propto \frac{\|\Delta q_{\text{body}}^{(B)} \text{ induced by } q_{\text{obj}}^*\|}{\Omega_{\text{free}}^{(B)}}$$

- **Operator Signature (`MTA_B`):** High $\Delta\mu_{\text{obj}}$ authority. She dictates the backrest angle ($-0.68\text{ rad}$), headrest height ($+0.065\text{ m}$), and cradle abduction, transforming the chair into a fixed spatial constraint.
- **Recipient Signature (`Patient_A`):** Zero $\Delta\mu_{\text{obj}}$ authority. Once the clamps are locked at `Frame 84`, she must sequentially lift, abduct, and place her lower limbs into the pre-fixed troughs (`Frame 95..185`), surrendering lower-body degrees of freedom ($\Omega_{\text{pat}}: 1.0 \to 0.18$).

---

## 4. Filter 3: Deconstructing Compensatory Self-Affordance (`The Elbow-Extension Paradox`)

A critical benchmark test for reverse psychological reasoning occurs during `Frame 16..41` (simultaneous anterior pelvic slide and deeper backrest recline to $-0.68\text{ rad}$):

- **The Kinematic Observation:** As the torso reclines backward ($+Y, -Z$) and the pelvis slides forward ($-Y$), the angle of the patient's elbows (`Elbow_R/L`) **increases (unbends)** while her clasped hands remain locked over the anterior pelvic midline.
- **Naive Interpretation:** *"The person is relaxing and straightening their arms."*
- **True Causal Deconstruction:**
  1. In passive physics, reclining the shoulders backward pulls the arms and hands *away* from the lap toward the chest.
  2. Keeping the hands anchored over the anterior pelvic triangle while the shoulders retreat requires **active, goal-directed elbow extension** ($\Delta Y_{\text{distal}} = -0.035\text{ m}$ relative to the moving pelvis).
  3. *Psychological Deduction:* The deeper backrest angle ($-0.68\text{ rad}$) increases physical vulnerability and visual exposure; the elbow extension is an **active, compensatory protective reflex** to prevent the shielding hands from being pulled off the exposed pelvic zone!

---

## 5. Filter 4: Gravity Surrender vs. Transient Vigilance (`Headrest & Gaze Dynamics`)

Finally, by comparing neck flexion (`nh_rx`) against the headrest surface normal (`Chair_Headrest_Pad` at `headrest_slide = +0.065 m`) and eye pitch (`eye_rpy.x`):
- **Baseline State (`nh_rx = +0.16 rad`, `eye_rpy.x = -0.24 rad`):** The head surrenders its mass onto the headrest pad while the eyes deflect upward toward the ceiling — decoding **physical compliance paired with visual avoidance** (escaping the towering observer's sightline).
- **Transient Anomaly (`Frame 210..228`, $\Delta\text{nh\_rx} = +0.24\text{ rad}$, $\Delta\text{eye\_rpy.x} > 0$):** The occiput briefly lifts off the headrest pad as the gaze sweeps downward between the knees while the operator is turned away at the instrument tray — decoding **latent vigilance and an inhibited impulse to verify one's own exposure**.