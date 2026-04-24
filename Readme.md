# Spider Robot
[NO AI USED IN THIS PROJECT]
The Spider Robot is a robot with 4 legs and 12 servos. It was built using Arduino. This Spider Robot has two operating modes. The first mode is Bluetooth control. The second mode is obstacle avoidance. The Spider Robot uses inverse kinematics for movement. It also has a display that shows face animations when it's in Bluetooth mode.

---

## Circuit Diagram

![Circuit Diagram](Schematics.png)

---

## Features

- The Spider Robot has 4 legs with 3 degrees of freedom each. This means the Spider Robot has 12 servos with inverse kinematics.

- In Bluetooth mode you can control the Spider Robot using any Bluetooth app. The Spider Robot uses HC-05 or HC-06 Bluetooth modules.

- In obstacle avoidance mode the Spider Robot navigates on its own using an HC-SR04 sensor.

- The Spider Robot has a display that shows face expressions like happy, sad, angry and sleepy. This only works in Bluetooth mode.

- The Spider Robot can do movements like walking backward turning left and right waving its hand shaking hands and dancing.

- The Spider Robot is powered by two 18650 Li-ion cells that are stepped down to 7 V for the servos.

---

## Hardware

| Component | Qty | Notes |
|---|---|---|
| Arduino Nano | 1 | The main microcontroller of the Spider Robot |
| SG90 / MG90 Servo | 12 | 3 servos per leg of the Spider Robot |
| HC-SR04 Ultrasonic Sensor | 1 | Used for obstacle avoidance in the Spider Robot |
| HC-05 or HC-06 Bluetooth Module | 1 | Used for remote control of the Spider Robot |
| SSD1306 OLED Display | 1 | Shows face animations in Bluetooth mode of the Spider Robot |
| DC-DC Buck Converter | 1 | Steps down the voltage to 7 V for the servos of the Spider Robot |
| 18650 Li-ion Battery | 2 | Powers the Spider Robot at ~7.4 V |
| Toggle Switch | 1 | Turns the Spider Robot on and off |

---

## Wiring

### Servo Pin Mapping

| Leg | Servo | Arduino Pin |
|---|---|---|
| Leg 0 | Coxa / Femur / Tibia | D3 / D4 / D2 |
| Leg 1 | Coxa / Femur / Tibia | D6 / D7 / D5 |
| Leg 2 | Coxa / Femur / Tibia | D9 / D8 / D10 |
| Leg 3 | Coxa / Femur / Tibia | D12 / D11 / D13 |

The servo labels in the diagram correspond to the following pins: Servo 01–03 (D2–D4) 04–06 (D5–D7) 07–09 (D8–D10) 10–12 (D11–D13).

### Sensors & Peripherals

| Module | Pin(s) |
|---|---|
| HC-SR04 Trigger | A5 (D19) |
| HC-SR04 Echo | A4 (D18) |
| Bluetooth TX/RX | D0 / D1 |
| OLED SDA / SCL | A4 / A5 |

Note: The OLED and Bluetooth module share the Arduino pins. They work with firmware sketches. Do not flash both at the time.

### Power

- Two 18650 cells are connected in series to get ~7.4 V. This voltage is then stepped down to 7 V using a DC-DC buck converter. The 7 V rail powers all the servos of the Spider Robot.

- The Arduino is powered from the 7 V rail via VIN or USB during programming.

---

## Firmware

There are two sketches for the Spider Robot:

| File | Mode |
|---|---|
| `Bluetooth-controlling_spider_robot.ino` | Bluetooth remote control + OLED face |
| `Obstacle_Avoiding_Spider_Robot.ino` | Autonomous obstacle avoidance |

### Required Libraries

You can install these libraries using the Arduino Library Manager:

| Library | Purpose |
|---|---|
| `Servo` | Controls the servos of the Spider Robot |
| `FlexiTimer2` | Provides 50 Hz servo ISR timing for the Spider Robot |
| `NewPing` | Drives the HC-SR04 ultrasonic sensor of the Spider Robot |
| `Adafruit SSD1306` | Drives the OLED display of the Spider Robot |
| `Adafruit GFX Library` | Provides graphics primitives for the OLED display of the Spider Robot |
| `Wire` | Enables I²C communication for the Spider Robot |

---

## Getting Started

1. Assemble the frame of the Spider Robot and mount all 12 servos.

2. Wire the components according to the circuit diagram.

3. Install all the required libraries in the Arduino IDE.

4. Choose a sketch based on the desired mode of the Spider Robot.

5. Upload the sketch to your Arduino Nano via USB.

6. Power on the Spider Robot using the toggle switch.

When the Spider Robot boots up for the time it will stand up and perform a short greeting animation before waiting for commands.

---

## Bluetooth Commands

You can connect to the Spider Robot using any Bluetooth terminal app at 9600 baud. Send characters to control the Spider Robot:

| Command | Action | OLED Expression |
|---|---|---|
| `F` | The Spider Robot steps forward | Happy |
| `B` | The Spider Robot steps backward | Sad |
| `L` | The Spider Robot turns left | Angry |
| `R` | The Spider Robot turns right | |
| `W` | The Spider Robot waves its hand | |
| `U` | The Spider Robot shakes hands | |
| `V` | The Spider Robot dances | |

---

## Obstacle Avoidance

When the Spider Robot is in obstacle avoidance mode:

1. The Spider Robot walks forward continuously.

2. The Spider Robot continuously checks for obstacles using the HC-SR04 sensor.

3. If the Spider Robot detects an obstacle within 20 cm it stops turns in a direction. Resumes walking.

You can adjust the detection threshold by changing the value of `int thresh = 20;` in the sketch. This value is in centimeters.

---

## Kinematics Parameters

The Spider Robot uses 3-DOF inverse kinematics per leg. Here are the key physical dimensions in millimeters:

| Parameter | Value |
|---|---|
| Coxa length | 27.5 |
| Femur length | 50 (in Bluetooth mode) / 55 (in obstacle avoidance mode) |
| Tibia length | 77.1 (in Bluetooth mode) / 77.5 (, in obstacle avoidance mode) |
| Body side length | 71 |
| Default stance Z | -50 |
| Step height Z | -30 |

---

## File Structure

```
.
├── Bluetooth-controlling_spider_robot.ino
├── Obstacle_Avoiding_Spider_Robot.ino
└── spider-3-in-1_bb.png
```
