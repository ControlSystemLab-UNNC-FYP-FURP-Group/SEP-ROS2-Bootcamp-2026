# 课程大纲 - ROS 2 Carter Bootcamp

> 语言：中文
> 周期：Week 0 预备期 + 8 周正式课程
> 平台：Linux2Go、Ubuntu 22.04、ROS 2 Humble、Carter 差速底盘

---

## 1. 课程定位

本课程是一门偏工程实践的移动机器人系统课程。课程目标不是只教 ROS 2 命令，而是帮助学生理解一个真实移动机器人系统如何被搭建、调试、集成和评估。

课程采用逐步递进路线：

```text
Linux 与 ROS 2 基础
  ↓
ROS 2 package、node、topic、service、action、launch、rosbag
  ↓
URDF / Xacro 建模与 TF 坐标树
  ↓
Carter 差速底盘 bringup
  ↓
LiDAR、IMU、里程计与状态估计
  ↓
室内 SLAM 建图
  ↓
Nav2 室内导航与避障
  ↓
GPS / RTK 条件下的室外 waypoint 导航
  ↓
最终系统集成演示
```

---

## 2. 学生背景要求

本课程适合具有工科或理科背景的学生。建议学生具备：

- 基础 Python 或 C++ 编程能力；
- 基础数学和物理背景；
- 愿意使用 Linux 终端；
- 愿意在小组中调试软硬件系统。

课程不要求学生提前掌握 ROS 2。

---

## 3. 最终学习目标

课程结束后，学生应该能够：

1. 解释 ROS 2 在移动机器人系统中的作用；
2. 创建、构建和运行 ROS 2 package；
3. 使用 `ros2` 命令行工具检查 node、topic、service、action、parameter 和 bag；
4. 使用 URDF / Xacro 建模差速机器人；
5. 调试 TF tree，并解释 `map`、`odom`、`base_link`、`laser_link`、`imu_link` 的关系；
6. 使用 `/cmd_vel` 控制 Carter 底盘；
7. 将轮速编码器数据转换为里程计；
8. 接入并验证 LiDAR 和 IMU 数据；
9. 使用 `robot_localization` 融合轮速里程计与 IMU；
10. 使用 SLAM Toolbox 完成室内建图；
11. 配置 Nav2 完成室内定位和导航；
12. 调整基础 costmap、planner 和 controller 参数；
13. 完成低速室外 waypoint 导航；
14. 使用日志、截图、地图、rosbag 和参数文件记录实验；
15. 提交包含系统设计、测试结果、失败案例和改进方向的工程报告。

---

## 4. 每周课程节奏

正式课程每周采用固定节奏。

| 时间     | 内容                   | 目的                               |
| -------- | ---------------------- | ---------------------------------- |
| 周一下午 | 主课 + guided lab      | 引入本周知识点，启动本周实验       |
| 周三下午 | clinic 工程问诊        | 集中诊断问题，帮助各组 unblock     |
| 周五下午 | 答疑 + checkpoint 验收 | 检查进度，判断是否可以进入下一阶段 |

移动机器人系统具有很强的累积性。如果底盘驱动、里程计或 TF 坐标树有问题，后续 SLAM 和导航都会受到影响。因此本课程强调每周 checkpoint。

---

## 5. Week 0 - Linux2Go 发放前预备期

### 时间

从现在到 **2026-06-08**。

### 主要目标

学生在拿到正式 Linux2Go 系统前，先熟悉 Ubuntu、VMware、Linux 终端和 ROS 2 Humble。

### 任务

- 安装 VMware Workstation Pro、VMware Fusion 或其他可用虚拟机软件；
- 创建 Ubuntu 22.04 虚拟机；
- 练习基础 Linux 命令；
- 尝试安装 ROS 2 Humble；
- 运行基础 ROS 2 demo；
- 阅读 ROS 2 beginner tutorials。

### 建议掌握的 Linux 命令

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

### 建议运行的 ROS 2 测试

```bash
source /opt/ros/humble/setup.bash
ros2 --help
ros2 doctor
ros2 run demo_nodes_cpp talker
ros2 run demo_nodes_py listener
```

### Checkpoint

Week 1 开始前，学生应至少了解：

- 什么是虚拟机；
- Ubuntu 是什么；
- 如何打开并使用 terminal；
- 如何通过 `apt` 安装软件；
- ROS 2 Humble 是什么；
- node 和 topic 的基本含义；
- 如何复制日志并提出可复现的技术问题。

### 参考资料

