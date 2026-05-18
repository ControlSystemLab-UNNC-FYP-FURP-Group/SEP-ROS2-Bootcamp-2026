# Course Outline - ROS 2 Carter Bootcamp

> Language: English  
> Duration: Week 0 preparation + 8 formal teaching weeks  
> Platform: Linux2Go, Ubuntu 22.04, ROS 2 Humble, Carter differential-drive robot

---

## 1. Course Positioning

This bootcamp is designed as a practical robotics systems course. The goal is not only to teach ROS 2 commands, but also to help students understand how a real mobile robot system is built, debugged, integrated, and evaluated.

The course follows a progressive learning path:

```text
Linux and ROS 2 basics
  ↓
ROS 2 packages, nodes, topics, services, actions, launch, and rosbag
  ↓
Robot modeling with URDF / Xacro and TF
  ↓
Carter differential-drive base bringup
  ↓
LiDAR, IMU, odometry, and state estimation
  ↓
Indoor SLAM
  ↓
Indoor Nav2 navigation and obstacle avoidance
  ↓
Outdoor waypoint navigation with GPS / RTK when available
  ↓
Final integrated robot demo
```

---

## 2. Expected Background

Students are expected to have:

- basic programming ability in Python or C++;
- basic mathematics and physics background;
- willingness to work with Linux terminal tools;
- willingness to debug hardware and software problems in teams.

No prior ROS 2 experience is required.

---

## 3. Final Learning Outcomes

By the end of the course, students should be able to:

1. explain the role of ROS 2 in a mobile robot system;
2. create, build, and run ROS 2 packages;
3. use `ros2` CLI tools to inspect nodes, topics, services, actions, parameters, and bags;
4. model a differential-drive robot with URDF / Xacro;
5. debug a TF tree and explain the relationship between `map`, `odom`, `base_link`, `laser_link`, and `imu_link`;
6. command the Carter base using `/cmd_vel`;
7. convert wheel encoder data into odometry;
8. connect and validate LiDAR and IMU data;
9. use `robot_localization` to fuse wheel odometry and IMU data;
10. build indoor maps using SLAM Toolbox;
11. configure Nav2 for indoor localization and navigation;
12. tune basic costmap, planner, and controller parameters;
13. perform low-speed outdoor waypoint navigation;
14. collect evidence with logs, screenshots, maps, and rosbag files;
15. present an engineering report that includes system design, test results, failures, and future improvements.

---

## 4. Course Rhythm

Each formal week uses the same structure.

| Day | Session | Purpose |
|---|---|---|
| Monday afternoon | Lecture + guided lab | Introduce new concepts and start the weekly task |
| Wednesday afternoon | Clinic | Diagnose issues and unblock teams |
| Friday afternoon | Q&A + checkpoint | Verify progress and prepare for next week |

The course emphasizes weekly checkpoints because mobile robot systems are cumulative. If the base driver, odometry, or TF tree is broken, later SLAM and navigation labs will also fail.

---

## 5. Week 0 - Preparation Before Linux2Go Distribution

### Time

From now to **2026-06-08**.

### Main Goal

Students should get familiar with Ubuntu, VMware, Linux terminal tools, and ROS 2 Humble before receiving the official Linux2Go system.

### Tasks

- Install VMware Workstation Pro, VMware Fusion, or another supported virtualization tool.
- Create an Ubuntu 22.04 virtual machine.
- Practice basic Linux commands.
- Try installing ROS 2 Humble.
- Run basic ROS 2 demo nodes.
- Read beginner ROS 2 tutorials.

### Suggested Linux Commands

```bash
pwd
ls
cd
mkdir
touch
cp
mv
rm
cat
less
grep
find
chmod
sudo
apt update
apt install
```

### Suggested ROS 2 Tests

```bash
source /opt/ros/humble/setup.bash
ros2 --help
ros2 doctor
ros2 run demo_nodes_cpp talker
ros2 run demo_nodes_py listener
```

### Checkpoint

Before Week 1, students should understand:

- what a virtual machine is;
- what Ubuntu is;
- how to open and use a terminal;
- how to install packages with `apt`;
- what ROS 2 Humble is;
- what nodes and topics roughly mean;
- how to copy logs and ask a reproducible technical question.

### References

