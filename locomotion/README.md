# Humanoid Stair Climbing

This section covers methods that enable humanoid robots to ascend and descend
stairs under **realistic constraints** like contact-rich interaction, and simultaneous manipulation (e.g., using rails or
carrying objects).

The focus is on **whole-body humanoid systems** where stair climbing is not an
isolated locomotion problem, but tightly coupled with **perception,
retargeting, and manipulation**.

---

## Categories

### 1. Model-Based Stair Climbing
Classical approaches that rely on explicit dynamics and contact modeling.

- ZMP / centroidal dynamics
- Preview control
- Contact and foothold planning
- Whole-body control with hand–foot contacts

**Limitations:**  
Struggles with perception noise, unseen stair geometries, and complex
loco-manipulation (e.g., holding rails or objects).

---

### 2. Learning-Based Approaches
Data-driven methods that learn policies for stair traversal from demonstrations
or interaction.

- Reinforcement Learning (RL)
- Imitation Learning (IL)
- AMP-style motion priors
- Vision-conditioned policies
---

### 3. Hybrid and Physics-Informed Methods
Methods that combine structured models with learning to improve robustness and
real-world transfer.

- Model-based planning + learned residuals
- Physics-informed RL
- Motion priors with physical feasibility constraints
- Retargeting-aware policy learning

---

## Key Papers

### Learning-Based and Imitation-Based Stair Climbing

#### **AMP: Adversarial Motion Priors**  
*Peng et al., SIGGRAPH 2021*  
- Introduces adversarial motion priors from human motion capture.
- Enables natural and stable humanoid walking, forming the backbone for
many later stair-climbing and loco-manipulation systems.
- Commonly used as a **pretraining prior** before task-specific adaptation.

---

#### **VideoMimic: Visual Imitation Enables Contextual Humanoid Control**
- Learns whole-body humanoid control from **monocular videos** of humans.
- Reconstructs both **human motion and scene geometry**, then retargets the
motion to humanoids.
- Demonstrates contextual skills including **stair ascent/descent** and
environment-aware locomotion.
- Highlights the importance of **vision + retargeting + RL** as a unified
pipeline.

**Key insight:**  
Stair climbing is treated as a *contextual behavior*, not a predefined task.

---

### Whole-Body Interaction and Loco-Manipulation on Stairs

#### **PhysHSI: Physically Realizable Humanoid–Scene Interaction**
- Trains humanoids to interact with complex environments using **physics-aware
RL**.
- Supports tasks such as carrying objects, standing up, and interacting with
scene geometry.
- Uses **AMP-based locomotion priors**, perception-driven object localization,
and real-world deployment on Unitree G1.
- Highly relevant for **stair climbing with object carrying or support rails**.

---

## Open Problems

- Generalization to unseen stair geometries and materials
- Vision-based foothold and handhold selection
- Stair climbing while:
  - carrying objects
  - using handrails
- Retargeting across different humanoid morphologies (e.g., G1 vs Booster T1)

---

