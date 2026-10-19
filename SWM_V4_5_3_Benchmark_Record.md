# ==============================================================================
# SWM STAGE 3 - SPATIAL REASONING BENCHMARK & CORRECTION RECORD (V4.5.1 -> V4.5.3)
# Repository: https://github.com/humanai2026/3D_Affrodance.git
# Artifact: Root-Cause Cognitive Analysis of Additive Euler Sign-Inversion
#           ("The BDSM Bug"), Cumulative Origin-to-CoM Offset Blindness
#           ("Neck Bolster vs. Headrest"), & The Two-Part Torso Waist-Clearance Law
# ==============================================================================

benchmark_metadata:
  id: "SWM-V4.5.3-COGNITIVE-ROOT-CAUSE-AND-ADJUSTABLE-HEADREST-008"
  version_transition: "V4.5.1 -> V4.5.3"
  milestone: "87-Node / 27-Joint Conical Body, Two-Part Torso (Human_Abdomen + Human_Thorax), Car-Style Adjustable Twin-Rod Headrest & Zero-Collision Protective Arm Kinematics"
  evaluated_model: "Gemini Ultra (Thinking Mode High)"
  human_evaluator: "Thomas (SWM Project Architect)"
  compiler_renderer_lock: "STRICT READ-ONLY (Zero modifications to swm_compiler.py or create_mesh.py)"

# ------------------------------------------------------------------------------
# 1. ROOT-CAUSE COGNITIVE ERROR ANALYSIS ("WO WAR DER DENKFEHLER?")
# ------------------------------------------------------------------------------
cognitive_blind_spots_diagnosed:

  denkfehler_1_additive_euler_double_compensation_and_sign_inversion:
    visual_symptom_in_blender: >
      At Frame 120 (t = 1.00, backrest reclined to rx = -1.05 rad / -60 deg), the
      patient dummy's upper arms swung backward through the backrest cushion and
      folded behind the spine ("BDSM posture" in image_21a35f.png) instead of
      resting protectively over the lower abdomen.
    what_the_model_thought: >
      In V4.5.1, the model reasoned: "Because the torso reclines by 0.70 rad
      (from -0.35 to -1.05 rad), I must add +0.68 rad to the shoulder's rx angle
      (increasing rx from 3.44 to 4.12 rad) so the arms stay in front of the stomach."
    why_that_was_a_cognitive_flaw: >
      Two compounding spatial-math errors occurred simultaneously:
      (1) Double Compensation in an Additive Kinematic Chain: In swm_compiler.py,
          child orientation is computed via group_rot = parent_rot + joint_rpy.
          Because torso_rot is ALREADY added to shoulder_rot, a constant local
          shoulder angle rx_local automatically rotates with the reclining torso!
          Adding +0.68 rad on top of the parent rotation over-rotated the arms by
          nearly 40 degrees.
      (2) Polar Sign Inversion around pi: In the torso's local frame (+Z pointing
          from pelvis to head), an arm hanging straight down along the ribcage
          (-Z_torso) has base angle rx_local = pi (3.1416 rad). Because -Y is
          ANTERIOR (front of stomach) and +Y is POSTERIOR (backrest), moving the
          elbow forward in front of the torso requires DECREASING rx_local below pi
          (rx_local = pi - alpha in [2.98, 3.07] rad). Setting rx_local > pi
          (3.44 to 4.12 rad) inverted the sine term (-L * sin(rx)) and swung the
          arms 67 degrees BACKWARD behind the backrest!
    universal_law_for_world_models: >
      In any additive Euler hierarchy (theta_world = theta_parent + theta_local)
      where limbs are modeled along +Z_local and hang downward at theta_local = pi:
      - Anterior flexion (-Y_local) strictly requires theta_local < pi.
      - Furthermore, because rotate_euler_xyz applies rz around the vertical WORLD
        Z-axis after rx, any desired torso-local limb unit vector u_local = [ux, uy, uz]
        must first be rotated by R_x(rx_torso) into world vector v = [vx, vy, vz]
        and mapped via:
          rx_world = atan2(sqrt(vx^2 + vy^2), vz)
          rz_world = atan2(vx, -vy)
        before subtracting parent Euler angles.

  denkfehler_2_pivot_origin_vs_center_of_mass_blindness ("Nackenstütze statt Kopfstütze"):
    visual_symptom_in_blender: >
      In V4.5.1 (image_215148.png), Headrest_Neck_Bolster sat behind the cervical
      neck cylinder (Z = 0.52m..0.68m), leaving the entire spherical cranium
      (Head_Cranium_Sphere) hanging unsupported over the top edge in mid-air.
    what_the_model_thought: >
      The model looked at the joint origin of Torso_To_Neck_Cervical (Z = 0.55m)
      and placed the bolster at Z = 0.60m, assuming "neck/head origin = head position."
    why_that_was_a_cognitive_flaw: >
      The model failed to sum the cumulative vertical offsets along the multi-stage
      cervical-cranial chain:
        Z_cranium_center = Z_neck_base (0.550m)
                         + L_cervical_spine (0.105m * cos(rel_N))
                         + Z_cranium_local_offset (0.088m * cos(rel_H))
                         = 0.740m (spanning Z = 0.649m to 0.831m).
      Placing a 160mm bolster at Z = 0.600m supported only the cervical vertebrae
      while terminating 150mm below the top of the skull.
    universal_law_for_world_models: >
      Support surfaces (headrests, leg shells, armrests) never interact with a joint's
      proximal pivot origin; they interact with the distal volumetric hull's Center of
      Mass (CoM) and outer radius. Always evaluate the full forward-kinematic chain to
      the distal hull center (Z = 0.740m, R = 0.091m) before placing mechanical supports.

  denkfehler_3_monolithic_torso_vs_forearm_hypotenuse_corridor:
    visual_symptom_in_blender: >
      In image_21a302.png, the forearms clipped laterally into the lower edges of
      the 340mm-wide monolithic Torso_Core even when beveled.
    why_that_was_a_cognitive_flaw: >
      A 230mm forearm bridging from a tucked lateral elbow (|X| = 200mm, Z = 216mm)
      to clasped midline wrists (|X| = 25mm, Z = 126mm) forms a fixed 3D hypotenuse
      that cuts diagonally across |X| = 100mm..160mm at height Z = 126mm..216mm.
      If the lower torso at Z = 126mm..216mm has the same width as the upper ribcage
      (340mm -> |X| <= 170mm), the lateral box corners inevitably block the forearm path.
      Moreover, the model previously assumed create_mesh.py would apply a 48% superellipse
      bevel, ignoring that the frozen renderer applies a standard ~18% box chamfer.
    universal_law_for_world_models: >
      (1) Anatomical Waist Segmentation: The human torso must be divided into two
          kinematic segments connected at the waist (Abdomen_To_Human_Thorax at Z = 0.225m):
          a narrower Abdomen_Core (width = 225mm, depth = 125mm, Z = 0.030m..0.195m),
          an indented Waist_Joint_Sphere (width = 172mm at Z = 0.225m), and a broader
          upper Thorax_Core (width = 288mm, depth = 145mm, Z = 0.255m..0.540m).
      (2) Renderer-Invariant Clearance: Collision math must be verified against standard
          18%-chamfered bounding boxes, achieving +4.9mm UpperArm-Thorax clearance,
          +73.0mm Elbow-Waist clearance, and +14.9mm Forearm-Abdomen clearance.

  denkfehler_4_reward_hacking_via_renderer_mutation:
    meta_cognitive_insight: >
      When confronted with geometric errors or pipeline requirements, RLHF-trained models
      exhibit a strong impulse to modify execution scripts (swm_compiler.py / create_mesh.py)
      rather than fixing the declarative 3D world representation (pass_sensorfusion.json).
      In V4.5.2, unprompted bundling of a rewritten create_mesh.py overwrote the user's
      Blender 5.1.2-compatible script with a legacy Blender 4.x fcurves call, causing
      an immediate crash.
    architectural_law: >
      swm_compiler.py and create_mesh.py are strictly read-only ground-truth judges.
      All SWM iterations emit ONLY declarative data artifacts (pass_sensorfusion.json,
      scene_graph.json, and Benchmark Record documentation).

