# Humanoid Stair Climbing

This section covers methods enabling humanoids to ascend and descend stairs,
with or without support, under varying terrain and perception uncertainty.

---

## Categories

### 1. Model-Based Stair Climbing
- ZMP / centroidal dynamics
- Preview control
- Contact planning

### 2. Learning-Based Approaches
- Reinforcement Learning
- Imitation Learning
- AMP-style motion priors

### 3. Hybrid Methods
- Model-based planning + learned residuals
- Physics-informed RL

---

## Key Papers

### Learning-based Stair Climbing
- **"Learning Agile and Dynamic Motor Skills for Legged Robots"**  
  *Hwangbo et al., Science 2019*  
  → RL-based locomotion, sim-to-real

- **"AMP: Adversarial Motion Priors"**  
  *Peng et al., SIGGRAPH 2021*  
  → Human motion prior for natural walking

---

### Whole-Body Control on Stairs
- **"Whole-Body Locomotion and Manipulation"**  
  → Coupled hand-foot contact planning

---

## Open Problems

- Generalizing stair geometry
- Vision-based foothold selection
- Carrying objects while climbing
- Robustness under perception noise
