
---
license: cc-by-4.0
task_categories:
- robotics
- computer-vision
tags:
- motion-capture
- humanoid
- unitree-g1
- kazakh-dance
- kara-zhorga

pretty_name: Kara Zhorga Unitree G1 Dataset
size_categories:
- 1K<n<10K
---

# 🕺 Kara Zhorga (Қара Жорға) · Unitree G1 Humanoid Motion Dataset

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Framework: PyTorch](https://img.shields.io/badge/Framework-PyTorch-orange.svg)](https://pytorch.org/)
[![Hardware: Unitree G1](https://img.shields.io/badge/Hardware-Unitree_G1-blue.svg)](https://www.unitree.com/g1)
[![Hugging Face Dataset](https://img.shields.io/badge/%F0%9F%A4%97-Hugging%20Face%20Dataset-yellow)](https://huggingface.co/datasets)

An open-source, high-fidelity motion capture and joint-trajectory dataset capturing the traditional Kazakh dance **"Kara Zhorga" (Қара Жорға)**, optimized explicitly for the **Unitree G1** humanoid robot.

This dataset bridges cultural heritage preservation with advanced robotics, providing clean, multi-modal structural sequences to train humanoid motor skills, reinforcement learning (RL) balancing locomotion policies, and generative motion synthesis.

---

## 🌟 Key Features

- **Multi-Performer Capture**: High-density motion configurations performed by professional dancers (**Kara, Dauren, and Dastan**).
- **Unitree G1 Optimized**: Pre-targeted and retargeted joint angle spaces compatible with the Unitree G1's 23-43 degrees of freedom (DoF) structural kinematics.
- **Rich Modalities**: Includes raw 3D joint positions, optimized orientation quaternions, angular velocities, and structural JSON annotations.
- **Interactive Visualization Panel**: Embedded local web viewer (`index.html`) using a responsive glassmorphic UI to preview motion segments, filter sub-sequences, and cross-reference validation statuses.

---

## 🗺️ Pipeline & Data Architecture


```

[ Raw MoCap Data ] ➔ [ Kinematic Retargeting ] ➔ [ Joint Trajectory Optimization ] ➔ [ G1 Simulation Deployment ]

```

1. **Mocap Data**: 3D keypoint extractions tracking complex chest, shoulder, hip, and ankle articulation sequences unique to Kara Zhorga.
2. **Retargeting Pipeline**: Scaling spatial constraints from human proportions down to the Unitree G1 structural mesh body lengths.
3. **Trajectory Smoothing**: Fine-tuning acceleration and torque limits to fit within the physical motor specifications of the real G1 humanoid.

---

## 📂 Repository & Dataset Structure

```hl
.
├── index.html              # Interactive visualization dashboard (Web UI)
├── README.md               # Project documentation & metadata
├── data/
│   ├── metadata.json       # Central registry maps tracking durations, performers, and states
│   ├── raw_mocap/          # Source positional coordinates (.csv / .bvh)
│   └── g1_trajectories/    # Targeted robot joint-space control tables (.json / .npz)
│       ├── kara/
│       ├── dauren/
│       └── dastan/
└── scripts/
    ├── retarget_g1.py      # URDF kinematic retargeting script
    └── validate_limits.py  # Check joint limits and sudden torque spikes

```

### Motion File Schema (`g1_trajectories/*.json`)

Each optimized trajectory slice outputs structural joint configuration blocks matching the motor indexing arrangement:

```json
{
  "sequence_id": "KARA_ZHORGA_001",
  "performer": "Kara",
  "frame_rate": 30,
  "total_frames": 450,
  "joint_order": ["left_hip_pitch", "left_hip_roll", "left_knee", "right_hip_pitch", "..."],
  "frames": [
    {
      "timestamp": 0.00,
      "joint_positions": [0.124, -0.045, 0.389, -0.112, 0.0],
      "root_linear_velocity": [0.01, 0.00, 0.00],
      "stable_ground_contact": [1, 1]
    }
  ]
}

```

---

## 🚀 Getting Started

### 1. Interactive Preview

To browse and cross-reference dataset splits interactively, simply run the visualization dashboard locally:

```bash
# Open via browser
open index.html

```

The interface allows you to view clip lengths, keep track of completion validations, and verify exact paths inside the `/data` layout tree.

### 2. Loading into Python (Hugging Face Datasets)

If using the repository directly within training pipelines via the Hugging Face Hub library:

```python
from datasets import load_dataset

# Load the motion trajectory data streams
dataset = load_dataset("your-username-or-org/kara-zhorga-unitree-g1")

# Preview a single sequence slice
sample_sequence = dataset['train'][0]
print(f"Sequence: {sample_sequence['sequence_id']} by {sample_sequence['performer']}")

```

---

## 🛠️ Hardware Requirements & Motor Tuning

When executing these joint paths inside simulation engines (e.g., Isaac Gym, Mujoco) or streaming to a live physical Unitree G1 unit, ensure your controller loops match these limits:

| Joint Group | Max Angular Velocity | Controller Mode | Recommended P Gain |
| --- | --- | --- | --- |
| **Waist / Pitch** | 20.0 rad/s | Position / PD | 80.0 |
| **Knee (Left/Right)** | 30.0 rad/s | Position / PD | 120.0 |
| **Shoulder Complex** | 15.0 rad/s | Position / PD | 40.0 |

---

## 📜 Citation

If you use this dataset, visualization tool, or target code trajectories in a publication, project, or exhibition, please cite it using the BibTeX format below:

```bibtex
@dataset{kara_zhorga_g1_2026,
  author       = {Kara Zhorga Dataset Project Contributors},
  title        = {Kara Zhorga (Қара Жорға) Traditional Dance Trajectory Dataset for the Unitree G1 Humanoid},
  year         = {2026},
  publisher    = {GitHub / Hugging Face},
  howpublished = {\url{[https://github.com/whiteraay/kara-zhorga](https://github.com/whiteraay/kara-zhorga)}}
}

```

---

## ⚖️ License

This project, dashboard code, and the underlying kinematic trajectories are licensed under a **Creative Commons Attribution 4.0 International License (CC BY 4.0)**. You are free to share, copy, and adapt the material for any purpose (even commercially) provided appropriate attribution is given.

```

```
