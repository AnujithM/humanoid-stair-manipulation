# Motion Retargeting to Humanoids (Unitree G1, Booster T1)

Motion retargeting converts human motion (MoCap, SMPL/AMASS, or video-based pose)
into robot joint targets that respect the humanoid’s kinematics, limits, and contacts.

This page focuses on **retargeting** (human → humanoid).  
For **stair-climbing RL** and **whole-body policies**, see `locomotion/` and `stairs/`.

---

## What “Retargeting” Usually Means

A practical retargeting pipeline often looks like:

1. **Human motion source**
   - MoCap skeleton (BVH), SMPL/AMASS, or video-based 3D pose
2. **Kinematic retargeting (IK / optimization)**
   - Map key bodies (torso, feet, hands), align rest poses, scale
3. **Contact + feasibility cleanup**
   - Reduce foot skating, avoid self-collisions, fix ground penetration
4. **Use the retargeted motion**
   - As tracking references for control, or as training data for RL/IL

---

## Core Retargeting Methods (G1 / T1-relevant)

### GMR / “Retargeting Matters” (2025) — strong general baseline
- General Motion Retargeting (GMR): key-body mapping → rest-pose alignment → non-uniform scaling → staged IK solve
- Focus: reduce common artifacts (foot sliding, infeasible poses) before training tracking policies
- Used with **Unitree G1** and evaluated with motion tracking pipelines

**Links**
- Paper: https://arxiv.org/abs/2510.02252
- Code: https://github.com/YanjieZe/GMR

---

### OmniRetarget (2025) — interaction-preserving (object + terrain)
- Builds an **interaction mesh** over (human body + object + terrain points)
- Optimizes robot motion to preserve geometry/contact while enforcing:
  - collision avoidance
  - joint/velocity limits
  - anti-foot-skating constraints
- Explicitly supports **Unitree G1/H1** and **Booster T1**

**Links**
- Paper: https://arxiv.org/abs/2509.26633
- Project: https://omniretarget.github.io/

---

### TWIST / TWIST2 (2025) — teleop-driven real-time retargeting
- Frames teleoperation as: **real-time retargeting → whole-body tracking policy**
- TWIST2 describes a detailed G1 retargeting tweak:
  - lower body uses position+rotation constraints
  - upper body uses rotation-only (more robust to noisy global pose)

**Links**
- TWIST: https://arxiv.org/abs/2505.02833
- TWIST2: https://arxiv.org/abs/2511.02832

---

### SPIDER (2025) — physics-informed retargeting at scale (dexterous + whole-body)
- Trajectory-optimization style retargeting that enforces **dynamic feasibility** and contact consistency
- Evaluated on humanoid whole-body control with **Unitree G1** and **Booster T1**
- Useful when you want **robot-ready datasets** from noisy human kinematic demos

**Links**
- Paper: https://arxiv.org/abs/2511.09484
- Project: https://jc-bao.github.io/spider-project/

---

## Vision-to-Retargeting (video → humanoid motion)

### VideoMimic (CoRL 2025) — monocular video → world motion → retarget
- Real-to-sim pipeline reconstructs 3D human motion from single-camera video and **retargets to humanoids**
- Often used to produce reference motions for imitation/control training

Repo: https://github.com/hongsukchoi/VideoMimic

---

### World-Coordinate Retargeting via SAM 3D Body (Dec 2025) — stable world trajectories → G1
- A lightweight vision pipeline that produces world-coordinate motion from monocular video
- Then retargets to **Unitree G1** using a kinematics-aware staged IK pipeline

Paper: https://arxiv.org/abs/2512.21573

---

## Learning-based Retargeting (emerging)

### MoReFlow (2025) — unsupervised flow matching for retargeting
- Learns motion-domain mappings without paired datasets (character/robot specific tokenizers)
- Includes **Booster T1** as one of the target embodiments in experiments

Paper: https://arxiv.org/abs/2509.25600

---

## Practical Notes for Unitree G1 / Booster T1

### Common pain points
- **Morphology mismatch** (limb proportions, hip offsets)
- **Foot contact quality** (anti-slip / anti-skate matters a lot)
- **Upper-body coupling** (arm motion affects balance)
- **Hand mismatch** (Dex3 often behaves closer to a gripper in teleop pipelines)

### What to record in your repo for each method
For each paper/tool, capture:
- Input format (BVH / SMPL / video pose)
- Robot(s) supported (G1, T1, H1…)
- Contact handling (foot skate, collisions, ground constraints)
- Output (joint angles, root trajectory, task-space targets)
- Whether it’s real-time or offline

---

## Open Problems (good research directions)
- Retargeting **stairs + manipulation** simultaneously (hands + feet contacts at once)
- Vision-conditioned retargeting (scene-aware foot placement & grasp points)
- Retargeting that preserves **force/torque feasibility**, not just kinematics