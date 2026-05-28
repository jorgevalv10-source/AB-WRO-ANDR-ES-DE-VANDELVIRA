# AB-WRO-ANDR-ES-DE-VANDELVIRA 🚀
### WRO 2026 - Future Engineers Category
**Team Name:** Andrés de Vandelvira  
**Country:** Spain 🇪🇸  
**Platform:** BBC micro:bit + Nezha Expansion Framework

---

## 👥 Team Members & Staff
* **Students:**
    * Marcelino Marín Pérez
    * Máximo Navalón Calavera
    * Adrián García Martínez
    * Jorge Valverde Navarro
    * Alejandro López Roderas
* **Coach / Teacher:**
    * Fernando Auñón García

> 📜 *Our signed **WRO Code of Ethics** is fully digitized and available under the `documentation/` directory of this repository.*

---

## 📸 Media Gallery
<p align="center">
  <img src="media/team/team photo.jpg" alt="Andrés de Vandelvira Engineering Team" width="45%"/>
  <img src="media/robot_photo.jpg" alt="Autonomous Vehicle Architecture" width="45%"/>
</p>

---

## 🛠️ Complete Project Overview & Technical Description

Our autonomous vehicle has been engineered from the ground up to satisfy the technical and operational constraints established by the WRO 2026 Future Engineers official guidelines. The structural framework is primarily designed using modular **Nezha expansion parts**, which provide high rigidity while keeping the structural mass below the maximum regulatory limits. The electronic brain governing all computation is a **BBC micro:bit** microcontroller, integrated onto a specialized Nezha breakout board that manages power distribution, motor actuation, and sensor interfaces.

### 1. Vehicle Mechanical Architecture & Powertrain System
The chassis features a low-clearance structural design utilizing foundational base-bars. This mechanical configuration was selected to optimize the vehicle's center of gravity, preventing lateral tipping during high-velocity turns. 
* **Actuation and Dynamic Steering:** Unlike differential-drive robots, our vehicle relies on a realistic car-like cinematic configuration. It is equipped with two independent motors:
    * **Front Steering Actuator:** A dedicated motor connected to a mechanical steering rack system that manipulates the steering geometry of the front wheels, allowing smooth and predictable turning angles.
    * **Rear Traction Powertrain:** A high-torque motor positioned on the rear axle delivering direct driving force to the rear wheels, providing continuous thrust to navigate both straights and sharp corners.
* **Wheel Configuration Geometry:** To minimize friction while maximizing surface grip, we utilized two distinct wheel sizes. The rear driving axle features large, high-traction rubber wheels designed to prevent slipping and maintain consistent odometer estimates. The front steering steering axle utilizes slim, low-friction profile wheels to guarantee that steering commands translate accurately to physical path corrections without structural binding.

### 2. Sensor Integration & Computer Vision Framework
To achieve full situational awareness on the track, our platform fuses computer vision telemetry with acoustic distance measurements.
* **Vision Processing Unit:** We integrated a **HuskyLens AI camera module** connected via a custom pin-to-cable adapter directly into the main communication bus of the Nezha board. This camera is calibrated to process real-time color signatures, specifically targeting traffic blocks (red and green pillars), tracking boundary walls, and identifying the specialized pinkish-toned parking zone.
* **Ultrasonic Distance Array:** The vehicle incorporates a multi-directional array of **three ultrasonic sensors** to accurately map the boundaries of the racetrack:
    * **Front-Facing Sensor:** Measures the longitudinal distance to upcoming walls, serving as the main trigger to initiate cornering maneuvers.
    * **Right-Side Sensor:** Constantly monitors the distance to the right perimeter wall, establishing a stable spatial baseline for wall-following behaviors.
    * **Left-Side Sensor:** Introduced in later iterations, this sensor works symmetrically with the right sensor to calculate the exact geometric center of the track. This dual-lateral sensing architecture guarantees that regardless of the randomized starting position or direction, the vehicle balances itself dynamically on the track.

---

## 📋 Electromechanical Component List
* **1x BBC micro:bit Controller:** Serves as the primary execution unit for our unified software stack.
* **1x Nezha Expansion Module:** Manages voltage regulation, motor power supply, and multi-sensor routing.
* **1x HuskyLens AI Camera:** High-speed vision processor for multi-signature color recognition.
* **3x Custom Ultrasonic Sensors:** High-frequency acoustic transducers for distance mapping.
* **1x Drive Motor:** High-efficiency DC actuator configured for rear-wheel power delivery.
* **1x Steering Motor:** High-precision directional actuator mated to the front steering mechanism.
* **2x High-Grip Rear Wheels:** Optimized for friction management and acceleration stability.
* **2x Slim Front Wheels:** Specially selected to reduce turning drag and increase steering fidelity.
* **Nezha Structural Components:** Comprehensive set of bars, pins, and mounting brackets.

---

## 💾 Software Architecture & Unified Code Base

