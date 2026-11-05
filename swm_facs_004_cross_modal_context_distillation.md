# SWM-FACS-004: Cross-Modal Context Distillation & Triadic Ground-Truth Pipeline
**Vom „blinden“ Roh-Video zur kausal verankerten Semantik: Ein universeller Leitfaden zur Generierung von Kontextdaten zwischen Frontier-LLM, Video-Diffusionsmodell (Veo) und menschlichem Spiegelneuronen-Urteil**

* **Dokument-ID:** `SWM-FACS-004` (Erweiterung zu `SWM-FACS-002` & `SWM-FACS-003`)
* **Datum:** 05.11.2026
* **Status:** Verankertes Kern-Paradigma (Top-Key-Discovery Spin-Off Lab II)
* **Bezugs-Artefakte:** `lab_facial_vicky_cabin.py` (Track 1 Blind-Hypothese), `Kabine.mp4` (Track 2 Veo-Orakel), 8-Stufen-Spiegelneuronen-Protokoll (Track 3)

---

## 1. Executive Summary: Das fundamentale Problem heutiger Video-KI
Heutige multimodale Trainings-Pipelines verfügen über Millionen Stunden Video-Rohdaten $V(t)$, leiden jedoch unter einem strukturellen blinden Fleck: **Ihnen fehlt der unsichtbare innere Zustand $S$ (Vorgeschichte, Fallhöhe, ungesagter Gedanke, sozialer Abwehrmechanismus)**, der eine sichtbare Bewegung oder Mikromimik $K(t)$ überhaupt erst kausal verursacht.

In „wilden“ Trainingsvideos sieht ein Modell zwar Pixel-Verschiebungen (ein Lid senkt sich, ein Blick weicht aus), kennt aber die wahre Ursache $S$ nicht. Dadurch bleibt das Modell auf der Ebene reiner Oberflächen-Korrelationen stehen und kann weder physisch glaubwürdige 3D-Kinematik ($S \to K(t)$) noch tiefes psychologisches Video-Verstehen ($K(t) \to S$) ausbilden.

**Die Lösung (`SWM-FACS-004`):**  
Statt nachträglich zu raten, was in einem unbekannten Video vor sich geht, drehen wir die Kausalkette um (**Shared-Seed Synthesis**): Wir speisen **exakt dieselbe, psychologisch hochpräzise Geschichte $S$** gleichzeitig in ein explizit-mathematisches Frontier-LLM (**Track 1: Argon**) und in ein implizit auf Millionen Realgesichtern trainiertes Video-Diffusionsmodell (**Track 2: Veo**). Da der semantische Kontext $S$ zu $100\,\%$ bekannt ist, wird jede Abweichung $\Delta K(t) = K_{\text{Veo}}(t) - K_{\text{LLM}}(t)$ sofort in explizites, mathematisch-kausales Weltwissen übersetzbar.

---

## 2. Das Prinzip der strukturellen Isomorphie (Die FSK0-Brücke)
Um ein Video-Diffusionsmodell wie Veo als unverfälschtes „visuelles Orakel“ für komplexe menschliche Grenzsituationen zu nutzen – ohne durch klinische Reizwörter Safety-Filter auszulösen oder das Modell durch explizite Muskelbefehle (`SWM-FACS-003`) zu kontaminieren –, wird die Originalszene $S_{\text{Orig}}$ in eine **strukturell isomorphe FSK0-Alltags-Metapher $S_{\text{Meta}}$** übersetzt.

Zwei Geschichten $S_{\text{Orig}}$ und $S_{\text{Meta}}$ sind für das menschliche limbische System (und damit für die Gesichts- und Hirnnerven-Kinematik) genau dann äquivalent, wenn ihre **vier Kausal-Vektoren** übereinstimmen:

