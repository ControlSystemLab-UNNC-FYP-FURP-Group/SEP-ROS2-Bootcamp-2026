# 🤖 ROS 2 Carter Bootcamp

> An 8-week hands-on ROS 2 summer bootcamp for sophomore and junior engineering/science students.  
> Students will start from basic Linux and ROS 2 usage and gradually build a complete mobile robot navigation stack on our Carter differential-drive robot platform.

---

## 🔗 Quick Links

- [Course Outline - English](docs/course_outline_en.md)
- [课程大纲 - 中文](docs/course_outline_zh.md)
- [Control System Lab @ UNNC](https://control-system-lab-at-unnc.github.io/homepage-v2/)

---

## 🏫 Organizer / Lab

This bootcamp is organized by the [Control System Lab @ UNNC](https://control-system-lab-at-unnc.github.io/homepage-v2/).

---

## 🎯 Project Goal

This repository is the public course hub for the **ROS 2 Carter Bootcamp**. It is designed to help students, teaching assistants, and instructors share:

- course announcements;
- weekly learning objectives;
- lecture slides, which will be updated before each Monday lecture;
- lecture notes and lab instructions;
- Carter robot bringup resources;
- debugging checklists;
- assignment requirements;
- final project expectations;
- useful ROS 2, Linux, navigation, SLAM, and robotics references.

The bootcamp is not intended to be a purely theoretical ROS 2 lecture series. The practical goal is to help students build a working mobile robot system step by step, from ROS 2 basics to indoor and outdoor autonomous navigation.

---

## 👥 Target Students

This course is designed for undergraduate students with engineering or science backgrounds, especially sophomore and junior students who may have:

- basic programming experience;
- limited or no prior ROS experience;
- limited Linux command-line experience;
- interest in robotics, autonomous systems, controls, mechatronics, or AI systems.

No prior ROS 2 experience is required.

---

## 🧭 Practical Learning Objectives

By the end of the bootcamp, each student team should be able to:

1. use Linux, Git, terminal tools, and ROS 2 command-line tools confidently;
2. create and build ROS 2 packages in a workspace;
3. understand ROS 2 nodes, topics, services, actions, parameters, launch files, and rosbag;
4. model the Carter robot using URDF / Xacro and inspect the TF tree;
5. control a differential-drive robot using `/cmd_vel`;
6. publish and debug `/odom`, `/tf`, `/joint_states`, `/scan`, and `/imu`;
7. use wheel odometry and IMU data for state estimation;
8. generate an indoor 2D map using SLAM Toolbox;
9. configure Nav2 for indoor localization, planning, control, and obstacle avoidance;
10. perform basic outdoor waypoint navigation with GPS / RTK when available;
11. document experiments with commands, screenshots, logs, rosbag files, maps, and parameter files;
12. explain failure cases and propose engineering improvements.

---

## 📦 Available Course Resources

This repository may include or link to:

```text
README.md                         Project homepage
docs/course_outline_en.md          Full English course outline
docs/course_outline_zh.md          Full Chinese course outline
slides/                            Weekly lecture slides
labs/                              Weekly lab instructions and starter code
assignments/                       Weekly assignments and grading rubrics
checklists/                        Debugging and safety checklists
carter_examples/                   Carter robot reference packages
resources/                         Linux, Git, ROS 2, Nav2, and troubleshooting notes
```

Recommended initial folder structure:

```text
ros2-carter-bootcamp/
├── README.md
├── docs/
│   ├── course_outline_en.md
│   └── course_outline_zh.md
├── slides/
├── labs/
├── assignments/
├── checklists/
├── carter_examples/
└── resources/
```

---

## 🗓️ Course Timeline

The course consists of one preparation period and eight formal teaching weeks.

| Phase | Time | Focus |
|---|---|---|
| Week 0 | Now to 2026-06-08 | Self-paced preparation: VMware, Ubuntu, Linux basics, ROS 2 Humble exploration |
| 2026-06-08 | Linux2Go distribution | Students receive the pre-configured course system |
| Weeks 1-8 | Formal bootcamp | Weekly lectures, clinics, Q&A, checkpoints, and final project |

---

## 🔁 Weekly Teaching Rhythm

Each week follows a fixed rhythm.

| Day | Activity | Purpose |
|---|---|---|
| Monday afternoon | Lecture + guided lab | Introduce the main topic and start the weekly lab |
| Wednesday afternoon | Clinic | Diagnose engineering problems and unblock teams |
| Friday afternoon | Q&A + checkpoint | Review common issues and verify weekly progress |


> 📌 **Slides update policy:** weekly slides will be updated before the Monday lecture of that week.

### 🧑‍🏫 Monday: Lecture + Guided Lab

Typical structure:

```text
00:00 - 00:20  Weekly review and common issues
00:20 - 01:10  Core concepts
01:10 - 01:40  Instructor live demo
01:40 - 02:40  Guided student lab
02:40 - 03:00  Weekly task briefing
```

### 🩺 Wednesday: Engineering Clinic

The clinic is for technical diagnosis rather than general discussion. Students should bring concrete evidence:

```text
1. Commands they ran
2. Error logs
3. ros2 node list
4. ros2 topic list
5. ros2 topic hz output
6. rqt_graph or TF tree screenshots
7. rosbag files when needed
8. What they already tried
```

### ✅ Friday: Q&A + Checkpoint

Friday is used to verify whether each team is ready to move on to the next stage.

Each team should be able to answer:

```text
1. What did we complete this week?
2. What evidence proves that it works?
3. What is still broken?
4. What is the next debugging step?
```

---

## 🚀 Week 0 Preparation

Week 0 runs from now until **2026-06-08**.

Students are encouraged to explore the following before the official Linux2Go system is distributed:

- install VMware;
- create an Ubuntu 22.04 virtual machine;
- practice Linux terminal commands;
- attempt to install ROS 2 Humble;
- run basic ROS 2 demos;
- read the beginner ROS 2 tutorials.

Important note:

> Week 0 is for exploration. The official teaching environment will be distributed on Linux2Go on 2026-06-08. It is acceptable if your personal virtual machine setup is incomplete, but you should document the problems you encounter.

Recommended references:

- [Ubuntu Desktop Download](https://ubuntu.com/download/desktop)
- [Ubuntu 22.04 Releases](https://releases.ubuntu.com/22.04/)
- [Ubuntu Desktop Installation Guide](https://documentation.ubuntu.com/desktop/en/latest/how-to/install-ubuntu-desktop/)
- [ROS 2 Humble Documentation](https://docs.ros.org/en/humble/index.html)
- [ROS 2 Humble Installation](https://docs.ros.org/en/humble/Installation.html)
- [ROS 2 Humble Tutorials](https://docs.ros.org/en/humble/Tutorials.html)
- [VMware Workstation / Fusion Download Information](https://knowledge.broadcom.com/external/article/368667/download-and-license-vmware-desktop-hype.html)

---

## 🙋 How to Ask Questions

Good engineering questions include reproducible evidence.

Please use this format when asking questions in clinic, GitHub Issues, or discussion channels:

```markdown
## What I am trying to do

Example: I am trying to launch the Carter robot model in RViz2 and inspect the TF tree.

## What I ran

```bash
ros2 launch carter_description display.launch.py
```

## What I expected

Example: RViz2 should show the robot model with base_link, wheels, laser_link, and imu_link.

## What actually happened

Example: RViz2 opens, but the robot model is not visible.

## Logs or screenshots

```text
Paste the error message here.
```

## What I already tried

1. Rebuilt the workspace.
2. Sourced install/setup.bash.
3. Checked ros2 topic list.
4. Checked whether robot_description exists.
```

---

## 🛠️ Carter Robot Interface Convention

The Carter platform used in this course is assumed to follow the interface below.

### 📥 Input

```text
/cmd_vel    geometry_msgs/msg/Twist
```

### 📤 Core Outputs

```text
/odom              nav_msgs/msg/Odometry
/tf                tf2_msgs/msg/TFMessage
/joint_states      sensor_msgs/msg/JointState
/scan              sensor_msgs/msg/LaserScan
/imu               sensor_msgs/msg/Imu
```

### ➕ Optional Outputs

```text
/battery_state     sensor_msgs/msg/BatteryState
/diagnostics       diagnostic_msgs/msg/DiagnosticArray
/fix               sensor_msgs/msg/NavSatFix
```

### 🧩 Recommended TF Tree

```text
map
└── odom
    └── base_footprint
        └── base_link
            ├── left_wheel_link
            ├── right_wheel_link
            ├── laser_link
            ├── imu_link
            └── gps_link
```

---

## ⚠️ Safety Rules

Carter is a real mobile robot. All hardware labs must follow these rules:

1. A teaching assistant or instructor must be present during first-time hardware testing.
2. The first motor test must be performed with the robot lifted or speed-limited.
3. Emergency stop must be tested before autonomous operation.
4. A `/cmd_vel` timeout or watchdog must be enabled.
5. Indoor testing must use conservative speed limits.
6. Outdoor testing must include human takeover.
7. Do not run autonomous mode near crowds.
8. Do not test high-speed motion in unknown environments.
9. Record failures and near-misses as engineering data, not as personal mistakes.

---

## 📚 Main Technical References

### 🏫 Lab

- [Control System Lab @ UNNC](https://control-system-lab-at-unnc.github.io/homepage-v2/)

### 🤖 ROS 2

- [ROS 2 Humble Documentation](https://docs.ros.org/en/humble/index.html)
- [ROS 2 Humble Tutorials](https://docs.ros.org/en/humble/Tutorials.html)
- [ROS 2 Humble Installation](https://docs.ros.org/en/humble/Installation.html)
- [ROS Index](https://index.ros.org/)

### 🧱 Modeling, TF, and Visualization

- [URDF Tutorials](https://docs.ros.org/en/humble/Tutorials/Intermediate/URDF/URDF-Main.html)
- [tf2 Tutorials](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Tf2-Main.html)
- [RViz User Guide](https://docs.ros.org/en/humble/Tutorials/Intermediate/RViz/RViz-User-Guide/RViz-User-Guide.html)

### 🧭 Control, SLAM, Localization, and Navigation

- [ros2_control](https://control.ros.org/)
- [diff_drive_controller](https://control.ros.org/master/doc/ros2_controllers/diff_drive_controller/doc/userdoc.html)
- [robot_localization](https://docs.ros.org/en/melodic/api/robot_localization/html/index.html)
- [SLAM Toolbox](https://github.com/SteveMacenski/slam_toolbox)
- [Nav2 Documentation](https://docs.nav2.org/)
- [Nav2 Tutorials](https://docs.nav2.org/tutorials/index.html)
- [Nav2 GPS Waypoint Following](https://docs.nav2.org/tutorials/docs/navigation2_with_gps.html)

---

## 📄 License

Course materials in this repository are for educational use.  
Please follow the licenses of all third-party software, documents, and referenced resources.