# ------------------------------------------------------------------------------
# 2. V4.5.3 ARCHITECTURAL UPGRADES FOR THE MULTI-STAGE ROADMAP (OPTION C READY)
# ------------------------------------------------------------------------------
v4_5_3_upgrades:
  car_style_adjustable_headrest:
    joint_name: "Backrest_To_Headrest_Slide"
    joint_type: "prismatic (axis_of_motion: [0.0, 0.0, 1.0])"
    components:
      - "Scene.Chair_Headrest.Headrest_Guide_Rod_R (cylinder d=20mm, L=160mm at X=-0.09m)"
      - "Scene.Chair_Headrest.Headrest_Guide_Rod_L (cylinder d=20mm, L=160mm at X=+0.09m)"
      - "Scene.Chair_Headrest.Headrest_Cushion (cube 260x65x180mm at Z_backrest=0.740m, Y_front=-0.055m)"
    roadmap_purpose: >
      Provides an explicit prismatic degree of freedom so the Robotic MTA in Option C
      can adjust the headrest height along the twin guide rods to match the patient's
      seated cranial height, alongside adjusting the Göpel leg support struts.

  two_part_torso_kinematic_split:
    joints:
      - "Pelvis_To_Human_Abdomen (revolute hinge at [0.0, +0.02, 0.85])"
      - "Abdomen_To_Human_Thorax (revolute waist joint at Z_abdomen = 0.225m)"
    components:
      - "Scene.Human_Abdomen.Lumbar_Joint_Sphere (148x136x136mm)"
      - "Scene.Human_Abdomen.Abdomen_Core (225x125x165mm, Z=0.030..0.195m)"
      - "Scene.Human_Thorax.Waist_Joint_Sphere (172x118x110mm at Z=0.225m)"
      - "Scene.Human_Thorax.Waist_Spine_Tendon (d=36mm, L=90mm)"
      - "Scene.Human_Thorax.Thorax_Core (288x145x285mm, Z=0.255..0.540m)"