- [Ubuntu Desktop Download](https://ubuntu.com/download/desktop)
- [Ubuntu 22.04 Releases](https://releases.ubuntu.com/22.04/)
- [ROS 2 Humble Installation](https://docs.ros.org/en/humble/Installation.html)
- [ROS 2 Humble Tutorials](https://docs.ros.org/en/humble/Tutorials.html)

---

## 6. Week 1 - ROS 2 基础与工具链

### 学习目标

学生将学习 ROS 2 的基础计算模型和开发流程。

### 主题

- ROS 2 workspace 和 package 结构；
- node 与 topic；
- message；
- service 与 action；
- parameter；
- launch 文件；
- `ros2` 命令行工具；
- `rqt_graph`；
- `rosbag2`；
- package 创建与构建流程。

### 周一主课

- ROS 2 是什么，为什么机器人系统需要中间件；
- node 如何通信；
- 如何创建 workspace；
- 如何使用 `colcon` 构建；
- 如何编写简单 publisher 和 subscriber。

### 周三 clinic

检查重点：

```text
1. Linux2Go 是否可以正常启动
2. ROS 2 Humble 是否可用
3. colcon build 是否成功
4. 是否知道如何 source setup.bash
5. talker / listener demo 是否可运行
6. 是否能用 ros2 topic list 和 ros2 topic echo 检查 topic
```

### 周五 checkpoint

每位同学提交：

```text
1. 一个 publisher
2. 一个 subscriber
3. 一个 launch 文件
4. 一段短 rosbag
5. 一个说明如何运行代码的 README
```

### 交付物

- `week1_ros2_basics` package；
- 测试命令；
- 截图或终端日志；
- 一段调试问题复盘。

### 参考资料

- [ROS 2 Tutorials](https://docs.ros.org/en/humble/Tutorials.html)
- [Understanding nodes](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Nodes/Understanding-ROS2-Nodes.html)
- [Understanding topics](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Topics/Understanding-ROS2-Topics.html)
- [Using colcon to build packages](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Colcon-Tutorial.html)

---

## 7. Week 2 - Carter 建模、URDF、TF 与差速运动学

### 学习目标

学生将理解 Carter 的物理结构和坐标系表示方法。

### 主题

- 差速底盘运动学；
- `/cmd_vel` 含义；
- `linear.x` 与 `angular.z`；
- URDF 和 Xacro；
- link 与 joint；
- visual、collision、inertial；
- `robot_state_publisher`；
- 静态 TF 与动态 TF；
- RViz2 机器人模型可视化。

### 周一主课

- 差速机器人如何运动；
- 如何将机器人几何结构表示为 URDF；
- 为什么 TF 对 SLAM 和导航至关重要；
- Carter 推荐坐标树。

### 周三 clinic

检查重点：

```text
1. Carter 模型是否能在 RViz2 中显示
2. 轮子 link 位置是否正确
3. laser_link 和 imu_link 是否挂在正确父坐标系下
4. TF tree 是否有断裂
5. frame 命名是否一致
```

### 周五 checkpoint

每组提交：

```text
1. carter_description package
2. display.launch.py
3. RViz2 截图
4. TF tree 截图
5. 一页差速底盘运动学说明
```

### 交付物

- `carter_description`；
- `urdf/carter.urdf.xacro`；
- `launch/display.launch.py`；
- TF tree 图片；
- 模型检查记录。

### 参考资料

- [URDF Tutorials](https://docs.ros.org/en/humble/Tutorials/Intermediate/URDF/URDF-Main.html)
- [Using Xacro](https://docs.ros.org/en/humble/Tutorials/Intermediate/URDF/Using-Xacro-to-Clean-Up-a-URDF-File.html)
- [tf2 Tutorials](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Tf2-Main.html)
- [RViz User Guide](https://docs.ros.org/en/humble/Tutorials/Intermediate/RViz/RViz-User-Guide/RViz-User-Guide.html)

---

## 8. Week 3 - Carter 底盘驱动与 ros2_control

### 学习目标

学生将把高层速度指令连接到底盘真实运动。

### 主题

- `/cmd_vel` 到左右轮速度转换；
- 编码器 tick 到轮速；
- 轮速里程计；
- `ros2_control`；
- `diff_drive_controller`；
- command timeout；
- 速度和加速度限制；
- 急停和人工接管。

### 周一主课

- Carter 底盘硬件接口；
- 差速控制链路；
- 如何从编码器计算里程计；
- 为什么安全机制是软件架构的一部分。

### 周三 clinic

硬件检查重点：

```text
1. 左右轮方向是否正确
2. 编码器正负号是否正确
3. /cmd_vel 是否能控制底盘
4. /odom 是否连续
5. odom -> base_link TF 是否稳定
6. 限速是否生效
7. 急停是否可用
```

### 周五 checkpoint

每组演示：

```text
1. 直线 1 米
2. 原地旋转 90 度
3. 方形轨迹
4. 发布 /odom
5. 发布 /tf
6. 底盘参数表
```

### 交付物

- Carter bringup launch 文件；
- 底盘驱动配置；
- 轮半径、轮距、编码器分辨率表；
- 简短测试报告。

### 参考资料

- [ros2_control Documentation](https://control.ros.org/)
- [diff_drive_controller](https://control.ros.org/master/doc/ros2_controllers/diff_drive_controller/doc/userdoc.html)
- [ROS 2 Launch Tutorials](https://docs.ros.org/en/humble/Tutorials/Intermediate/Launch/Launch-Main.html)

---

## 9. Week 4 - LiDAR、IMU、rosbag 与状态估计

### 学习目标

学生将验证机器人传感器，并融合里程计与 IMU 数据。

### 主题

- `sensor_msgs/LaserScan`；
- `sensor_msgs/Imu`；
- frame_id 与 timestamp 一致性；
- rosbag 记录和回放；
- 里程计漂移；
- EKF 基础；
- `robot_localization`；
- raw odometry 与 filtered odometry 对比。

### 周一主课

- ROS 2 中的 LiDAR 和 IMU 数据长什么样；
- 常见传感器坐标系错误；
- 如何记录可复现实验；
- 基于 EKF 的状态估计如何帮助导航。

### 周三 clinic

检查重点：

```text
1. /scan 是否稳定
2. /imu 是否稳定
3. /scan 和 /imu 的 frame_id 是否正确
4. /odom 是否异常跳变
5. /odometry/filtered 是否发布
6. rosbag 回放是否能复现问题
```

### 周五 checkpoint

每组提交：

```text
1. 一段 Carter 运动 rosbag
2. ekf.yaml
3. raw odom 与 filtered odom 对比
4. 传感器 TF 检查表
5. 一次传感器调试记录
```

### 交付物

- `carter_sensors` launch 文件；
- `carter_localization` 配置；
- rosbag 文件或链接；
- odometry 对比图或截图。

### 参考资料

- [sensor_msgs Package](https://docs.ros.org/en/humble/p/sensor_msgs/)
- [robot_localization Documentation](https://docs.ros.org/en/melodic/api/robot_localization/html/index.html)
- [Nav2: Setting Up Odometry](https://docs.nav2.org/setup_guides/odom/setup_robot_localization.html)
- [Recording and Playing Back Data](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Recording-And-Playing-Back-Data/Recording-And-Playing-Back-Data.html)

---

## 10. Week 5 - 室内 SLAM 建图

### 学习目标

学生将使用 Carter 生成可用的室内 2D 地图。

### 主题

- 2D LiDAR SLAM；
- scan matching；
- pose graph；
- loop closure；
- SLAM Toolbox；
- 地图保存与加载；
- 地图质量评估；
- 好的建图路线设计。

### 周一主课

- 为什么 SLAM 需要 odometry、LiDAR 和 TF；
- 如何采集一段好的建图数据；
- 如何识别地图变形和墙体重影；
- 如何保存和复用地图。

### 周三 clinic

建图检查重点：

```text
1. 地图是否有严重重影
2. 主要墙体是否闭合
3. LiDAR 高度是否合理
4. base_link 到 laser_link 的 transform 是否正确
5. odometry 漂移是否过大
6. 是否理解动态障碍物干扰
```

### 周五 checkpoint

每组提交：

```text
1. 室内 map.yaml 和地图图片
2. 建图 rosbag
3. mapping.launch.py
4. 地图质量分析
5. 一次失败建图案例说明
```

### 交付物

- 室内地图文件；
- SLAM launch 文件；
- 建图测试记录；
- 一个失败案例分析。

### 参考资料

- [SLAM Toolbox GitHub](https://github.com/SteveMacenski/slam_toolbox)
- [SLAM Toolbox on ROS Index](https://index.ros.org/r/slam_toolbox/)
- [Nav2 Tutorials](https://docs.nav2.org/tutorials/index.html)

---

## 11. Week 6 - Nav2 室内导航与避障

### 学习目标

学生将配置 Nav2 完成室内导航。

### 主题

- Nav2 架构；
- map server；
- localization；
- planner server；
- controller server；
- behavior tree navigator；
- global costmap 与 local costmap；
- obstacle layer；
- inflation layer；
- recovery behaviors；
- RViz2 目标点设置。

### 周一主课

- Nav2 如何把目标点转换成机器人运动；
- global planning 和 local control 的区别；
- 为什么 costmap 调参很重要；
- 如何调试导航失败。

### 周三 clinic

Nav2 检查重点：

```text
1. AMCL 或 localization 是否稳定
2. costmap 是否正确显示障碍物
3. global plan 是否生成
4. local controller 是否输出 /cmd_vel
5. 机器人是否严重振荡
6. 是否理解 recovery behavior
```

### 周五 checkpoint

每组演示：

```text
1. 单点导航
2. 多点导航
3. 动态障碍物避障
4. 至少一次失败案例分析
5. carter_nav2_params.yaml 参数说明
```

### 交付物

- `carter_navigation.launch.py`；
- `carter_nav2_params.yaml`；
- 导航演示视频；
- 参数调优记录。

### 参考资料

- [Nav2 Documentation](https://docs.nav2.org/)
- [Nav2 Setup Guides](https://docs.nav2.org/setup_guides/index.html)
- [Nav2 Configuration Guide](https://docs.nav2.org/configuration/index.html)
- [Nav2 Tutorials](https://docs.nav2.org/tutorials/index.html)

---

## 12. Week 7 - 室外 waypoint 导航与 GPS / RTK 扩展

### 学习目标

学生将理解室内导航与室外 waypoint 导航的差异。

### 主题

- 室外导航挑战；
- GPS 与 RTK 基础；
- `sensor_msgs/NavSatFix`；
- `navsat_transform_node`；
- local EKF 与 global EKF；
- waypoint following；
- 室外安全；
- 人工接管。

### 周一主课

- 为什么 GPS 不是室内定位的直接替代品；
- 如何融合 IMU、轮速里程计和 GPS；
- 如何定义和测试室外 waypoint；
- 如何设计安全的室外实验。

### 周三 clinic

室外检查重点：

```text
1. GPS 是否有 fix
2. IMU 航向是否合理
3. 坐标转换是否合理
4. waypoint 是否落在正确位置
5. 机器人是否低速安全运行
6. 是否具备人工接管
```

### 周五 checkpoint

每组演示或提交：

```text
1. 3-5 个室外 waypoint 跟随演示
2. 低速避障或人工接管流程
3. 室外失败案例分析
4. GPS / IMU / odom 数据日志
```

如果 GPS / RTK 条件不可靠，本周任务可降级为：

```text
1. 使用轮速里程计和 IMU 完成短距离室外 waypoint
2. 记录 GPS 数据
3. 离线 GPS / EKF 分析
```

### 交付物

- 室外 waypoint 文件；
- GPS / EKF 配置；
- 室外安全 checklist；
- rosbag 或日志；
- 简短室外实验报告。

### 参考资料

- [Nav2 GPS Waypoint Following Tutorial](https://docs.nav2.org/tutorials/docs/navigation2_with_gps.html)
- [robot_localization Documentation](https://docs.ros.org/en/melodic/api/robot_localization/html/index.html)
- [sensor_msgs/NavSatFix](https://docs.ros.org/en/humble/p/sensor_msgs/msg/NavSatFix.html)

---

## 13. Week 8 - Capstone 集成与 Final Demo

### 学习目标

学生将集成完整 Carter 移动机器人导航系统。

### 主题

- 系统集成；
- launch 文件组织；
- 参数管理；
- 实验可复现性；
- final demo 设计；
- 工程报告写作；
- 失败分析与未来改进。

### 周一主课

- 如何组织最终系统；
- 如何写可复现运行说明；
- 如何解释系统架构和工程权衡；
- 如何准备机器人演示。

### 周三 clinic

最后检查重点：

```text
1. bringup launch 是否可用
2. TF tree 是否正确
3. 传感器 topic 是否可用
4. localization 是否稳定
5. Nav2 参数是否正确加载
6. 地图和 bag 是否整理好
7. demo 路线是否安全
```

### 周五 Final Demo

每组展示 10-15 分钟：

```text
1. 系统架构
2. Carter bringup
3. 室内 SLAM / localization / navigation
4. 动态障碍物避障
5. 室外 waypoint 导航或扩展任务
6. 失败案例与改进计划
```

### 最终交付物

- Git 仓库；
- launch 文件；
- 参数文件；
- 地图；
- rosbag 文件或链接；
- 演示视频；
- final report；
- presentation slides；
- 包含可复现运行说明的 README。

---

## 14. 建议评分方式

| 项目                     | 占比 |
| ------------------------ | ---: |
| 每周实验与作业           |  30% |
| Carter 真机 bringup      |  15% |
| 室内 SLAM 与 Nav2 导航   |  20% |
| 室外 waypoint / GPS 实验 |  15% |
| Final demo 与报告        |  20% |

---

## 15. 工程思维要求

本课程重视基于证据的调试。一个好的回答不只是“它能跑”，而是：

```text
1. 你运行了什么命令？
2. 哪个 topic 或 transform 证明它正常？
3. 你记录了什么数据？
4. 你观察到了什么失败？
5. 哪个修改改善了结果？
6. 还有什么不确定？
```
