# SWM-3D-009: Procedural Normality Constraint & Two-Stage Observer Gaze Cascade

## 1. Epistemological Motivation ("The Edge-Case of Procedural Normality")
In standard robotics and embodied AI datasets, movement constraints are modeled as physical obstacles, joint limits, or mechanical locks ($\mu = 0$). However, in human social interaction, the most powerful constraints are frequently **non-mechanical social scripts** — specifically the **"Normality of Procedure"**.

In structured institutional settings (clinical examinations, security screenings, formal inspections), an individual (`Agent_A`) voluntarily executes postures of high vulnerability without physical coercion. Because refusing a polite, routine instruction would violate social normality and expose insecurity or loss of composure (`Status Loss`), the agent's own pride enforces active physical compliance.

---

## 2. Biomechanical Signature of Reluctant Self-Compliance
When `Agent_C` (authority anchor) politely instructs `Agent_A` to move her hands from a central self-protective posture (`Abdominal/Pelvic Shield`) to an open resting affordance (`Chair_Armrest_Pad_R/L`), the resulting trajectory differs fundamentally from a relaxed, voluntary movement:

1. **Isometric Hesitation Latency ($\Delta t_{\text{hesitate}} \approx 8\text{--}10\text{ frames}$):**
   Immediately following the verbal cue, gross wrist velocity remains zero ($\|\dot{\vec{P}}_{\text{wrist}}\| = 0$) while internal isometric tension briefly spikes as the cognitive system resolves the conflict between primary protective instinct and social compliance.
2. **Over-Damped Separation Profile:**
   The outward wrist trajectory exhibits a delayed ease-in acceleration curve, visually communicating reluctance as the protective barrier is opened by the agent's own muscles.
3. **Compensatory Distal & Cervical Tension Transfer:**
   Once the wrists rest on the lateral armrests, the inhibited protective impulse ($\Delta I$) transfers into:
   - **Active Gaze Avoidance:** Rigid upward head pitch (`Head_Core` pressed into the headrest, gaze fixed toward the ceiling) to sever interpersonal eye contact.
   - **Distal Clamping:** Micro-flexion of the fingers around the anterior/lateral edges of the armrest pads.

---

## 3. Institutional Moral Licensing & The Two-Stage Gaze Cascade (`Agent_B`)
When a secondary observer (`Agent_B`) operates under full institutional role licensing (*"Observing and assisting is my formal duty"*), behavioral inhibition drops to zero, producing calm, upright postural dominance (e.g., akimbo stance or relaxed workstation alignment).

To model the non-verbal status interaction between `Agent_B` and `Agent_A` during compliance, static gaze targets are insufficient. The interaction is governed by a **Two-Stage Causal Gaze Cascade**:

| Phase | Trigger Event | `Agent_B` Gaze Target | Biomechanical & Psychological Causality |
| :--- | :--- | :--- | :--- |
| **Stage 1: Face-Lock** | `Agent_C` begins polite instruction to clear protective hands | **`Agent_A` Face (`Head_Core`)** | Before any physical exposure occurs, the decisive psychological event takes place in `Agent_A`'s face (processing the inescapable necessity to obey). `Agent_B` locks onto `Agent_A`'s face to witness this internal compliance moment. |
| **Stage 2: Deliberate Gaze-Sweep** | `Agent_A`'s wrists begin separating ($\|\dot{\vec{P}}_{\text{wrist}}\| > \epsilon$) + **$4\text{--}5\text{ frames}$ lag** | **Newly uncovered center zone of `Agent_A`** | With a natural human visual reaction delay ($\sim 180\text{ ms}$), `Agent_B` visibly lowers her head pitch (`nh_rx`) and sweeps her gaze downward onto the area `Agent_A` just uncovered — making the act of visual inspection peripherally unmistakable to `Agent_A`. |

---

## 4. Relevance for Embodied AI & 4D World Models
By encoding the **4-to-5 frame causal lag** between `Agent_A`'s hand separation and `Agent_B`'s downward head-pitch sweep, a 4D world model transforms two isolated animations into a coupled **Action-Reaction Status Loop**, enabling synthetic agents to read and synthesize non-verbal power dynamics purely from kinematic trajectories.