- [Ubuntu Desktop Download](https://ubuntu.com/download/desktop)
- [Ubuntu 22.04 Releases](https://releases.ubuntu.com/22.04/)
- [ROS 2 Humble Installation](https://docs.ros.org/en/humble/Installation.html)
- [ROS 2 Humble Tutorials](https://docs.ros.org/en/humble/Tutorials.html)

---

## 6. Week 1 - ROS 2 Basics and Tooling

### Learning Objectives

Students will learn the fundamental ROS 2 computing model and development workflow.

### Topics

- ROS 2 workspace and package structure;
- nodes and topics;
- messages;
- services and actions;
- parameters;
- launch files;
- `ros2` CLI tools;
- `rqt_graph`;
- `rosbag2`;
- basic package creation and build process.

### Monday Lecture

- What ROS 2 is and why robotics systems use middleware.
- How nodes communicate.
- How to create a workspace.
- How to build with `colcon`.
- How to write a simple publisher and subscriber.

### Wednesday Clinic

Diagnostic checklist:

```text
1. Linux2Go boots successfully.
2. ROS 2 Humble is available.
3. colcon build works.
4. Students know how to source setup.bash.
5. Talker/listener demos work.
6. Students can inspect topics with ros2 topic list and ros2 topic echo.
```

### Friday Checkpoint

Each student submits:

```text
1. One publisher
2. One subscriber
3. One launch file
4. One short rosbag recording
5. A README explaining how to run the code
```

### Deliverables

- `week1_ros2_basics` package;
- commands used during testing;
- screenshots or terminal logs;
- short reflection on one debugging problem.

### References

- [ROS 2 Tutorials](https://docs.ros.org/en/humble/Tutorials.html)
- [Understanding nodes](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Nodes/Understanding-ROS2-Nodes.html)
- [Understanding topics](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Topics/Understanding-ROS2-Topics.html)
- [Using colcon to build packages](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Colcon-Tutorial.html)

---

## 7. Week 2 - Carter Modeling, URDF, TF, and Differential Drive Kinematics

### Learning Objectives

Students will understand the physical and coordinate-frame representation of Carter.

### Topics

- Differential-drive kinematics;
- `/cmd_vel` interpretation;
- `linear.x` and `angular.z`;
- URDF and Xacro;
- links and joints;
- visual, collision, and inertial elements;
- `robot_state_publisher`;
- static and dynamic TF;
- RViz2 robot model visualization.

### Monday Lecture

- How a differential-drive robot moves.
- How robot geometry becomes a URDF model.
- Why TF is critical for SLAM and navigation.
- Recommended Carter frame tree.

### Wednesday Clinic

Diagnostic checklist:

```text
1. Carter model appears in RViz2.
2. Wheel links are placed correctly.
3. laser_link and imu_link are attached to the correct parent frame.
4. TF tree has no missing branches.
5. Frame names are consistent.
```

### Friday Checkpoint

Each team submits:

```text
1. carter_description package
2. display.launch.py
3. RViz2 screenshot
4. TF tree screenshot
5. One-page explanation of differential-drive kinematics
```

### Deliverables

- `carter_description`;
- `urdf/carter.urdf.xacro`;
- `launch/display.launch.py`;
- TF tree image;
- model inspection notes.

### References

- [URDF Tutorials](https://docs.ros.org/en/humble/Tutorials/Intermediate/URDF/URDF-Main.html)
- [Using Xacro](https://docs.ros.org/en/humble/Tutorials/Intermediate/URDF/Using-Xacro-to-Clean-Up-a-URDF-File.html)
- [tf2 Tutorials](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Tf2-Main.html)
- [RViz User Guide](https://docs.ros.org/en/humble/Tutorials/Intermediate/RViz/RViz-User-Guide/RViz-User-Guide.html)

---

## 8. Week 3 - Carter Base Driver and ros2_control

### Learning Objectives

Students will connect high-level velocity commands to real base motion.

### Topics

- `/cmd_vel` to wheel velocity conversion;
- encoder ticks to wheel speed;
- wheel odometry;
- `ros2_control`;
- `diff_drive_controller`;
- command timeout;
- velocity and acceleration limits;
- emergency stop and manual takeover.

### Monday Lecture

- Carter base hardware interface.
- Differential-drive control pipeline.
- Odometry computation from encoders.
- Why safety checks are part of the software architecture.

### Wednesday Clinic

Hardware diagnostic checklist:

```text
1. Left and right wheel directions are correct.
2. Encoder signs are correct.
3. /cmd_vel controls the base.
4. /odom is continuous.
5. odom -> base_link TF is stable.
6. Speed limits are active.
7. Emergency stop works.
```

### Friday Checkpoint

Each team demonstrates:

```text
1. 1-meter straight-line motion
2. 90-degree in-place rotation
3. Square trajectory
4. /odom publication
5. /tf publication
6. Base parameter table
```

### Deliverables

- Carter bringup launch file;
- base driver configuration;
- wheel radius, wheel separation, encoder resolution table;
- short test report.

### References

- [ros2_control Documentation](https://control.ros.org/)
- [diff_drive_controller](https://control.ros.org/master/doc/ros2_controllers/diff_drive_controller/doc/userdoc.html)
- [ROS 2 Launch Tutorials](https://docs.ros.org/en/humble/Tutorials/Intermediate/Launch/Launch-Main.html)

---

## 9. Week 4 - LiDAR, IMU, rosbag, and State Estimation

### Learning Objectives

Students will validate robot sensors and fuse odometry with IMU data.

### Topics

- `sensor_msgs/LaserScan`;
- `sensor_msgs/Imu`;
- frame_id and timestamp consistency;
- rosbag recording and playback;
- odometry drift;
- EKF basics;
- `robot_localization`;
- raw odometry versus filtered odometry.

### Monday Lecture

- What LiDAR and IMU data look like in ROS 2.
- Common sensor-frame mistakes.
- How to record reproducible experiments.
- How EKF-based state estimation helps navigation.

### Wednesday Clinic

Diagnostic checklist:

```text
1. /scan is stable.
2. /imu is stable.
3. /scan and /imu frame_id values are correct.
4. /odom does not jump unexpectedly.
5. /odometry/filtered is published.
6. rosbag playback reproduces the issue.
```

### Friday Checkpoint

Each team submits:

```text
1. One Carter motion rosbag
2. ekf.yaml
3. Raw odom versus filtered odom comparison
4. Sensor TF checklist
5. One sensor debugging record
```

### Deliverables

- `carter_sensors` launch file;
- `carter_localization` configuration;
- rosbag file or link;
- plots or screenshots comparing odometry outputs.

### References

- [sensor_msgs Package](https://docs.ros.org/en/humble/p/sensor_msgs/)
- [robot_localization Documentation](https://docs.ros.org/en/melodic/api/robot_localization/html/index.html)
- [Nav2: Setting Up Odometry](https://docs.nav2.org/setup_guides/odom/setup_robot_localization.html)
- [Recording and Playing Back Data](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Recording-And-Playing-Back-Data/Recording-And-Playing-Back-Data.html)

---

## 10. Week 5 - Indoor SLAM Mapping

### Learning Objectives

Students will create a usable indoor 2D map with the Carter robot.

### Topics

- 2D LiDAR SLAM;
- scan matching;
- pose graph;
- loop closure;
- SLAM Toolbox;
- map saving and loading;
- map quality evaluation;
- good mapping route design.

### Monday Lecture

- Why SLAM needs odometry, LiDAR, and TF.
- How to collect a good mapping run.
- How to identify map distortion and duplicated walls.
- How to save and reuse maps.

### Wednesday Clinic

Mapping diagnostic checklist:

```text
1. Map does not contain severe duplicated walls.
2. Major walls are closed.
3. LiDAR height is appropriate.
4. base_link to laser_link transform is correct.
5. Odometry drift is not excessive.
6. Dynamic obstacle interference is understood.
```

### Friday Checkpoint

Each team submits:

```text
1. Indoor map.yaml and map image
2. Mapping rosbag
3. mapping.launch.py
4. Map quality analysis
5. One failed mapping case explanation
```

### Deliverables

- indoor map files;
- SLAM launch file;
- mapping test notes;
- one failure analysis.

### References

- [SLAM Toolbox GitHub](https://github.com/SteveMacenski/slam_toolbox)
- [SLAM Toolbox on ROS Index](https://index.ros.org/r/slam_toolbox/)
- [Nav2 Tutorials](https://docs.nav2.org/tutorials/index.html)

---

## 11. Week 6 - Indoor Navigation and Obstacle Avoidance with Nav2

### Learning Objectives

Students will configure Nav2 for indoor navigation.

### Topics

- Nav2 architecture;
- map server;
- localization;
- planner server;
- controller server;
- behavior tree navigator;
- global and local costmaps;
- obstacle layer;
- inflation layer;
- recovery behaviors;
- RViz2 goal setting.

### Monday Lecture

- How Nav2 turns a goal pose into robot motion.
- How global planning and local control differ.
- Why costmap tuning matters.
- How to debug navigation failures.

### Wednesday Clinic

Nav2 diagnostic checklist:

```text
1. AMCL or localization is stable.
2. Costmaps show obstacles correctly.
3. Global plan is generated.
4. Local controller outputs /cmd_vel.
5. Robot does not oscillate excessively.
6. Recovery behavior is understood.
```

### Friday Checkpoint

Each team demonstrates:

```text
1. Single-goal navigation
2. Multi-goal navigation
3. Dynamic obstacle avoidance
4. At least one failure analysis
5. Explanation of carter_nav2_params.yaml
```

### Deliverables

- `carter_navigation.launch.py`;
- `carter_nav2_params.yaml`;
- navigation demo video;
- tuning notes.

### References

- [Nav2 Documentation](https://docs.nav2.org/)
- [Nav2 Setup Guides](https://docs.nav2.org/setup_guides/index.html)
- [Nav2 Configuration Guide](https://docs.nav2.org/configuration/index.html)
- [Nav2 Tutorials](https://docs.nav2.org/tutorials/index.html)

---

## 12. Week 7 - Outdoor Waypoint Navigation and GPS / RTK Extension

### Learning Objectives

Students will understand the difference between indoor navigation and outdoor waypoint navigation.

### Topics

- Outdoor navigation challenges;
- GPS and RTK basics;
- `sensor_msgs/NavSatFix`;
- `navsat_transform_node`;
- local EKF and global EKF;
- waypoint following;
- outdoor safety;
- manual takeover.

### Monday Lecture

- Why GPS is not a direct replacement for indoor localization.
- How IMU, wheel odometry, and GPS can be fused.
- How to define and test outdoor waypoints.
- How to design a safe outdoor experiment.

### Wednesday Clinic

Outdoor diagnostic checklist:

```text
1. GPS fix is available.
2. IMU heading is reasonable.
3. Coordinate conversion is reasonable.
4. Waypoints are placed correctly.
5. Robot runs at safe low speed.
6. Human takeover is available.
```

### Friday Checkpoint

Each team demonstrates or submits:

```text
1. 3-5 outdoor waypoint following demo
2. Low-speed obstacle avoidance or human takeover procedure
3. Outdoor failure analysis
4. GPS / IMU / odom data log
```

If GPS / RTK is unreliable, the task can be downgraded to:

```text
1. Short-distance outdoor waypoint navigation with wheel odometry and IMU
2. GPS data recording
3. Offline GPS / EKF analysis
```

### Deliverables

- outdoor waypoint file;
- GPS / EKF configuration;
- outdoor safety checklist;
- rosbag or log file;
- short outdoor experiment report.

### References

- [Nav2 GPS Waypoint Following Tutorial](https://docs.nav2.org/tutorials/docs/navigation2_with_gps.html)
- [robot_localization Documentation](https://docs.ros.org/en/melodic/api/robot_localization/html/index.html)
- [sensor_msgs/NavSatFix](https://docs.ros.org/en/humble/p/sensor_msgs/msg/NavSatFix.html)

---

## 13. Week 8 - Capstone Integration and Final Demo

### Learning Objectives

Students will integrate the full Carter mobile robot navigation system.

### Topics

- system integration;
- launch file organization;
- parameter management;
- experiment reproducibility;
- final demo design;
- engineering report writing;
- failure analysis and future work.

### Monday Lecture

- How to structure the final system.
- How to write reproducible run instructions.
- How to explain architecture and tradeoffs.
- How to prepare for a robot demo.

### Wednesday Clinic

Final diagnostic checklist:

```text
1. Bringup launch works.
2. TF tree is correct.
3. Sensor topics are available.
4. Localization is stable.
5. Nav2 parameters are loaded correctly.
6. Maps and bags are organized.
7. Demo route is safe.
```

### Friday Final Demo

Each team presents for 10-15 minutes:

```text
1. System architecture
2. Carter bringup
3. Indoor SLAM / localization / navigation
4. Dynamic obstacle avoidance
5. Outdoor waypoint navigation or extension task
6. Failure cases and improvement plan
```

### Final Deliverables

- Git repository;
- launch files;
- parameter files;
- maps;
- rosbag files or links;
- demo video;
- final report;
- presentation slides;
- README with reproducible instructions.

---

## 14. Suggested Grading

| Component | Weight |
|---|---:|
| Weekly labs and assignments | 30% |
| Carter hardware bringup | 15% |
| Indoor SLAM and Nav2 navigation | 20% |
| Outdoor waypoint / GPS experiment | 15% |
| Final demo and report | 20% |

---

## 15. Engineering Mindset

The course values evidence-based debugging. A good answer is not only “it works,” but:

```text
1. What command did you run?
2. What topic or transform proves it works?
3. What data did you record?
4. What failure did you observe?
5. What change improved the result?
6. What remains uncertain?
```