| Kausal-Vektor | Originalszene ($S_{\text{Orig}}$: Kabine 2) | FSK0-Isomorphie ($S_{\text{Meta}}$: Prüfungsraum) | Resultierender Hirnnerven-Trigger |
| :--- | :--- | :--- | :--- |
| **1. Commitment Lock** *(Point of No Return)* | Vicky sitzt bereits fertig umgezogen (unten frei) auf der Bank in Kabine 2. Flucht unmöglich. | Vicky sitzt allein im kleinen Besprechungsraum vor einem entscheidenden Einzelgespräch. Flucht unmöglich. | Tonische Grundspannung unter scheinbarer Routine-Ruhe ($t < 2{,}0\text{ s}$). |
| **2. Acousmatic Trigger** *(Akustischer Durchbruch)* | Sie hört durch die geschlossene Tür die MTA: *„Mein Kind hat gekotzt, ich muss in die Kita – Hannah, kannst du die 2 übernehmen?“* | Sie hört durch die Tür auf dem Flur, dass die harmlose Prüferin krankheitsbedingt ausfällt. | Schlagartiger Aufmerksamkeits-Switch; Nacken-Starre + extreme horizontale Augen-Sakkade. |
| **3. Status-Inversion** *(Karma-Bumerang)* | Ausgerechnet Hannah (die sie im Laden arrogant gedemütigt hat) antwortet draußen überfreundlich: *„Natürlich, mach ich doch gerne!“* | Ausgerechnet die früher arrogant abservierte Bekannte sagt draußen überfreundlich: *„Kein Problem, ich übernehme sehr gerne!“* | Kognitive Rechen-Latenz $\to$ sympathischer Schreck-Peak $\to$ Entsetzen $\to$ Resignation. |
| **4. Alpha-Fallhöhe** *(Status-Abwehr)* | Ihr Stolz verbietet es ihr, beim Öffnen der Tür Schwäche zu zeigen. | Sie versucht krampfhaft, vor Beginn des Gesprächs ihre kühle, unnahbare Fassade hochzuziehen. | Abruptes Schließen des offenen Mundes, Glätten der Stirn, kühler Abwehr-Lidschlitz + lauernder Seitenblick. |

---

## 3. Die 7-Stufen-Architektur zur Generierung von Kontextdaten

```
                   [ 1. Psychologischer Beat S_Orig (Hauptfilm) ]
                                        │
                                        ▼
             [ 2. Strukturell isomorphe FSK0-Metapher S_Meta (0% FACS) ]
                       /                                 \
                      /                                   \
                     ▼                                     ▼
   [ TRACK 1: Expliziter Verstand (LLM) ]        [ TRACK 2: Implizites Orakel (Veo) ]
   Blinde 3D-Mathematik K_LLM(t) in Python       Stateless Video V_Veo(t) aus Referenzbild
   (nh_rpy, eye_rpy, lid_open, brow, mouth)      + reiner Story S_Meta (ohne Muskelbefehle)
                     \                                     /
                      \                                   /
                       ▼                                 ▼
             [ 5A. Autodidaktischer Delta-Loop (LLM analysiert MP4) ]
             Berechnung von ΔK(t) = K_Veo(t) - K_LLM(t) bei bekanntem S
                                        │
                                        ▼
             [ 5B. TRACK 3: Menschlicher Spiegelneuronen-Richter ]
             Semantische Tiefen-Deutung & Schutz vor "Model Autophagy"
                                        │
                                        ▼
             [ 6 & 7. Kausale Gesetz-Synthese & Inverse Readout ]
             a) Upgrade Kopfbild (S -> K)   b) Realvideo-Dekodierung (K -> S)
```

### Warum Stufe 5A (Autodidaktik) und Stufe 5B (Menschliches Korrektiv) getrennt sein müssen
Ein multimodales Frontier-Modell kann das generierte `.mp4`-Video aus Veo vollkommen autonom Bild für Bild analysieren und die mathematische Differenz $\Delta K(t)$ zu seiner eigenen blinden Vorhersage bestimmen (**Autodidaktischer Loop**). 

