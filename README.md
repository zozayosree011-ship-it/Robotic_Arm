# Robotic Arm Control System Using AVR

## Project Overview

This project is an **AVR-based robotic arm control system** that allows the user to control a robotic arm using a **4×4 Keypad** and display the current operation on a **16×2 LCD**.

The robotic arm uses **four servo motors**:

* **Base Servo:** Controls left/right rotation.
* **Arm Servo 1 & Arm Servo 2:** Move together to control the forward/backward movement of the arm.
* **Gripper Servo:** Controls opening and closing of the gripper.

## Features

* Control the robotic arm using a 4×4 keypad.
* Move the base **left and right**.
* Move the arm **forward and backward**.
* Open and close the gripper.
* Each movement changes the servo angle by **5°**.
* Servo angles are limited between **0° and 180°**.
* LCD displays the current operation.
* Uses hardware timers to generate the PWM signals required to control the servos.

## Keypad Controls

| Key | Function             |
| --- | -------------------- |
| `8` | Move Arm Forward     |
| `2` | Move Arm Backward    |
| `4` | Move Base Left       |
| `6` | Move Base Right      |
| `5` | Open / Close Gripper |

## Hardware Used

* AVR Microcontroller
* 4 Servo Motors
* 4×4 Matrix Keypad
* 16×2 LCD
* Power Supply
* Robotic Arm Mechanism

## Microcontroller Peripherals

The project uses the following AVR peripherals and drivers:

* **DIO:** Controls servo output pins.
* **Timer0:** Generates PWM for the Base Servo.
* **Timer1:** Generates PWM for the two Arm Servos.
* **Timer2:** Generates PWM for the Gripper Servo.
* **Keypad Driver:** Reads user commands.
* **LCD Driver:** Displays system status.
* **Global Interrupt:** Enabled during system initialization.

## Servo Connections

| Servo   | Timer Output | AVR Pin | Function           |
| ------- | ------------ | ------- | ------------------ |
| Base    | OC0          | PB3     | Left / Right       |
| Arm 1   | OC1A         | PD5     | Forward / Backward |
| Arm 2   | OC1B         | PD4     | Forward / Backward |
| Gripper | OC2          | PD7     | Open / Close       |

## Software Structure

The project is divided into several software layers:

```text
Application
    │
    ├── Keypad
    ├── LCD
    │
HAL
    │
    ├── KPD Driver
    └── LCD Driver
    │
MCAL
    │
    ├── DIO
    ├── Timer0
    ├── Timer1
    ├── Timer2
    └── Global Interrupt
    │
LIB
    ├── STD_TYPES
    └── BIT_MATH
```

## Servo Control

The software converts the required servo angle from **0° to 180°** into the corresponding timer compare value.

The initial position of the arm is:

* Base = **90°**
* Arm 1 = **90°**
* Arm 2 = **90°**
* Gripper = **Open**

The arm and base movements are performed incrementally using a **5° step**, making the movement easier to control.

## LCD Status

The LCD provides simple feedback to the user, such as:

```text
Ready
Move: Forward
Move: Backward
Move: Left
Move: Right
Catch
Release
```

## Main Concept

The system continuously reads the keypad. When a valid key is pressed, the corresponding servo angle is updated and the new position is sent to the appropriate timer PWM output. The LCD then displays the performed action.

## Project Goal

The main goal of this project is to implement a simple and reliable **embedded control system for a robotic arm**, combining **AVR timers, PWM, keypad input, LCD output, and servo motor control**.
