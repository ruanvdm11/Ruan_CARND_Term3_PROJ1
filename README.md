# Udacity Self-Driving Car Nanodegree

[//]: # (Image References)
[image1]: https://raw.githubusercontent.com/ruanvdm11/Ruan_CARND_Term3_PROJ1/master/Reference_Images/Video_Screenshot.png "Video1"

## Term 3 Project 1: Path Planning

### Introduction
I n this project is was necessary to use the Term 3 udacity simulator in order to use some sensor fusion data to do path planning. The scope for the project is very open with some clear goals:
* Have zero collisions.
* Do not accelerate too fast.
* Do not exceed the speed limit.

These are the main constraints that need to be adhered to by the vehicle on its course on a freeway.

### Maintaining the Speed
The class note provide a good method to get started on the course such that the vehicle maintains its lane and a set velocity. IN order to maintain the correct lane it is easiest to use Frenet coordinates, where -s is seen as the distance along a curve (longitudinal travel) and -d is the perpendicular offset from a curve (lateral motion).

An array of values are created that represents x and y coordinates. The simulator then calls a set (x and y) of coordinates every 0.2 seconds. This means that depending on the distance between consecutive points; the velocity of the vehicle can be controlled.

### Longitudinal Control
The next step to focus on is to ensure that the vehicle does not drive into other vehicles from the rear. The vehicle is equiped with some instrumentation that allows us to create some sensor-fused data that allows us to know the whereabouts of the other vehicles. By knowing the Frenet coordinates of the other vehicles a filter can quickly be set up that can distnguish between cars in different lanes. Then it is possible to search for the closest car infront of us (defined by a larger -s values than our current -s value) and make certain decisions based on proximity of the other vehicle.

A formula was set up that applies a certain deceleration depending on how far the vehicle is away from the self driving car. If a car is closer than 25 metres from us then an initial deceleration of 0.65 m/s^2 is applied. When the vehicle infront is less than 8 metres aways the vehicle decelerates at 2.25 m/s^2. This also means that if a vehicle suddenl drives infront of the self-driving vehcile it will react depending on the distance.

The other important longitudinal part is to maintain the correct velociy that does not exceed the speed limit. If there are no vehicle infront of our vehicle it will accelerate at 1.65 m/s^2 until it reaches roughly 50 mph.

### Lateral Control
If a vehicle determines that there is another vehicle getting too close it signals that an overatke is required. The overtake also make suse of the sensor fusion data but now it evaluates the adjacent lanes.

Firstly, the function determines if there is a reasonable 'gap' in the lane to the left. A reasonable gap means that if lane change is make that the closest car infront of our vehicles is greater than 27 metres away and the closest vehicle to the rear is 5 metres away. 

Secondly, if the change cannot be made to the left lane the same checks are done to determine if a lane change to the right is possible.

Lastly, if the vehicle is not in the left most lane. It will determine whether there is sufficient space to move to the left (fast) lane. If the closest vehicle (ahead of our car) in the lane to our left is 40 metres away and we are 5 metres ahead of a vehicle in the lane to our left; the vehicle will move to the left.

Please see the below video that shows a successful run of the track.

[![alt text][image1]](https://youtu.be/yu87EzoiUrY)
