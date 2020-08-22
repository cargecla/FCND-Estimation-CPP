## Project: Estimation for a 3D Quadrotor
![Scenario1_Simulator](./Scenario1_Simulator.png)

---


## [Rubric](https://review.udacity.com/#!/rubrics/1643/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it! Below I describe how I addressed each rubric point and where in my code each point is handled.

### Implemented Controller General

#### 1. Implemented controller in C++.
These scripts contain a basic controller implementation that includes the following:

1) Introduction (scenario 1):

In this scenario it is required to make the drone hover less than a second by adjusting the mass of the drone on the QuadControlParams.txt file.

[Scenario1_Simulator.mp4](./Scenario1_Simulator.mp4)


2) Body rate and roll/pitch control (scenario 2):

In this scenario it is required to implement the GenerateMotorCommands(), BodyRateControl() and RollPitchControl() functions. It is also require to tune the kpPQR and kpBank parameters using the QuadControlParams.txt file and the .\FCND-Controls-CPP\project\Simulator.sln provided.


[Scenario2_Simulator.mp4](./Scenario2_Simulator.mp4)


3)Position/velocity and yaw angle control (scenario 3):

In this scenario it is required to implement the LateralPositionControl(), AltitudeControl() and YawControl() functions. It is also require to tune the kpPosZ, KiPosZ, kpVelXY, kpVelZ, kpYaw and kpPQR {3rd (z) component} parameters using the QuadControlParams.txt file and the .\FCND-Controls-CPP\project\Simulator.sln provided.


[Scenario3_Simulator.mp4](./Scenario3_Simulator.mp4)


4)Non-idealities and robustness (scenario 4):

In this scenario it is required to edit the AltitudeControl() function to add integral control to our controller (PID). It is also require to tune various parameters using the QuadControlParams.txt file and the .\FCND-Controls-CPP\project\Simulator.sln provided.

[Scenario4_Simulator.mp4](./Scenario4_Simulator.mp4)


5)Tracking trajectories (scenario 5):

In this scenario it is require to tune various parameters using the QuadControlParams.txt file and the .\FCND-Controls-CPP\project\Simulator.sln provided. Thus, your drone follow the trayectory.

[Scenario5_Simulator.mp4](./Scenario5_Simulator.mp4)


### Implemented Controller

#### 1. Implemented body rate control in C++
The controller should be a proportional controller on body rates to commanded moments. The controller should take into account the moments of inertia of the drone when calculating the commanded moments.

On the QuadControl.cpp file, from line 112 to 116 the body rate control is implemented as a proportional controllers that commands moments using the momenta of inertia.


#### 2. Implement roll pitch control in C++
The controller should use the acceleration and thrust commands, in addition to the vehicle attitude to output a body rate command. The controller should account for the non-linear transformation from local accelerations to body rates. Note that the drone's mass should be accounted for when calculating the target angles.

Using the accelearation, thrust command and vehicle attitude, it was determine the body rate command from line 147 to 165 of the QuadControl.cpp file.


#### 3. Implement altitude controller in C++
The controller should use both the down position and the down velocity to command thrust. Ensure that the output value is indeed thrust (the drone's mass needs to be accounted for) and that the thrust includes the non-linear effects from non-zero roll/pitch angles. Additionally, the C++ altitude controller should contain an integrator to handle the weight non-idealities presented in scenario 4.

The altitude controller was implemented between line 197 and 212 of the of the QuadControl.cpp file.


#### 4. Implement lateral position control in C++
The controller should use the local NE position and velocity to generate a commanded local acceleration.

From line 250 to 257, the lateral position controller was implemented in order to generate the commanded local acceleration.


#### 5. Implement yaw control in C++
The controller can be a linear/proportional heading controller to yaw rate commands (non-linear transformation not required).

In order to include yaw control the lines of code from 280 to 282 were implmented. Refer to the QuadControl.cpp file.


#### 6. Implement calculating the motor commands given commanded thrust and moments in C++
The thrust and moments should be converted to the appropriate 4 different desired thrust forces for the moments. Ensure that the dimensions of the drone are properly accounted for when calculating thrust from moments.

This was done on the QuadControl.cpp file from line 79 to 87.



### Flight Evaluation
#### 1. Your C++ controller is successfully able to fly the provided test trajectory and visually passes inspection of the scenarios leading up to the test trajectory.
It works!
####I got this validation on the C++ simulator:

#####Scenario 6

Simulation #1543 (../config/06_SensorNoise.txt)
PASS: ABS(Quad.GPS.X-Quad.Pos.X) was less than MeasuredStdDev_GPSPosXY for 71% of the time
PASS: ABS(Quad.IMU.AX-0.000000) was less than MeasuredStdDev_AccelXY for 68% of the time


#####Scenario 7

Simulation #2333 (../config/07_AttitudeEstimation.txt)
PASS: ABS(Quad.Est.E.MaxEuler) was less than 0.100000 for at least 3.000000 seconds


#####Scenario 8

It follow the path


#####Scenario 9

It follows the path but very slow


#####Scenario 10

Simulation #3777 (../config/10_MagUpdate.txt)
FAIL: ABS(Quad.Est.E.Yaw) was less than 0.120000 for 0.000000 seconds, which was less than 10.000000 seconds
FAIL: ABS(Quad.Est.E.Yaw-0.000000) was less than Quad.Est.S.Yaw for 27% of the time


#####Scenario 11
Simulation #3782 (../config/11_GPSUpdate.txt)
FAIL: ABS(Quad.Est.E.Pos) was less than 1.000000 for 0.000000 seconds, which was less than 20.000000 seconds
