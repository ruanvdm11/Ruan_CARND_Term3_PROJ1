# Udacity Self-Driving Car Nanodegree

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

A formula was set up that applies a certain deceleration depending on how far the vehicle is away from the self driving car. If a car is closer than 25 metres from us then an initial deceleration of 0.13 m/s^2 is applied. When the vehicle infront is less than 8 metres aways the vehicle decelerates at 0.45 m/s^2. This also means that if a vehicle suddenl drives infront of the self-driving vehcile it will react depending on the distance.

The other important longitudinal part is to maintain the correct velociy that does not exceed the speed limit. If there are no vehicle infront of our vehicle it will accelerate at 0.33 m/s^2 until it reaches roughly 50 mph.
