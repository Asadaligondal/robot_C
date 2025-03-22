VEX IQ Autonomous Robot Project
This repository contains a RobotC program for a VEX IQ robot designed to navigate a custom environment using line following, obstacle avoidance, and data logging capabilities.

Project Overview
Software: RobotC for VEX Robotics 4.x
Environment: Custom setup with a black line on a white surface (grayscale values: ~200-330 for the line, >356 for white) and obstacles (e.g., walls) detectable within 210 mm.
Hardware: VEX IQ robot with:
Left Motor (port 1)
Right Motor (port 6, reversed)
Line Detector (port 3, grayscale mode)
Distance Sensor (port 2)
Code Flow
Initialization: Sets initial motor speeds, resets encoders, and logs a CSV header to the Debug Stream.
Main Loop:
Wandering: Randomly moves (left, right, forward) every 5 loops (~250 ms), checks for lines or obstacles.
Line Following: Follows a black line (grayscale 200-330) by turning left/right based on sensor readings.
Obstacle Avoidance:
Slows proportionally as distance to an obstacle drops from 210 mm to 10 mm.
Stops at 10 mm, moves backward for 0.5s, then executes a predefined maneuver (right turn, forward, left turn, forward).
Data Logging: Records distance, speed, acceleration, obstacles avoided, and state times every 1s to the Debug Stream.
State Transitions: Switches states based on line detection or obstacle proximity, with immediate line following when detected.
Proportional Control
Mechanism: In OBSTACLE_AVOIDANCE, motor speed scales from 50 (at 210 mm) to 0 (at 10 mm) using the formula:
text

Collapse

Wrap

Copy
proportionalSpeed = baseSpeed * (currentDistance - minDistance) / (distanceThreshold - minDistance)
Behavior: Robot slows smoothly as it nears an obstacle, stops at 10 mm, then triggers the avoidance sequence.
Setup Instructions
Install RobotC:
Download and install RobotC for VEX Robotics 4.x from www.robotc.net.
Ensure the VEX IQ firmware is updated via the RobotC IDE.
Check Port Configuration:
Open the code in RobotC.
Go to Robot > Motors and Sensors Setup.
Verify:
leftMotor on port 1
rightMotor on port 6 (reversed)
lineDetector on port 3 (ColorGrayscale mode)
distanceMM on port 2 (Distance mode)
If ports differ (e.g., your distance sensor is on port 7), update the #pragma config lines accordingly.
Run the Program:
Connect the VEX IQ brain to your PC via USB.
Compile and download the code to the robot via Robot > Compile and Download.
Start the program from the VEX IQ brain or RobotC.
Access Logs:
Open Robot > Debugger Windows > Debug Stream in RobotC.
Run the robot, then copy the CSV data (e.g., Time,State,Distance,...) from the Debug Stream.
Paste into a text editor and save as robot_log.csv for analysis.
Environment Details
Custom Setup: A flat surface with a black line (width ~1-2 cm) on a white background, plus obstacles (e.g., walls or boxes) within 210 mm of the robot’s path.
Calibration: Adjust lineThreshold (250), distanceThreshold (210), and minDistance (10) if your line grayscale or obstacle distances differ.
Usage Notes
Wheel Diameter: Set to 60 mm in the code. Update wheelDiameter if your wheels differ for accurate distance logging.
Debugging: Add displayTextLine() calls (e.g., for distance or state) to the VEX IQ screen if needed for real-time monitoring.
Port Issues: If sensors/motors don’t respond, double-check port numbers and cable connections in the Motors and Sensors Setup window.
License
MIT License (feel free to modify as needed)
