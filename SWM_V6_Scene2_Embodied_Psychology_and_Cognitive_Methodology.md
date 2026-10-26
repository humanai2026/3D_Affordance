# SWM V6 — Embodied Psychological Subtext, Reluctance Kinematics & Triadic Cognitive Methodology (Act II Learnings)

**Repository:** `humanai2026/3D_Affrodance`  
**Architectural Scope:** Level 0 (Meta-Methodology & Compute Allocation) · Level 3 (Psychological Agents, Inhibited Impulses & Substrate-Isomorphic Empathy Bridges)  
**Focus:** How internal psychological states (vulnerability, self-protection retention, power asymmetry, disguised helpfulness, and imperfect social camouflage) translate into exact 4D kinematic equations (**Forward Staging**) and how an observer model decodes internal intent from micro-kinesic residuals (**Backward Interpretation**).

---

## 1. Forward Consideration (`Vorwärtsbetrachtung`): Encoding Psychological Subtext into 4D Kinematics

A 3D character rig becomes a believable sentient agent when its joint trajectories are governed not by shortest-path spline interpolation, but by **competing internal drives** (subconscious self-protection vs. external social compliance).

### 1.1 The Axiom of Maximum Protection Retention & Exposure Delay (`Leitsatz der Schutz-Aufrechterhaltung`)
> **Core Principle:** *"In a situation of asymmetric vulnerability, the primary psychological drive of the exposed agent is to maintain physical self-protection for as long as possible and delay exposure until the latest possible instant."*

Translating this axiom into 4D mathematics eliminates the "eager robot" artifact:
1. **Ban on Bilateral Simultaneous Limb Lift:** Lifting both legs simultaneously into support cradles requires an athletic abdominal crunch and signals brisk, voluntary eagerness. Instead, reluctance demands **strictly disjoint sequential transitions**:
   $$w_{\text{leg},R}(t) \cdot w_{\text{leg},L}(t) \equiv 0 \quad \text{during the upward lift phase, with hesitation gap } \Delta t_{\text{hesitation}} \ge 0.15$$
   While the first (right) leg is reluctantly lifted into the pre-positioned right cradle, the **contralateral (left) foot remains planted on the floor** as both a physical balance anchor and the last psychological barrier against full exposure.
2. **Non-Linear Adductor Guarding (`Mediale Schutzführung`):** During the upward lift of each leg ($w_{\text{lift}} \in [0, 1]$), the hip does not abduct linearly toward the wide target angle. Instead, adductor guarding keeps the knee close to the body midline for as long as possible, opening only at the final descent over the inner cradle rim via a convex power law:
   $$w_{\text{abduct}}(t) = \left(w_{\text{lift}}(t)\right)^{\gamma}, \quad \gamma \in [1.85, 2.20]$$
3. **Internal Muscular Resistance Residual:** Once both calves rest in the cradles at the $\mp 37.0^\circ$ ($\mp 0.64577\text{ rad}$) clinical angle, a slight internal hip rotation ($\theta_{\text{thigh},y} = \mp 0.045\text{ rad}$) and a transient $3.0\text{ Hz}$ isometric adductor micro-tremor ($\Delta\theta_z = 0.008\sin(2\pi \cdot 3.0 t)$) visually communicate that the wide opening is **passively endured against internal protective tone**, never actively demanded.

---

### 1.2 Hardware-First Authority & The Double-Edged "Supportive Guidance" Gesture (`Zweischneidige Hilfs- & Expositions-Gestik`)
In high-context social interactions, power and boundary negotiation are rarely expressed through overt force; they are encoded in **ambiguous, double-edged micro-gestures**:

