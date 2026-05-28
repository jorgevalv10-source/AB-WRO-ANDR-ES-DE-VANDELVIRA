
### WRO 2026 - Future Engineers Category
**Team:** Andrés de Vandelvira  
**Country:** Spain 🇪🇸

---

## Team Members & Staff
* **Students:**
    * Fernando Auñón García
    * Máximo Navalón Calavera
    * Adrián García Martínez
    * Jorge Valverde Navarro
    * Alejandro López Roderas
* **Coach / Teacher:**
    * Marcelino Marín Pérez

## 🛠️ Technical Description

Our autonomous vehicle is built using **Nezha expansion parts** and powered by a **BBC micro:bit** board as the core controller. 

### Vehicle Architecture & Powertrain
* **Chassis:** Structured with low-clearance bars to properly house the central power module, micro:bit board, motors, and sensors.
* **Actuation & Steering:** We implemented a dual-motor configuration. 
    * A **front directional motor** coupled with a steering rack system controls the vehicle's turning angle.
    * A **rear traction motor** delivers the driving force to move forward and backward efficiently.
* **Wheels:** Fitted with two large high-traction rear wheels for stability and power, and two slim, low-friction front wheels to maximize steering accuracy.

### Sensors & Vision System
* **Computer Vision:** We integrated a **HuskyLens AI camera** configured for real-time color detection. This allows the vehicle to recognize traffic/colored blocks, detect boundary walls, and locate the parking zone.
* **Distance Sensors:** The vehicle utilizes **three ultrasonic sensors** for environment mapping and localization:
    * **Front Sensor:** Measures distance to oncoming walls to accurately calculate when to execute turns at corners.
    * **Right-Side Sensor:** Keeps a constant wall distance reference to guide the car steadily through straight sections.
    * **Left-Side Sensor:** Working alongside the right sensor, it calibrates the car’s exact middle position on the track, ensuring a reliable autonomous start from any starting point.

---

## 📋 Component List
* 1x BBC micro:bit board
* 1x Nezha Expansion Module (Power & motor driver)
* 1x HuskyLens AI Vision Sensor + Custom mounting bracket
* 3x Ultrasonic Distance Sensors
* 1x Driving Motor (Rear traction)
* 1x Steering Motor (Front direction)
* 2x Large rear wheels
* 2x Small/slim front wheels
* Nezha structural parts & custom cabling

---

## 📈 Engineering Development & Challenges

### Robot Prototyping
During the initial design phases, we faced structural challenges. We started with a three-wheeled concept and struggled to find an optimal position for the HuskyLens camera. After two days of iterations, we shifted to a four-wheeled Nezha chassis with dedicated front steering. 

Wiring the HuskyLens also presented challenges due to connection pin compatibility; we solved this by designing a custom pin-to-cable adapter to connect it safely to the central Nezha module. Additionally, to resolve lateral drift and maintain a perfectly centered path, we upgraded our sensor array from one to two side ultrasonic sensors.

### Track & Environment Setup
To test our vehicle under official conditions, we acquired the official canvas track. We constructed custom black perimeter walls to sharply delimit the inner and outer boundaries. 

We encountered tensioning issues keeping the outer walls straight, which we resolved by placing heavy structural blocks at the corners to reinforce them. For the parking zone, we utilized a distinct pinkish hue and stabilized the target wall using a custom cardboard backing structure to ensure rigid placement.
