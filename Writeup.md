Path Planning Project 
__________________________
This project deals with path planning. For this purpose, the simulator provides us with telemetry data like x and y cartesian coordinates, s and d Frenet coordinates in the map, as well as yaw and speed data. 
Furthermore sensor fusion data is available, listing all other cars on the same side of the road.
The waypoints show the way car should follow along the highway. They are listed in a csv-file and read into a vector in the C++ Code.

To move the car in the simulator, a vector of x and a vector of y values have to be sent to the simulator. The time interval of the simulator is 0.02s, so the velocity of the car is calculated by the distance between the new (x_new,y_new) position and the actual (x,y) position, divided by the time interval 0.02s.

The challenge is to respect the acceleration, jerk and speed limits, but also not to collide with other vehicles. The car should be able to change lanes if necessary.
---------------------------
In line 253, the starting lane is defined. After evaluating the telemetry in line 279-291, the sensor fusion data is used to look for cars in the same lane (line 310-330).
If there is another car in front of the ego-car within a defined distance, the flag lane_change is set to true. Next in line 332, the flag lane_change is checked and leads to the a check if a lane change is safe or not. 
If the lane_change flag is false, there are two options: accelerating to speed limit, or keeping the velocity (obviously the speed limit is already reached then).
The lange change algorithm first uses the localization date to distinguish between different case: ego car is in the left, middle or right lane. 
By using the function check_gap, which is defined in line 183, the other lanes are checked by using the sensor fusion data. Every car in the respective lane is checked concerning its distance to the ego car.
If there is a car within a defined distance in front or behind the ego car, the flag lane_change_possible is turned to false.
In this case the velocity is reduced to match the car in front of us. 
----------------------------
Changing the velocity is achieved by setting the variable ref_vel, which is part of the calculation of the distance between the x and y points in the lines 507 - 510.
----------------------------

