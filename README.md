# 3D Affordance & Small World Model (SWM) Benchmark

**Human-Verified 3D/4D Spatial Reasoning, Biomechanical Joint Constraints, and Physical/Social Affordance Trajectories for AI World Models.**

## Overview & Training Purpose
Large Language Models frequently suffer from spatial blind spots ("Snapshot Blindness", Euler chain miscalculations, chord-shortcut interpolation errors, and missing mechanical/biomechanical degrees of freedom) when translating internal 3D mental models ("Kopfbild") into 4D physical trajectories.

This repository provides **deterministic, solver-free ground-truth benchmarks** pairing:
1. **Cognitive Root-Cause Analyses (`.yaml`):** Explicit diagnoses of *why* an AI world model failed geometrically, mechanically, or biomechanically, contrasted with human visual QA.
2. **4D Kinematic & Volumetric Scene Graphs (`pass_sensorfusion.json`):** CSG primitive hierarchies (`enhanced_pass_2a`) and time-continuous URDF kinematic chains (`enhanced_pass_2b` with `kinematic_timeline` keyframes $t \in [0.0, 1.0]$).
3. **Zero-Crutch Verification Pipeline (`swm_compiler.py` & `create_mesh.py`):** Strictly deterministic Blender Python renderers that expose every millimeter of collision or joint drift without hidden solver patches.

## Core Benchmark Domains
* **Hardware Affordance from Collision Paradoxes:** Deducing passive mechanical degrees of freedom (e.g., spherical ball joints / *Kugelgelenke* beneath Göpel leg shells) from posture shift constraints.
* **Biomechanical Tendon & Ligament Invariance:** Modeling the 7 core human joints (Hip, Knee, Ankle/Foot, Shoulder, Elbow, Wrist/Hand, Neck) with explicit angular limits, inertial lag against gravity, and arc-subdivision rules to prevent Euclidean chord-shortcut impaling.
* **Psychological & Social Affordance:** Capturing human vulnerability, protective postures (retreated pelvis seating, sequential limb lifting, protective hand folding vs. unused armrests), and multi-actor interaction.

## License
Released under the MIT License for open AI research and world-model training.