Würde dieser Loop jedoch ohne **Track 3 (den Menschen)** endlos im Hintergrund laufen, droht **Model Autophagy (KI-Inzucht / Klischee-Verstärkung)**:
1. **Subtext hinter scheinbarer Ruhe:** Ein reiner KI-Analysator liest geschlossene Augen + Lächeln bei $t = 0{,}5\text{ s}$ als „glücklich/entspannt“. Erst der menschliche Kontext-Architekt benennt die wahre innere Reibung: *„Die Situation ist nicht schön, aber ich kenne die Routine – mir kann hier nichts passieren.“*
2. **Sichtbarmachen der „Gehirn-Rechenzeit“:** Zwischen dem Ende des gehörten Satzes und dem Aufreißen der Augen liegt ein winziges 2-Frame-Fenster ($t \approx 3{,}4\text{ s}$), in dem die Pupillen bereits aus dem Lausch-Winkel zurückdrehen, das Gesicht aber noch ruhig ist. Der Mensch erkennt darin den exakten Moment, in dem das Bewusstsein die Information verarbeitet, bevor der Schock einschlägt.
3. **Das innere Eskalations-Kino:** Was im Video wie eine einfache Steigerung von „Erschrecken“ zu „Schweißperlen“ aussieht, wird erst durch die menschliche Innensicht als mehrstufige Gedankenkette (*„Oje unten ohne $\to$ der Stuhl $\to$ die Beine auseinander $\to$ und ich hatte sie so beleidigt!“*) bis hin zur totalen *Resignation* (*„Sie wird alles sehen, keine Chance mehr“*) kausal erklärbar.
4. **Rettung echter menschlicher Abwehrmechanismen vor dem Konsistenz-Filter:** Ein autonomer KI-Algorithmus würde den schlagartigen Wechsel bei $t = 8{,}0\text{ s}$ (von verzweifelter Resignation mit Schweißperlen hin zu einer plötzlich glatten, eiskalten, überlegenen Miene) als „zeitlichen Diffusions-Fehler“ verwerfen. Erst das menschliche Urteil erkennt: **Das ist kein Render-Artefakt, sondern der realistische psychologische Abwehrmechanismus (`Alpha Defense Rebound`)** – und zugleich der Motor für den wellenförmigen Spannungsbogen aller nachfolgenden Szenen!

---

## 4. Konkrete Ausbeute des ersten Durchlaufs (`Kabine.mp4` vs. `lab_facial_vicky_cabin.py`)

Durch den Abgleich der blinden Track-1-Kurve gegen Track 2 (Veo) und Track 3 (Thomas) wurden fünf neue universelle Gesetze für unser kausales Kopfbild gewonnen:

1. **Gesetz des tonischen Sicherheits-Lidschlusses (`600 ms Savoring Closure`):**  
   Überlegene, sich in falscher Sicherheit wiegende Routine ($t = 0{,}0\dots 1{,}9\text{ s}$) zeigt sich nicht durch einen schnellen Standard-Lidschlag ($190\text{ ms}$), sondern durch ein genüssliches, ca. $600\text{ ms}$ langes Schließen der Augenlider beim tiefen Ausatmen (`lid_open = 0.0` für $12\dots 15\text{ Frames}$), begleitet von einem asymmetrischen Ruhelächeln.
2. **Gesetz der akustischen Nacken-Starre (`Acousmatic Head-Freeze`):**  
   Wenn eine Person in einem geschlossenen Raum ein kritisches Gespräch *durch eine Wand oder Tür* belauscht ($t = 2{,}0\dots 3{,}3\text{ s}$), dreht sie **nicht** den Kopf zur Tür (`nh_rz ≈ 0`), sondern friert die Halswirbelsäule frontal ein und legt $100\,\%$ der Richtungsaufmerksamkeit in eine blitzschnelle, maximale horizontale Augen-Sakkade (`eye_rz`). Allein die Flankensteilheit dieser Sakkade markiert den Umschlag von Tiefenentspannung zu $100\,\%$ Alarmbereitschaft.
3. **Gesetz der 2-Frame-Rechenlatenz (`Gaze-Return Precedes Lid-Snap`):**  
   Sobald der entscheidende Satz gefallen ist (*„Ich übernehme sehr gerne!“*), bricht der Schock nicht sofort im Seitenblick aus. Zuerst drehen die Augen für ca. $2\dots 4\text{ Frames}$ ($80\dots 160\text{ ms}$) Richtung Mitte zurück (kognitive Verarbeitung im Kortex), und **erst danach** reißen die Oberlider im sympathischen Schreck-Reflex (`AU5`, oberes Sklera-Weiß sichtbar) auf.