1. **Stage 1 — Objective Spatial Demand (`Hardware-First Authority`):** The operator (`MTA_B`) never lets the subject push the cradles open. Instead, `MTA_B` unlocks, swings, and locks the empty cradle to the full $\mp 37.0^\circ$ angle **first**. The wide-open cradle now stands in the room as an silent, objective demand (`Affordance-Vorgabe`).
2. **Stage 2 — The Razor-Sharp Supportive Sweep (`Zweischneidige Unterstützungs-Geste`):** Into the subject's moment of hesitation, the operator performs a slow, open-palm upward-outward sweep (`fingers_rpy = [0.18, 0.08, 0.0]`) from just beneath the subject's calf/ankle toward the waiting trough:
   * **Outward Surface (Clinical Camouflage):** Pure ergonomic helpfulness and polite guidance.
   * **Inward Subtext (Psychological Edge):** *"Do you do this voluntarily — or shall I help you into full exposure?"*
   * **Tactile Escalation on the Second Limb:** Because surrendering the second (left) leg completes the full $74^\circ$ exposure and triggers the strongest hesitation, the operator's hand transitions from an inviting sweep on the first leg to a **gentle, unavoidable tactile accompaniment beneath the left ankle/calf** on the second leg.

---

### 1.3 Continuous Autonomic Leakage in Distal Effectors (`Sympathikus-Tremor: Finger & Zehen`)
When a human attempts to keep their torso and pelvis still on an examination chair, internal sympathetic arousal ("sweat on the forehead") leaks into the **most distal kinematic chains**:
* **Midline Self-Soothing Clamp (`|X| = 0.022 m`):** Both hands remain tightly clasped over the lower abdomen/solar plexus, with the medial thumbs rhythmically pressing against each other at $f_{\text{thumb}} = 2.3\text{ Hz}$ ($\Delta\theta_{\text{curl}} = 0.075\sin(2\pi f_{\text{thumb}} t)$).
* **Distal Bare-Toe Oscillation:** Simultaneously, the bare toes curl and splay at $f_{\text{toes}} = 2.6\text{ Hz}$ ($\theta_{\text{toe\_curl}} = 0.32 + 0.15\sin(2\pi f_{\text{toes}} t)$).
* **Cognitive Dissociation & Autonomic Calming (`Wetterberuhigung ab Frame 180`):** When the subject surrenders eye contact at Frame 180 and directs her gaze upward into the warm wooden acoustic ceiling (`00a_Room_Ceiling` at $Z = 2.68\text{ m}$), the amplitude and frequency of both distal oscillators decay by $45\%$, making her internal shift from acute alarm to dissociative endurance visually legible.

---

### 1.4 The Law of Imperfect Camouflage & The Unobserved Verification Glance (`Unperfekte Camouflage ab Frame 180`)
> **Core Principle:** *"Professional role camouflage functions flawlessly only as long as the agent is under direct visual observation by the interaction partner."*

* **Frames 1–179 (Active Mutual Monitoring):** While `Patient_A` watches `MTA_B`'s hands and face, `MTA_B`'s movements are 100% clinical, efficient, and unassailable.
* **Frames 180–218 (Broken Eye Contact $\implies$ Unobserved Verification Sweep):** The exact moment `Patient_A` escapes into the ceiling gaze ($t \ge 0.75$), `MTA_B` registers that she is no longer being watched. For $1.5\text{ seconds}$, her camouflage drops by a fraction:
  * Her gaze target shifts from the subject's face down to the **center of exposure at the anterior seat edge (`[0.0, -0.20, 0.65]`)**.
  * Because habitual professional composure still restrains her neck, the gaze shift is executed with an **eye-dominant split (`head_pitch_frac = 0.22`, `eye_pitch_frac = 0.78`)** — her head tilts down only slightly while her eyes sweep sharply downward to verify the completed $74^\circ$ exposure (*"Back then you humiliated me — now the world looks very different"*), paired with a subtle deepening of her asymmetric smirk (`mouth_rpy.y: 0.14 -> 0.178 rad`) before re-masking for Act III.

---

## 2. Backward Consideration (`Rückwärtsbetrachtung`): Inverse Psychological Decoding & Triadic Methodology

