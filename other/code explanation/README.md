## 💻 Software Logic and Algorithm Explanation

Our autonomous program is designed in two main phases to address both the navigation stability and the randomized obstacle challenges.

### Phase 1: Open Challenge & Lap Control
The execution starts with a **While Loop** governed by a lap-counting logic. This is our primary method for ensuring the vehicle completes exactly three laps before stopping.
* **Lap Tracking:** We use a variable named `cuentaparedes` (wall_counter). Every time the `giro` (turn) function is executed at a corner, this variable increments. Since a standard track has 4 corners, once the counter reaches 12, the vehicle identifies that three full laps have been completed and executes a stop command.
* **Navigation Logic:** Within the main loop, an **If-Else** structure monitors the ultrasonic sensors. 
    * **Corner Detection:** When the front ultrasonic sensor detects a wall within a specific threshold, it triggers the `giro` function to navigate the corner.
    * **Straight-Line Stability:** If no front wall is detected, the program executes the `siguedosparedes` (follow_two_walls) function. This algorithm uses the lateral sensors (J1 and J3) to calculate the car's offset and maintain it perfectly centered between the boundaries.

### Phase 2: Obstacle Avoidance & Autonomous Parking
This phase manages the vision-based decision-making process using the HuskyLens AI camera.
* **State Management:** We use a control variable called `controbloques` to manage the vehicle's behavior based on visual input. 
* **Navigation & Cornering:** By default (`controbloques = 0`), the car continues its wall-following logic. If the distance from the left (`izda`) or right (`dcha`) sensors exceeds the `distcentro` threshold, the `giro2` function is called to handle cornering while obstacles are present.
* **Traffic Block Interaction:**
    * **Green Block (Right side):** When the HuskyLens identifies a green signature, `controbloques` switches to **1**. The `seguirverde1` function aligns the car with the block. Once the distance is ≤ 20cm, the `giroizda` function is triggered to safely overtake the block on the left side.
    * **Red Block (Left side):** When a red signature is detected, the variable switches to **2**. The `seguirojo2` function aligns the car, and at a distance of ≤ 20cm, the `giradcha` function executes to dodge the block on the right side.
* **Autonomous Parking Sequence:**
    * The parking logic is protected by a boolean flag. Once the `cuentaparedes` variable indicates the completion of the required laps, the `aparca` (park) variable becomes **False**.
    * When the camera detects the **Magenta** color signature (Parking Zone) and `aparca` is False, `controbloques` is set to **3**.
    * This activates the `seguirmagenta` routine to center the robot with the parking slot. When the distance reaches 20cm, the `aparcar` function executes a specialized reverse-entry maneuver, followed by a stabilizing forward-and-backward sequence (8 iterations) to ensure the vehicle is perfectly positioned within the zone before the final system shutdown.
