## 📌 Overview

Accurate localization is a fundamental requirement for autonomous drones, especially in GPS-denied environments such as indoor spaces or urban canyons.

This project presents a sensor fusion framework that combines:

Ultra-Wideband (UWB) measurements for absolute positioning
Inertial Measurement Unit (IMU) data for motion estimation

These two sources are fused using an Extended Kalman Filter (EKF) to achieve robust and accurate 3D localization.

The system leverages the complementary strengths of both sensors:
IMU provides high-frequency motion data but suffers from drift
UWB provides absolute positioning but is noisy and delayed

The proposed fusion framework significantly improves localization accuracy and stability.

<table align="centre">
  <tr>
    <td><img src="images/Video.gif" width="400"/></td>
  </tr>
</table>
<br clear="left"/>

**🧠 Key Contributions**
Designed a complete UWB–IMU fusion pipeline for drone localization
Implemented TDOA-based UWB positioning
Developed an Extended Kalman Filter (EKF) for nonlinear sensor fusion
Processed and analyzed real sensor data (IMU + UWB)
Evaluated system performance through trajectory reconstruction and error analysis

🧮 **Methodology**
**1. IMU-Based Motion Estimation**

The IMU provides:

Linear acceleration
Angular velocity
Orientation (via integration)

Processing steps:

Coordinate transformation (body → inertial frame)
Gravity compensation
Numerical integration → velocity & position

⚠️ Issue: IMU accumulates drift over time

**2. UWB-Based Localization**

UWB positioning is performed using Time Difference of Arrival (TDOA):

Multiple ground anchors receive signals from the drone
Time differences are used to estimate relative distances
A linear system is solved to compute the drone’s position

Advantages:

High accuracy (centimeter-level)
Robust in indoor environments

Limitations:

Measurement noise
Susceptible to NLOS conditions
3. Sensor Fusion using EKF

To combine IMU and UWB data, an Extended Kalman Filter (EKF) is used.

State Vector
x = [position, velocity, orientation]
Prediction Step (IMU-driven)
x_k = f(x_{k-1}, u_k)
Update Step (UWB measurements)
z_k = h(x_k)

Key features:

Nonlinear system modeling
Linearization using Jacobians
Measurement validation using residuals
Rejection of unreliable UWB measurements

🔧 **Hardware Setup**

The system is implemented using the following components:

UWB Module: DWM1000
IMU Sensor: MPU9250 (9-DOF)
Microcontroller: STM32 (Cortex-M3)
Flight Controller: Pixhawk
Communication: Wi-Fi / USB interface
Ground Stations: Multiple UWB anchors

The drone communicates with ground stations to collect UWB signals, while onboard sensors provide IMU data.

**🧪 Experimental Pipeline**
Data acquisition (IMU + UWB)
Dataset extraction (e.g., bag files)
IMU preprocessing
UWB signal processing (TDOA)
EKF-based sensor fusion
Visualization and analysis (MATLAB / Python)
📊 Results

The system performance is evaluated using:

**📍 Trajectory reconstruction**
📉 Position error analysis (e.g., RMSE)
🔄 Comparison between:
IMU-only estimation (drift)
UWB-only estimation (noisy)
EKF fusion (stable and accurate)

Example outputs:

2D / 3D trajectory plots
Error vs time graphs

**🚀 Future Work**
Implementation of Unscented Kalman Filter (UKF)
Integration with Visual Odometry (VIO)
Real-time onboard deployment optimization
Robustness improvement under NLOS conditions

**📚 References**
Li et al., Accurate 3D Localization for MAV Swarms using UWB and IMU Fusion
UWB-based localization methodologies (TDOA, ToA)
Kalman Filtering and Nonlinear State Estimation
📌 Acknowledgment

This project is based on concepts from UWB localization research and extended with a full system-level implementation, including sensor fusion, hardware integration, and experimental evaluation.

👤 Author

Arash Rezaeinezhad
Research Assistant | Robotics & Deep Learning