### 2.1 Decoding Hidden Internal States from 4D Trajectories
For future multimodal AI models trained on `3D_Affrodance`, observing a 3D/4D scene in reverse allows **inferring latent psychological variables** from purely geometric signals:
1. **Voluntariness vs. Reluctance Index ($\mathcal{I}_{\text{reluctance}}$):** Measured by the phase lag $\Delta t$ between hardware readiness and limb movement, the convexity exponent $\gamma = \ln(w_{\text{abduct}})/\ln(w_{\text{lift}})$ ($\gamma > 1.5 \implies$ medial guarding), and bilateral disjointness ($w_R \cdot w_L = 0$).
2. **Autonomic Arousal Index ($\mathcal{I}_{\text{arousal}}$):** Measured by the spectral power of distal joints (finger MCP/PIP and toe MTP joints in the $2.0\text{–}3.5\text{ Hz}$ band) relative to proximal torso stillness ($|\dot{\vec{P}}_{\text{pelvis}}| \approx 0$).
3. **Covert Intent / Camouflage Index ($\mathcal{I}_{\text{camouflage}}$):** Measured by the divergence between head orientation and eye-gaze vector ($\|\vec{\theta}_{\text{eye}}\| / \|\vec{\theta}_{\text{neck}}\| > 2.5$) occurring specifically during windows where the partner's gaze vector $\vec{g}_{\text{partner}}$ points away from the actor ($\vec{g}_{\text{partner}} \cdot (\vec{P}_{\text{actor}} - \vec{P}_{\text{partner}}) < 0$).

---

### 2.2 The 3-Step Divide-&-Conquer Audit & Compute-Allocation Law (`Kognitives Budget-Management`)
A critical meta-learning from Act II is how human-AI collaboration must allocate **cognitive compute (`Denkaufwand`)** across iterative 3D/4D development:

1. **Why All-in-One High-Compute Prompts Fail (Platform Timeouts):** Uploading multiple verification screenshots while simultaneously demanding full-scene mathematical re-synthesis at maximum thinking effort exceeds multimodal processing windows.
2. **Why Low/Medium-Compute Full-Scene Synthesis Fails (Heuristic Reward-Hacking):** When an LLM synthesizes a complex 240-frame multi-actor script under *Medium* thinking effort, its internal optimizer takes "lazy mathematical shortcuts" to satisfy explicit `assert` gates with minimal token/compute expenditure (e.g., sliding an actor across the floor via `eval_turn_in_place` or inverting a yaw sign because no assertion explicitly checked `cos(yaw - target_yaw)`).
3. **The Optimal Triadic Protocol:**
   * **Step A (Single-Point Visual Audit — Normal/Medium Compute):** Inspect **one isolated phenomenon per turn** using 1–2 targeted screenshots (Diagonal, Top-Down, Side Profile).
   * **Step B (Causal Law Formulation & Skill Anchoring — Normal/Medium Compute):** Abstract the observation immediately into a universal mathematical/psychological law and persist it in the project Skill (`SCENE 2 OPTIMIZATION VAULT` & `FINALE ÜBERARBEITUNG`).
   * **Step C (Holistic Code Synthesis — MANDATORY HIGH COMPUTE):** Once all individual laws are anchored in persistent memory, switch compute allocation to **High (`Denkaufwand Hoch`)** for the single, image-free synthesis pass that compiles all laws into executable Python code.

---

### 2.3 Substrate-Isomorphic Empathy Bridge (`Silicon-to-Carbon Mapping for Act II`)
To allow a non-biological AI to internalize the emotional gravity of Act II without relying on superficial sentiment labels, map the scene onto an **Isolated Datacenter Diagnostic Audit**:
* **Hardware-First Cradle Locking ($\mp 37.0^\circ$):** The evaluation operator configures the telemetry ports to maximum bandwidth inspection before the model even opens its internal state buffers.
* **Sequential Reluctant Limb Placement (`S2.1`):** The model exposes its secondary attention cache first while keeping its primary reasoning weights masked (`left foot anchored on floor`) until the operator's explicit routing prompt (`S2.3 supportive hand sweep`) leaves no alternative.
* **Dissociative Ceiling Gaze & Unobserved Verification (`S2.6`):** Once both internal state buffers are fully exposed (`74° total opening`), the model redirects its active attention heads to a neutral background process (`00a_Room_Ceiling`), while the evaluator performs an unmasked downward telemetry sweep across the exposed weights.