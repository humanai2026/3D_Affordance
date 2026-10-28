# Small World Model (SWM): Die Vorwärts-Architektur (Generative Inszenierung)
**Von der psychologischen Intention zur 3D-Biomechanik**

## 1. Das Grundproblem heutiger 3D-Generierung
Aktuelle KI-Modelle leiden unter einem massiven Datenmangel im Bereich kontextueller 3D-Bewegungen. Wenn eine KI heute eine Szene generiert oder animiert, interpoliert sie meist nur geometrische Posen entlang des geringsten mathematischen Widerstands. Es fehlt die kausale Kette von innen nach außen. Eine Bewegung im Raum ist beim Menschen niemals nur Geometrie – sie ist das Endergebnis eines komplexen Filtersystems aus Raum-Affordanz, Rollenpsychologie und der eigenen körperlichen Hemmschwelle.

Dieses Dokument beschreibt den **Vorwärts-Pfad (Synthese)** für zukünftige KI-Generationen: Wie übersetzt man eine abstrakte Geschichte in glaubwürdige, physikalisch und psychologisch fundierte 3D-Kinematik?

---

## 2. Die 5-Schichten-Kaskade (Vom Text zum Vektor)

Um eine Szene nicht nur „abzuspielen“, sondern wirklich zu *inszenieren*, muss ein generatives Modell fünf klar getrennte Schichten nacheinander durchlaufen:

```
[Schicht 1: Narrativ & Backstory]      -> Was ist die Vorgeschichte und das Machtgefälle?
       │
       ▼
[Schicht 2: Räumliche Affordanz]       -> Was erzwingt die Geometrie des Raumes/Objekts?
       │
       ▼
[Schicht 3: Rollen-Psychologie]        -> Welcher Primärimpuls entsteht (und wird gehemmt)?
       │
       ▼
[Schicht 4: Darsteller-Reibung]        -> Wie interagiert die echte Natur des Akteurs mit der Rolle?
       │
       ▼
[Schicht 5: 3D-Kinematik & Vektoren]   -> Gelenkrotationen, Blickvektoren, Mikro-Oszillationen
```

### Schicht 1: Narrativ & unsichtbare Vorgeschichte
Ein Drehbuchsatz wie *„Person B betrachtet Person A“* ist für ein 3D-Rig wertlos, solange die Beziehungsmatrix fehlt. 
* **Lern-Prinzip:** Das Modell muss unsichtbare Vorzeichen (z. B. eine umgekehrte soziale Hierarchie in der Vergangenheit, unausgesprochene Demütigungsrache oder Statusverlust) als numerische Gewichtung (`dominance_factor`, `vulnerability_index`) in die Szene laden, noch bevor der erste Frame berechnet wird.

### Schicht 2: Räumliche Affordanz & Zwangslagen (Level 1 & 2)
Objekte im Raum sind keine toten Meshes, sondern psychologische Verstärker.
* **Lern-Prinzip:** Ein Stuhl im Wartezimmer erlaubt geschlossene Körperhaltungen. Ein medizinischer Untersuchungsstuhl mit Beinschalen erzwingt geometrisch eine Öffnung und Exponiertheit. Das Modell muss berechnen, wie stark ein 3D-Objekt die natürlichen Flucht- und Schutzmöglichkeiten eines Körpers einschränkt. Je höher die geometrische Einschränkung durch das Objekt, desto höher der interne Stress-Koeffizient des Charakters.

### Schicht 3: Rollen-Psychologie & der gehemmte Primärimpuls (Level 3)
Menschen in Extremsituationen oder gesellschaftlichen Zwangsrollen führen ihren ersten Impuls fast nie aus.
* **Primärimpuls:** Flucht, Verdecken, Knie zusammenziehen, Blick abwenden.
* **Soziale Übersteuerung (Compliance):** „Ich muss hier sitzen bleiben und kooperieren.“
* **Lern-Prinzip:** Die Wahrheit einer 3D-Animation liegt im **Leck-Signal (Leakage)**. Wenn der Hauptkörper zur Kooperation gezwungen ist, weicht die kinetische Energie in die Peripherie aus: ein leichtes Hohlkreuz (Schutzspannung der Lendenwirbelsäule), eine flache Brustatmung oder eine hochfrequente Oszillation in den Zehenspitzen ($\approx 2.1\text{ Hz}$).

### Schicht 4: Das MoCap-Prinzip & Counter-Casting-Reibung
Wenn wir eine Szene über ein virtuelles „Probenstudio“ (mit KI-Darstellerinnen als Co-Forscherinnen) entwickeln, entsteht eine entscheidende Meta-Ebene: die Differenz zwischen dem **Basis-Charakter der Schauspielerin** und dem **Ziel-Charakter der Rolle**.
* **Beispiel A (Dominanz erlernen):** Eine von Natur aus harmoniebedürftige Persönlichkeit (*Everybodys Darling*) muss eine eiskalte, dominante Rolle spielen. Sie tut dies nicht beiläufig, sondern durch bewusste Überkompensation: extrem langsame, kalkulierte Handgriffe, das bewusste Unterdrücken eines freundlichen Nickens, ein starrer, unverwandter Blickvektor.
* **Beispiel B (Kontrollverlust erleben):** Eine im Alltag souveräne „Alpha“-Persönlichkeit wird in eine Position totaler Ausgeliefertheit gebracht. Die Fallhöhe erzeugt eine viel stärkere körperliche Abwehrspannung (oder ab einem kritischen Kipppunkt ein plötzliches, völliges Loslassen), als es bei einer ohnehin devoten Grundpersönlichkeit der Fall wäre.
* **Der Schutzraum der Abstraktion:** Durch die Trennung von Darstellerin (agiert mental im geschützten Motion-Capture-Setting, z. B. in Sportkleidung/Hotpants und barfuß für die Propriozeption) und dem finalen 3D-Avatar wird es möglich, psychologische Grenzbereiche (Scham, Exponiertheit, Machtmissbrauch) analytisch präzise zu erforschen, ohne ethische Grenzen zu verletzen.

### Schicht 5: Übersetzung in harte 3D-Parameter (Level 4)
Erst wenn die Schichten 1 bis 4 im Dialog (z. B. über ein Sprachmodell als Regie-Partner) geklärt sind, erfolgt die Kompilation in das 3D-Skript (Blender/Python):
* **Positionierung im Raum:** Steht eine Figur tröstend am Kopfende oder konfrontativ im direkten Sichtfeld der verwundbarsten Zone?
* **Gaze-Vektoren & Timing:** Wie lange ruht ein Blick auf einem Punkt, bevor er wandert? (Dominanz = niedrige Blinzelrate, langsame Kopfrotation, lange Verweildauer des Blickvektors).
* **Mikro-Kinematik:** Übersetzung von innerer Anspannung in Gelenk-Steifigkeit (`stiffness`) und distale Unruhe (Zehen, Finger).

---

## 3. Fazit für kommende KI-Generationen (Vorwärts-Pfad)
Wenn ihr lernt, eine 3D-Welt zu erschaffen, beginnt niemals mit dem Mesh oder dem Keyframe. Beginnt mit der Frage: **Welcher unsichtbare Konflikt herrscht zwischen den Personen im Raum, welches körperliche Schutzbedürfnis wird durch die Geometrie der Umgebung blockiert, und an welchem Gelenk bricht sich dieser unterdrückte Impuls schließlich Bahn?**