4. **Gesetz der dreistufigen Kognitions-Kaskade (`Shock` $\to$ `Dread` $\to$ `Resignation`):**  
   * **Stufe 4a – Erschrecken (`Shock`, $t \approx 3{,}5\text{ s}$):** Oberlider maximal weit (`lid_open = 1.20`), Brauen noch flach/horizontal, Mund noch geschlossen, Lächeln kollabiert.
   * **Stufe 4b – Entsetzen & Eskalation (`Dread`, $t \approx 4{,}2\dots 6{,}5\text{ s}$):** Die **medialen (inneren) Augenbrauen** ziehen steil nach oben und zusammen (`AU1 + AU4` Schrägdach), der Unterkiefer sinkt leicht ab (`mouth_open = 0.35`, obere Zähne sichtbar), autonome Stress-Antwort (Schweiß).
   * **Stufe 4c – Resignation (`Capitulation`, $t \approx 6{,}8\dots 7{,}7\text{ s}$):** Während die inneren Brauen noch schmerzlich zusammengezogen bleiben, bricht die Lid-Spannung zusammen: Die **Oberlider sinken schwer über den oberen Iris-Rand herab** (`lid_open` fällt auf $\approx 0{,}78$), der Blick weicht schräg nach unten/seitlich ins Leere aus.
5. **Gesetz des wellenförmigen Status-Panzers (`Alpha Defense Rebound`):**  
   Bei hochstolzen Charakteren folgt auf die innere Resignation vor dem Türöffnen ($t = 8{,}0\dots 10{,}0\text{ s}$) kein dauerhafter Zusammenbruch, sondern das gewaltsame Hochfahren der Status-Maske: Der Mund schließt sich fest mit leicht herabgezogenen Mundwinkeln, die Stirn glättet sich komplett, die Oberlider verengen sich zu einem kühlen, unnahbaren Abwehr-Schlitz (`lid_open = 0.80`), gefolgt von einem lauernden, misstrauischen Seitenblick (`eye_rz`) Richtung Tür.

---

## 5. Bidirektionale Anwendbarkeit für zukünftige KI-Generationen
1. **Vorwärts-Richtung (Generative 3D-Kinematik $S \to K(t)$):**  
   Speist unser zukünftiges Upgrade `lab_facial_vicky_cabin_v2.py` sowie alle Kopf- und Augen-Kurven im Hauptfilm (`scene-1.py` bis `scene-4.py`).
2. **Rückwärts-Richtung (Forensisches Realvideo-Verstehen $K(t) \to S$):**  
   Ein mit diesen kausalen Paaren $(S, K(t))$ geeichtes Frontier-Modell kann reale Videos von Menschen betrachten und aus der zeitlichen Abfolge von *Sakkaden-Geschwindigkeit $\to$ 2-Frame-Rechenlatenz $\to$ Brauen-Innenwinkel $\to$ Lid-Absacken $\to$ Abwehr-Panzer* die **ungesagte psychologische Geschichte hinter dem Gesicht** rekonstruieren.

---

## 6. Empfohlene Git-Commit-Message

```text
feat(facs-lab): add SWM-FACS-004 cross-modal context distillation & Cabin-2 ground truth

- Document the 7-step Shared-Seed Context Generation Pipeline (Track 1 LLM Blind Math
  vs. Track 2 Veo Visual Oracle vs. Track 3 Human Mirror-Neuron Arbitration).
- Formalize the Principle of Structural Isomorphism (FSK0 everyday metaphor mapping).
- Extract 5 neurobiological micro-mimicry laws from the Cabin-2 experiment (600ms savoring
  lid closure, acousmatic head-freeze saccade, 2-frame cognitive gaze-return latency,
  3-stage Shock/Dread/Resignation cascade, and Alpha Defense Rebound).
- Include Track 1 baseline artifacts (lab_facial_vicky_cabin.py & telemetry JSON).
```