Per WRO 2026 regulations, code adjustments are prohibited once a competition round commences. Since track variables, driving direction, and challenges are randomized right before the start sequence, our engineering team developed a **Unified Software Architecture**. All operational routines—including the Open Challenge navigation, Obstacle Challenge logic, and the Parallel Parking subroutine—are integrated into a single, comprehensive program file located at `src/main.hex`.

### Code Structure and Functional Modules
The software logic is divided into modular subroutines designed to run inside a high-speed execution loop:
1. **System Initialization Module:** Executes immediately upon power-on. Configures the I2C communication channels for the HuskyLens, establishes input/output pins for the three ultrasonic sensors, resets the steering servo to its absolute center ($90^\circ$), and initializes internal state variables.
2. **Mode Selection Routine:** Utilizing the built-in physical inputs on the micro:bit (Buttons A and B), the team can toggle the active challenge mode during technical setup. Pressing Button A loads the *Open Challenge* state variables, while Button B arms the *Obstacle Challenge* routines, fulfilling the dual independent button starting sequence required by Rule 9.10/9.11.
3. **Sensor Fusion & Calibration Loop:** Reads data from all three ultrasonic sensors simultaneously. It calculates the error offset relative to the track center using the formula: $Error = Distance_{Left} - Distance_{Right}$. This error feeds directly into our navigation logic to apply proportional steering corrections.
4. **Vision Processing Routine:** Queries the HuskyLens every cycle. If a color block signature is returned, the code processes its horizontal X-coordinate. If a Green Block is detected, the steering shifts left; if a Red Block is detected, the steering shifts right to avoid a collision.
5. **Parallel Parking Subroutine:** Activated exclusively during the Obstacle Challenge mode. An internal counter tracks completed laps via front wall detection. Upon entering the 3rd lap, the software activates the pink color signature filter. Once the parking zone is detected via HuskyLens, the forward drive loop terminates, and a pre-calculated timed reverse steering sequence executes to park the vehicle completely inside the magenta-bordered zone.

### Compilation and Execution Guide
To compile, flash, and run our software on the vehicle, follow these precise technical steps:
1. Launch the official **Microsoft MakeCode for micro:bit** editor (or your local Python IDE if running a script version).
2. Import the project code by selecting "Load File" and choosing `src/main.hex` from this repository.
3. Ensure the **Nezha** and **HuskyLens** extensions are fully loaded into your environment palette.
4. Connect the micro:bit controller to your computer via a high-quality USB-to-microUSB data cable.
5. Click the **Download** button in the IDE to compile the source code into binary machine format. Flash the compiled file directly onto the micro:bit drive.
6. Mount the micro:bit securely onto the vehicle's Nezha breakout board.
7. Turn on the independent system power switch. Select the desired challenge mode using the micro:bit interface buttons. Place the vehicle at the designated starting position, and press the start trigger to execute autonomous navigation.

---

## 📈 Engineering Development Process & Iterations

### 1. Prototype Design Challenges
Our early developmental phases were marked by structural instability. We initially built a three-wheeled vehicle prototype, but quickly discovered that mounting the heavy HuskyLens camera on a high-clearance bracket caused massive front-end vibrations and balance failures during sharp cornering. To resolve this, we scrapped the three-wheeled design and shifted to a robust four-wheeled chassis with independent front-wheel steering. 

Connecting the HuskyLens presented a major hardware compatibility hurdle due to conflicting connector pin footprints on the Nezha board. Our team designed a custom wire-to-pin mapping harness that safely bridges the camera data lines to the main bus without causing voltage drops. Furthermore, during track testing, we noticed that a single lateral ultrasonic sensor allowed the vehicle to drift or snake down straightaways. We resolved this path deviation by introducing a symmetrical third ultrasonic sensor on the opposite side, creating a reliable auto-balancing algorithm.

### 2. Racetrack Environment Optimization
To ensure our development environment matched tournament standards, we installed an official competition canvas. Building the perimeter walls presented structural challenges; the initial black cardboard boundaries warped easily, altering the sensor baseline distance readings. We engineered a locking corner block system using rigid Nezha parts to square the outer walls and eliminate deviations. For the obstacle parking challenge, we calibrated the target wall using heavy cardboard backings to ensure it remained perfectly upright, allowing the HuskyLens color filters to lock onto the pink target signature consistently under shifting ambient light conditions.

---

## 🎥 Autonomous Video Demonstrations

Our autonomous vehicle performance has been fully logged and published on YouTube Shorts. The videos capture uninterrupted, autonomous operations exceeding the 30-second regulatory requirement for both official formats:

* 🏎️ [Laps & Wall-Following Challenge - Open Challenge Video](https://youtube.com/shorts/PFYmbsbghdM?feature=share)
* 🛑 [Traffic Block Avoidance - Obstacle Challenge Video](https://youtube.com/shorts/C6o_aeeS0og?si=LdYddICI6gDbA_ps)
* 🅿️ [Autonomous Parallel Parking Maneuver - Parking Video](https://youtube.com/shorts/OMSZubMgkV8?feature=share)
