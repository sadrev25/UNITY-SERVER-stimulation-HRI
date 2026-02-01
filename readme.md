# Unity Underwater Simulation Server

This repository contains a Unity-based simulation server developed
for underwater robotics experimentation and academic evaluation.
The system provides a simulated underwater environment with ROS2
connectivity, enabling interaction with a BlueROV-style vehicle.

The project focuses on simulation-side logic rather than visualization
output, making it suitable for backend testing and control integration.

---

## Core Functionality

### Simulation Setup
- Underwater physics modeling for robotic vehicles
- Buoyancy and drag effects applied to the ROV
- Collision handling with environment objects
- Stable motion behavior suitable for teleoperation

### Robotic Vehicle
- BlueROV-type underwater vehicle model
- Integrated virtual camera sensor
- Vehicle dynamics driven by ROS2 velocity commands

### Environment
- Pool-based underwater test environment (UJI scenario)
- Static underwater objects including a target / black-box element
- Collision-aware interaction with environment geometry

---

## ROS2 Communication

The simulation server communicates with ROS2 using a TCP-based bridge.

### Active Interfaces
- **Velocity Input**
  - Subscribes to `/bluerov1/cmd_vel` for motion control
- **Camera Output**
  - Publishes simulated camera images
- **State Feedback**
  - Publishes odometry (position and orientation)
- **Collision Events**
  - Detects and reports collisions during runtime

---

## System Requirements

### ROS2 Dependencies

The following ROS2 packages are required:

- **ROS TCP Endpoint**
  - Enables data exchange between Unity and ROS2
  - Repository: https://github.com/Unity-Technologies/ROS-TCP-Endpoint

- **Keyboard Teleoperation**
  - Used for manual control of the simulated vehicle
  - Repository: https://github.com/ros2/teleop_twist_keyboard

---

## Running the Simulation Server

### Step 1: Start ROS TCP Bridge

Launch the ROS TCP server to allow Unity communication:

```bash
ros2 run ros_tcp_endpoint default_server_endpoint --ros-args \
-p ROS_IP:=127.0.0.1 \
-p ROS_TCP_PORT:=10000
Notes:

Use 127.0.0.1 for local execution

Ensure the port matches the configuration inside Unity

Step 2: Start Unity Simulation

Open the Unity project and press Play.
The simulation server will begin running and wait for ROS2 connections.

Step 3: Control the Vehicle

Send velocity commands using keyboard teleoperation:

ros2 run teleop_twist_keyboard teleop_twist_keyboard \
--ros-args --remap cmd_vel:=/bluerov1/cmd_vel


The ROV will respond in real time to velocity inputs.

Software Stack

Unity (Simulation Server)

Unity Robotics Hub packages

ROS2 Humble distribution

Academic Context

This project was prepared as part of a university coursework
focused on simulation servers and human–robot interaction (HRI).




