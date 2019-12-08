# **Path Planning** 

---

**Introduction**

The goal of this project is to navigate the car through a map  with following criteria
* The car drives atleast 4.32 Miles without incident
* The car respects the speed limit
* Maximum Acceleration / Jerk is not Exceeded.
* Car does not have collissions
* Car stays in lane except for changing the lanes
* The car is able to change lanes

---

### Reflection

### 1. Inputs

Model provides following inputs to decide on the trajectory of simulated cars
1. Map waypoints(x, y, s, dx and dy)
2. Simulated Cars (x, y, s, d, yaw, speed)
3. Previous Paths (x, y)
4. end_path (s,d)
5. Other Vehicles (s,d, vx, vy)



### 2. Steps

Previous Paths keep a list of points not consumed the simulator. At a time, there as many 50 points provided in previous path as input to the simulator.

#### i) Generating a smooth trajectory
1. Model generate a smooth trajectory using the spline implementation. 
2. It uses tangents from the last 2 points in the previous path to maintain continuity. 
3. 3 points are chosen 30 meters apart.
4. The above generated 5 points are fed to Spline , to generate a curve equation.
5. Points are chosen on the curve for a distance of upto 30 meters, so that number of points fed to the simulator is not more than 50.
#### ii) Avoiding Jerks
To avoid the jerk, the speed of the vehicle is increased / decreased with maximum allowed acceleration/deacceleration of 0.224 miles/hour
#### ii) Avoiding Collission
1.  Frenel coordinates are used to define the vehicles with respect to other vehivles.
2.  Model uses the variable too_close to mark the proximity with vehicles in the same lane.
3. Vehicles in the same lane with distance lesser than 30 meters infront of it are defined as close.
4. If a vehicle is too close and there are no empty slots available in the adjacent lane, the vehicle starts reducing its speed to avoid collission.

#### iii) Changing lane
1. Model examines vehicles in all lanes in same direction.
2. All vehicles in 30 meters radius are defined as close.
3. If there is a vehicle too close in the current lane, the vehicle checks adjacent lanes.
4. If there are no vehicles in adjacent lane, the vehicle switches lane.
5. Vehicle switches one 1 lane at a time.

