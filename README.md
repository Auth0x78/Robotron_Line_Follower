# Line Following Robot with TT Motors and IR Sensors

This project is a simple line-following robot using two TT motors, three IR sensors, and an AVR microcontroller. The robot is programmed to follow a black line on a white background, adjusting its motor speed and direction based on input from the IR sensors. This project uses PID control to ensure smooth and precise movement.

## Hardware Requirements

- AVR Microcontroller (e.g., Arduino Uno)
- TT Motors (DC geared motors)
- Motor Driver (e.g., L298N)
- Three IR Sensors
  - **Right**: Connected to pin 11
  - **Left**: Connected to pin 12
  - **Center**: Connected to pin 4
- Power source
- Breadboard and wires

## Code Overview

### Pin Definitions

- **IR Sensors**
  - `IR_SENSOR_RIGHT` (Pin 11)
  - `IR_SENSOR_LEFT` (Pin 12)
  - `IR_SENSOR_CENTER` (Pin 4)

- **Motor Control**
  - Right Motor (Motor A): Pins 5 (ENA), 9 (INA1), 10 (INA2)
  - Left Motor (Motor B): Pins 6 (ENB), 7 (INB1), 8 (INB2)

### Key Parameters

- **Motor Speeds**
  - `MOTOR_SPEED`: Normal forward speed.
  - `NC_SPEED`: No confidence speed, when bot doesn't see forward path revert to lesser speed amount.
  - `REV_SPEED`: Reverse speed for sharp turns or reversing.

- **PID Control Parameters**
  - `kp`, `kd`, and `ki`: Proportional, derivative, and integral gains for the PID controller.

### Watchdog Timer

A watchdog timer (`wdt`) is set to 250ms, which resets the controller if the code encounters an issue or stalls. This ensures the robot continues to function even if it encounters unexpected states.

### Functions

- `rotateMotor(int rightMotorSpeed, int leftMotorSpeed)`: Controls the motors' speed and direction.
- `rotateMotorSharp(int rightMotorSpeed, int leftMotorSpeed, int delayms)`: Controls the motors for sharp turns with a specified delay.

### Control Loop

The control logic is based on the following steps:
1. Read values from the IR sensors to determine line position.
2. Calculate the error for the PID controller.
3. Use PID correction to adjust the motor speed and direction.
4. The center sensor guides straight motion; left and right sensors are used for turns.

### PWM Frequency Adjustment

To control the motor speed at lower PWM values, the PWM frequency on pins D5 and D6 is set to 7812.5 Hz for smoother motion.

## Setup and Compilation

1. Connect the hardware as described above.
2. Compile and upload the code to the microcontroller using the Arduino IDE or other compatible software.
3. Place the robot on a black line and observe its movement.

## License

This project is licensed under the MIT License.
