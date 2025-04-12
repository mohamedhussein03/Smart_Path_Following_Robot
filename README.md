📌 Project Overview
This project was developed as part of the Computer Control course during Spring 2025 at the British University in Egypt (BUE).
It demonstrates the design and implementation of an autonomous mobile robot capable of:

Following a black path using IR sensors

Avoiding obstacles using ultrasonic sensors

Returning to the path after rerouting

The system is built using an Arduino Uno and integrates real-time sensor data, servo motor scanning, and intelligent decision-making logic.


⚙️ Features

🔍 Line Following using a 3-way IR sensor module

🚧 Obstacle Detection using an HC-SR04 ultrasonic sensor

🔄 Path Recovery after obstacle avoidance

🧠 Servo-based scanning from 0° to 180° for better pathfinding

🤖 Autonomous behavior blending both line tracking and obstacle navigation


🛠️ Hardware Used
Arduino Uno

3-way IR sensor module

HC-SR04 ultrasonic sensor

DXW90 servo motor

L298N motor driver

4 DC motors

Chassis with wheels and caster

Jumper wires, battery pack, breadboard


Behavior Overview
Startup: Robot begins by scanning its environment and aligning to the line.

Normal Mode: Follows the black line using the IR sensor.

Obstacle Detected: If an obstacle is detected within 12 cm, the robot stops.

Avoidance Mode: Servo scans for the best clear direction, reroutes the robot accordingly.

Recovery Mode: After bypassing the obstacle, the robot searches for and returns to the line.


🖥️ Software & Logic
The code is written in C/C++ (Arduino IDE) and structured for modular control:

IR sensor values determine motor direction (line following)

Ultrasonic sensor triggers obstacle avoidance

Servo scans multiple angles to find the optimal reroute path

Motor control logic handles navigation and turning sequences
