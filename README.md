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

