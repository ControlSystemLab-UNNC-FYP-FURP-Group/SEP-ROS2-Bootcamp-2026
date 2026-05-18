# 🧠 How to Ask Questions in This Bootcamp  
# 🧠 如何在本课程中高效提问

> Inspired by [How To Ask Questions The Smart Way / 提问的智慧](https://github.com/ryanhanwu/How-To-Ask-Questions-The-Smart-Way/tree/main).  
> We borrow the engineering spirit: **be precise, be reproducible, be respectful of other people's debugging time**.

---

## 1. 🌱 The mindset

In robotics, a question is rarely just a sentence.  
A good question is a small debugging package.

When you ask for help, your goal is not only to get an answer. Your goal is to help the instructor, TA, or teammate quickly reconstruct your problem.

A strong question says:

> I know what I was trying to do.  
> I know what I ran.  
> I know what happened.  
> I have evidence.  
> I tried something.  
> I am ready to learn from the answer.

---

## 2. ✅ Before asking

Please try these first:

- Search this repository.
- Read the current week's slides and lab notes.
- Search the official ROS 2 / Nav2 documentation.
- Re-run the command and copy the full error.
- Check whether you sourced the workspace.
- Check whether the robot is powered and connected.
- Check whether the relevant node, topic, or TF frame exists.
- Ask one teammate to reproduce the problem.

Useful commands:

```bash
pwd
ls
echo $ROS_DISTRO
echo $ROS_DOMAIN_ID
source /opt/ros/humble/setup.bash
source install/setup.bash
colcon build --symlink-install
ros2 doctor
ros2 node list
ros2 topic list
ros2 topic hz /scan
ros2 topic echo /odom --once
ros2 run tf2_tools view_frames
```

---

## 3. 🧩 Minimum question template

Use this template in GitHub Issues, clinic notes, or chat.

````md
## Goal
What were you trying to achieve?

## Environment
- Machine: Linux2Go / VMware / other
- OS: Ubuntu 22.04
- ROS 2: Humble
- Robot: Carter / simulation / rosbag replay
- Branch or commit:

## Command
```bash
paste the exact command here
```

## Expected behavior
What did you expect to happen?

## Actual behavior
What happened instead?

## Evidence
- Error log:
- Screenshot:
- rosbag:
- TF tree:
- `ros2 node list`:
- `ros2 topic list`:
- Relevant YAML / launch file:

## What I already tried
1.
2.
3.

## My current guess
Optional, but useful.
````

---

## 4. 🤖 Robot debugging checklist

For Carter-related problems, bring this information to Wednesday clinic.

### Motion problem

```bash
ros2 topic info /cmd_vel
ros2 topic echo /cmd_vel
ros2 topic echo /joint_states --once
ros2 topic echo /odom --once
```

Questions to answer:

- Does Carter receive `/cmd_vel`?
- Do the wheels move in the correct direction?
- Does `/odom` change when the robot moves?
- Does the robot stop when `/cmd_vel` stops?
- Is the emergency stop released?
- Is the speed limit too low or too high?

### TF problem

```bash
ros2 run tf2_tools view_frames
ros2 run tf2_ros tf2_echo odom base_link
ros2 run tf2_ros tf2_echo base_link laser_link
```

Questions to answer:

- Is there exactly one continuous chain from `odom` to `base_link`?
- Is `laser_link` connected to `base_link`?
- Is the transform direction correct?
- Are there duplicate TF publishers?

### LiDAR problem

```bash
ros2 topic info /scan
ros2 topic hz /scan
ros2 topic echo /scan --once
```

Questions to answer:

- Is `/scan` published?
- Is the frame ID correct?
- Is the scan rate stable?
- Does RViz show the scan in the expected place?

### Nav2 problem

```bash
ros2 node list | grep nav
ros2 topic list | grep costmap
ros2 topic echo /cmd_vel --once
```

Questions to answer:

- Is localization active?
- Does RViz show the map?
- Does the global costmap show obstacles?
- Does the local costmap show nearby obstacles?
- Does Nav2 produce a path?
- Does the controller output `/cmd_vel`?

---

## 5. 🟢 Good vs. weak questions

### Weak

> Nav2 does not work. What should I do?

### Strong

> I am trying to run Week 6 single-goal navigation on Carter.  
> The map loads correctly and AMCL particles appear in RViz, but after I send a goal, the global path appears and `/cmd_vel` stays empty.  
> I ran `ros2 topic echo /cmd_vel --once` and got no output.  
> `controller_server` is active according to lifecycle manager.  
> I attached my `nav2_params.yaml`, TF tree screenshot, and a short rosbag.  
> My guess is that the local costmap or controller plugin is not configured correctly.

Why this is better:

- It states the goal.
- It describes expected vs. actual behavior.
- It gives evidence.
- It narrows the problem.
- It shows what has already been checked.

---

## 6. 🧪 Evidence you should collect often

| Evidence | Why it helps |
|---|---|
| Screenshot of RViz | Shows map, TF, laser scan, costmap, robot pose |
| `rqt_graph` screenshot | Shows node-topic connections |
| TF tree PDF / screenshot | Reveals broken or duplicated frames |
| rosbag | Lets others replay your issue |
| YAML parameters | Most navigation bugs are parameter bugs |
| Launch command | Reproduces the exact system |
| Terminal logs | Shows warnings and errors before failure |

---

## 7. 中文版：提问的核心原则

在机器人课程里，提问不是“我不会，帮我看看”。  
一个好的问题应该让助教或同学能够快速复现你的场景。

提问前，请尽量准备：

```text
1. 我想实现什么？
2. 我运行了什么命令？
3. 我期待发生什么？
4. 实际发生了什么？
5. 有没有完整报错？
6. 我已经尝试过什么？
7. 我能否提供截图、TF tree、rosbag、参数文件或 launch 文件？
```

一个好的问题通常长这样：

> 我在做 Week 5 的 Carter 室内建图。  
> `/scan` 在 RViz 里可以看到，但是地图出现明显重影。  
> 我检查了 `/odom`，发现原地转弯时 yaw 变化方向似乎反了。  
> 我已经附上 TF tree、`ros2 topic echo /odom --once`、建图截图和 20 秒 rosbag。  
> 我怀疑是左右轮编码器方向或 wheel separation 参数有问题。

这类问题比“建图失败怎么办”更容易得到有效帮助。

---

## 8. Clinic rule of thumb

For Wednesday clinic, do not come only with a feeling.  
Come with a reproducible case.

Minimum clinic package:

```text
command + error log + screenshot + topic list + TF tree
```

For hardware / navigation issues, add:

```text
rosbag + parameter YAML + launch file
```

---

## 9. Be kind to your future self

Good notes are not just for instructors.  
They are for you three weeks later, when a problem returns and you cannot remember how you fixed it.

After solving a problem, write down:

```text
Problem:
Root cause:
Fix:
How to verify:
How to avoid next time:
```

That habit is one of the fastest ways to become a better robotics engineer.
