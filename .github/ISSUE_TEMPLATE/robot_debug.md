---
name: "🤖 Robot Debug"
about: Report a Carter / ROS 2 robot debugging issue
title: "[Robot Debug] "
labels: robot-debug
assignees: ""
---

## What is failing?

- [ ] Carter does not move
- [ ] `/cmd_vel` issue
- [ ] `/odom` issue
- [ ] TF issue
- [ ] LiDAR `/scan` issue
- [ ] IMU issue
- [ ] SLAM issue
- [ ] Nav2 issue
- [ ] Outdoor / GPS issue
- [ ] Other:

## Goal

What were you trying to make the robot do?

## System

- Week:
- Robot:
- Machine:
- Branch / commit:
- Launch file:
- Parameter file:

## Commands

```bash
paste commands here
```

## Evidence checklist

Please include as much as possible.

```bash
ros2 node list
ros2 topic list
ros2 topic hz /scan
ros2 topic echo /odom --once
ros2 run tf2_tools view_frames
```

Attach screenshots / rosbag / logs if possible.

## Expected behavior

## Actual behavior

## What I already checked

- [ ] Power / battery
- [ ] E-stop
- [ ] Network / connection
- [ ] Workspace sourced
- [ ] Correct ROS_DOMAIN_ID
- [ ] Correct launch file
- [ ] TF tree generated
- [ ] Relevant topics published

## Notes

Any extra context.
