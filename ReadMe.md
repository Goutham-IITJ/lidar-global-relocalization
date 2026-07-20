# LiDAR Global Relocalization
### Robust Kidnapped Robot Recovery using LiDAR Scan Descriptor Matching

> Developed and extensively extended during my Robotics Internship at **ugo Inc., Tokyo, Japan**

![ROS2](https://img.shields.io/badge/ROS2-Humble-blue)
![Gazebo](https://img.shields.io/badge/Gazebo-Classic-orange)
![Python](https://img.shields.io/badge/Python-3.10-green)
![Platform](https://img.shields.io/badge/Platform-Ubuntu%2022.04-lightgrey)

---

# Overview

This repository implements a **LiDAR-based global relocalization system** capable of recovering a robot from an unknown position after a kidnapped robot event.

The work is based on the original scan descriptor localization framework by **Saad Waqar**, and was significantly extended during my internship to support a realistic indoor service robot workflow.

Major modifications include

- Migration to AWS Small House World
- New occupancy maps
- Updated localization configuration
- Improved launch pipeline
- Parameter tuning
- Extensive kidnapped robot evaluation
- Documentation and visualization
- Experimental analysis

---

# Problem Statement

Localization systems relying only on odometry or local scan matching fail when the robot is physically moved without updating odometry (Kidnapped Robot Problem).

The objective of this project is to

- detect the correct global location using only LiDAR observations,
- estimate the global pose,
- recover localization without resetting odometry,
- continue normal navigation.

---

# Localization Pipeline

```
                Laser Scan
                     │
                     ▼
          Scan Descriptor Generation
                     │
                     ▼
         Descriptor Database Matching
                     │
                     ▼
          Candidate Global Pose
                     │
                     ▼
             ICP Scan Alignment
                     │
                     ▼
          Estimated Global Pose
                     │
                     ▼
      Localization Recovery (map→odom)
```

---

# Repository Structure

```
lidar-global-relocalization/

├── config/
│   └── config.yaml
│
├── global_localizer/
│   ├── descriptor_database.py
│   ├── icp_registration.py
│   ├── localization.py
│   └── ...
│
├── maps/
│   ├── aws_house_map.pgm
│   └── aws_house_map.png
│
├── media/
│   ├── screenshots/
│   ├── output1.gif
│   ├── output2.gif
│   └── output3.gif
│
├── resource/
├── test/
│
├── package.xml
├── setup.py
└── README.md
```

---

# Internship Contributions

Compared to the original repository, the following major modifications were introduced.

## Simulation Environment

- Migrated to AWS Small House World
- Generated new occupancy grid maps
- Updated map server configuration
- Created new testing routes

---

## Localization

- Updated localization parameters
- Improved descriptor search configuration
- Tuned ICP registration
- Improved recovery robustness

---

## Experimental Evaluation

- Performed repeated kidnapped robot experiments
- Validated localization recovery
- Verified odometry consistency
- Recorded recovery behaviour
- Analysed localization stability

---

## Documentation

- Complete repository restructuring
- Experimental media
- Updated launch workflow
- Hardware deployment guide
- Result documentation

---

# Running the Package

## 1. Clone

```bash
git clone https://github.com/Goutham-IITJ/lidar-global-relocalization.git

cd lidar-global-relocalization
```

---

## 2. Build

```bash
colcon build --symlink-install

source install/setup.bash
```

---

## 3. Launch Gazebo

```bash
ros2 launch gazebo_ros gazebo.launch.py
```

---

## 4. Start Localization

```bash
ros2 run global_localizer localization_node
```

---

# Kidnapped Robot Evaluation Procedure

The evaluation follows the standard kidnapped robot protocol.

1. Localize the robot.
2. Teleoperate normally.
3. Physically move the robot to a different location.
4. Keep odometry unchanged.
5. Allow descriptor matching.
6. Observe map→odom correction.
7. Verify localization recovery.

---

# Experimental Results

## Generated Map

<p align="center">
<img src="media/screenshots/generated_map.png" width="700">
</p>

---

## Localization

<p align="center">
<img src="media/screenshots/localization.png" width="700">
</p>

---

## Kidnapped Robot Recovery

<p align="center">
<img src="media/output1.gif" width="700">
</p>

---

# Example Recovery

During kidnapped robot experiments

- Robot odometry remained locally continuous.
- Descriptor matching produced candidate global poses.
- ICP refined the pose estimate.
- The **map→odom transform** was updated.
- Localization recovered without resetting odometry.

This confirms true global relocalization instead of odometry teleportation.

---

# Evaluation Metrics

Experiments evaluate

- Recovery Success Rate
- Recovery Time
- Descriptor Matching Robustness
- ICP Convergence
- Localization Stability
- Transform Consistency
- Kidnapped Robot Recovery Accuracy

---

# Applications

This work is applicable to

- Indoor Service Robots
- Warehouse Robots
- Hospital Robots
- Delivery Robots
- Autonomous Mobile Robots (AMRs)

---

# Future Work

- Multi-session descriptor database
- Faster nearest-neighbour search
- RGB + LiDAR hybrid localization
- Semantic place recognition
- Large-scale environment support

---

# Related Work

During the internship, a second localization pipeline based on

- Monocular RGB Camera
- 3D LiDAR
- RTAB-Map

was also developed and evaluated.

Repository:

**rtabmap-rgb-3dlidar-relocalization**

---

# Acknowledgements

This work extends the original LiDAR global localization framework developed by **Saad Waqar**.

The repository was significantly modified and experimentally evaluated during my Robotics Internship at **ugo Inc., Tokyo, Japan** to support realistic kidnapped robot recovery experiments in the AWS Small House environment.

---

# Author

**Goutham A. S.**

B.Tech Electrical Engineering

Indian Institute of Technology Jodhpur

Robotics | SLAM | Localization | Autonomous Navigation

GitHub: https://github.com/Goutham-IITJ
