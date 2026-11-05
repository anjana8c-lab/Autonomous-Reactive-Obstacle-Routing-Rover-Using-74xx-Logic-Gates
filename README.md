# Autonomous Reactive Obstacle Routing Rover Using 74xx-Logic Gates

An autonomous obstacle-routing rover that operates entirely using discrete digital logic components without any microcontroller, programming, or embedded softwareThe rover continuously monitors its surroundings using three obstacle sensors positioned on the left, center, and right sides. Based on the obstacle information, a combinational logic circuit built using 74xx series logic ICs determines the appropriate motor actions. The logic immediately controls the wheel motors, enabling the rover to move forward, turn away from obstacles, or stop when no safe path is available.

# Working Principle & Logic Design

The **Autonomous Reactive Obstacle-Routing Rover** operates entirely on real-time combinational hardware logic without using any microcontrollers or software programming.

---

## 1. System Inputs & Outputs

### Input Signals (Sensors)
The rover continuously monitors its immediate environment using three front-facing Infrared (IR) obstacle sensors:
* **S_L**: Left Sensor
* **S_C**: Center Sensor
* **S_R**: Right Sensor

**Logic Convention:**
* `1` = Obstacle detected
* `0` = Path clear

---

### Output Signals (Motor Drivers)
The decisions made by the logic gates directly control two DC BO Motors via transistor driver circuits:
* **M_L**: Left Motor
* **M_R**: Right Motor

**Logic Convention:**
* `1` = Motor ON
* `0` = Motor OFF

---

## 2. Truth Table

The control logic evaluates all possible input states to determine the correct motor behavior:

| S_L (Left) | S_C (Center) | S_R (Right) | M_L (Left Motor) | M_R (Right Motor) | Rover Behavior |
| :---: | :---: | :---: | :---: | :---: | :--- |
| **0** | **0** | **0** | **1** | **1** | **Move Straight** |
| **0** | **0** | **1** | **1** | **0** | **Turn Left** |
| **0** | **1** | **0** | **0** | **0** | **Stop** |
| **0** | **1** | **1** | **0** | **0** | **Stop** |
| **1** | **0** | **0** | **1** | **0** | **Turn Right** |
| **1** | **0** | **1** | **0** | **0** | **Stop** |
| **1** | **1** | **0** | **0** | **0** | **Stop** |
| **1** | **1** | **1** | **0** | **0** | **Stop** |

---

## 3. Simplified Boolean Logic Equations

By solving the truth table using Boolean algebra, the functions simplify to minimal expressions:

### Left Motor Expression (M_L)
The Left Motor runs only when **neither** the Center nor the Right sensor detects an obstacle.
> **Logic Formula: M_L = S_C' · S_R'**

### Right Motor Expression (M_R)
The Right Motor runs only when **neither** the Center nor the Left sensor detects an obstacle
> **Logic Formula: M_R = S_C' · S_L'**
---

## 4. Hardware Implementation
1. **IC 7404 (Hex Inverter):** Used to invert the sensor signals
2. **IC 7408 (Quad AND Gate):** Used to perform the logical AND operation between the inverted signals.
