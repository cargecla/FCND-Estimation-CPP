## Project: Building an Estimator
![Scenario1_Simulator](./Scenario1_Simulator.png)

---


## [Rubric](https://review.udacity.com/#!/rubrics/1807/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it! Below I describe how I addressed each rubric point and where in my code each point is handled.

### Implement Estimator

#### 1. Implemented estimator introduction


1) Step 1: Sensor Noise:

In this scenario it is required to use the simulator to generate GPS and IMU measurements.

[Step1_Simulator.mp4](./Step1_Simulator.mp4)


2) Step 2: Attitude Estimation:

In this scenario it is required to include IMU information into the state.


[Step2_Simulator.mp4](./Step2_Simulator.mp4)


3) Step 3: Prediction Step:

In this scenario it is required to use accelaration measurement to predict the estate. In addition, it is required to update the covariance matrix and complete the EKF state.


[Step3_Simulator.mp4](./Step3_Simulator.mp4)


Covariance prediction:
[Step3.1_Simulator.mp4](./Step3.1_Simulator.mp4)


4) Step 4: Magnetometer Update:

In this scenario it is required to use magnetometer measurement to predict the estate. 

[Step4_Simulator.mp4](./Step4_Simulator.mp4)


5)Step 5: Closed Loop + GPS Update:

In this scenario it is required to use GPS measurement to predict the estate. The drone follows the square trayectory.

[Step5_Simulator.mp4](./Step5_Simulator.mp4)


### Implemented Estimator
These scripts contain a basic estimator implementation that includes the following:

#### 1. Determine the standard deviation of the measurement noise of both GPS X data and Accelerometer X data.
The calculated standard deviation should correctly capture ~68% of the sensor measurements. Your writeup should describe the method used for determining the standard deviation given the simulated sensor measurements.

I transferred the data of files Graph1.txt and Graph2.txt located at the config/log folder into a spreadsheet and used the in-built formula to calculate the stadard deviations, results are below:

MeasuredStdDev_GPSPosXY = 0.71279695
MeasuredStdDev_AccelXY = 0.4905941014



#### 2. Implement a better rate gyro attitude integration scheme in the UpdateFromIMU() function.
The improved integration scheme should result in an attitude estimator of < 0.1 rad for each of the Euler angles for a duration of at least 3 seconds during the simulation. The integration scheme should use quaternions to improve performance over the current simple integration scheme.

On the QuadEstimatorEKF.cpp file, from line 104 to 112 an improved rate gyro attitude integration scheme was implemented.


#### 3. Implement all of the elements of the prediction step for the estimator.
The prediction step should include the state update element (PredictState() function), a correct calculation of the Rgb prime matrix, and a proper update of the state covariance. The acceleration should be accounted for as a command in the calculation of gPrime. The covariance update should follow the classic EKF update equation.

The prediction step for the estimator was implemented between line 176 and 184 (PredictState), line 212 and 226 (GetRbgPrime) and line 273 and 281 (Predict) of the of the QuadEstimatorEKF.cpp file.


#### 4. Implement the magnetometer update.
The update should properly include the magnetometer data into the state. Note that the solution should make sure to correctly measure the angle error between the current state and the magnetometer value (error should be the short way around, not the long way).

From line 334 to 345, the magnetometer update was implemented.


#### 5. Implement the GPS update.
The estimator should correctly incorporate the GPS information to update the current state estimate.

In order to include GPS information the lines of code from 307 to 311 were implmented. Refer to the QuadEstimatorEKF.cpp file.



### Flight Evaluation
#### 1. Meet the performance criteria of each step.

It works!

####I got this validation on the C++ simulator:

#####Step 1: Sensor Noise

Simulation #741 (../config/06_SensorNoise.txt)
PASS: ABS(Quad.GPS.X-Quad.Pos.X) was less than MeasuredStdDev_GPSPosXY for 71% of the time
PASS: ABS(Quad.IMU.AX-0.000000) was less than MeasuredStdDev_AccelXY for 68% of the time


#####Step 2: Attitude Estimation

Simulation #745 (../config/07_AttitudeEstimation.txt)
PASS: ABS(Quad.Est.E.MaxEuler) was less than 0.100000 for at least 3.000000 seconds


#####Step 3: Prediction Step

It follows the path. Refer to video: Step3_Simulator.mp4


#####Step 4: Magnetometer Update

Simulation #821 (../config/10_MagUpdate.txt)
PASS: ABS(Quad.Est.E.Yaw) was less than 0.120000 for at least 10.000000 seconds
PASS: ABS(Quad.Est.E.Yaw-0.000000) was less than Quad.Est.S.Yaw for 78% of the time


#####Step 5: Closed Loop + GPS Update

Simulation #823 (../config/11_GPSUpdate.txt)
PASS: ABS(Quad.Est.E.Pos) was less than 1.000000 for at least 20.000000 seconds


#### 2. De-tune your controller to successfully fly the final desired box trajectory with your estimator and realistic sensors.

#####Step 6: Adding Your Controller

Everything worked after tuning it. Videos can be seen above and attached.

