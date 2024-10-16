# Position Estimation of Autonomous Vehicle using UKF in ESP32

This project implements position estimation of an autonomous vehicle using the **Unscented Kalman Filter (UKF)** on an **ESP32 microcontroller**. The system uses data from the **MPU6050 (IMU)** and the **NEO-6M (GPS)** modules to fuse sensor readings and provide accurate position estimation.

## Table of Contents
- [Introduction](#introduction)
- [Hardware Requirements](#hardware-requirements)
- [Software Requirements](#software-requirements)
- [Architecture](#architecture)
- [Working Principle](#working-principle)
- [Kalman Filter Implementation](#kalman-filter-implementation)
- [Setup and Usage](#setup-and-usage)
- [Results](#results)
- [Future Improvements](#future-improvements)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)

## Introduction
The goal of this project is to estimate the position of an autonomous vehicle using sensor fusion techniques with the Unscented Kalman Filter (UKF). The vehicle's position is tracked using GPS data, while the vehicle's movement is predicted based on IMU sensor data (acceleration and orientation). 

The UKF is used to improve the accuracy of the position estimates by combining the noisy measurements from both the GPS and IMU.

## Hardware Requirements
- **ESP32 Dev Module**
- **MPU6050** (IMU for accelerometer and gyroscope readings)
- **NEO-6M** (GPS module for latitude and longitude data)
- **OLED-Display** (OLED Display for displaying results)
- Breadboard, jumper wires, power supply, etc.
The following image shows the circuit connections between the ESP32, MPU6050, NEO-6M GPS module, and the OLED display:

![Screenshot 2024-06-18 163332](https://github.com/user-attachments/assets/2c8359f8-cf68-418c-abc5-d7814dd38d11)

## Software Requirements
- **Arduino IDE** (for programming ESP32)
- **ESP32 board libraries** (for Arduino IDE)
- **MPU6050 library** (for IMU interfacing)
- **TinyGPS++ library** (for GPS data parsing)
- **Adafruit-SSD1306** (for OLED Display)
- **UKF implementation in C++** (custom or open-source library)

## Architecture
The project is divided into the following key components:
1. **Sensor Data Acquisition**: Reading IMU and GPS data.
2. **Preprocessing**: Converting sensor data (e.g., Latitude/Longitude to ECEF).
3. **Prediction Step**: Using IMU data for vehicle motion prediction.
4. **Update Step**: Correcting the predicted position using GPS data.
5. **Position Estimation**: Outputting the final estimated position of the vehicle.
Below is a flowchart that represents the architecture of the system:


## Working Principle
The IMU (MPU6050) continuously measures acceleration and orientation of the vehicle. The NEO-6M GPS module provides absolute position data (latitude and longitude). 

The Unscented Kalman Filter (UKF) works as follows:
1. **Prediction**: Based on IMU data, the UKF predicts the vehicle's next position.
2. **Update**: The GPS data is used to update the prediction, refining the vehicle's current position.

This filtering technique minimizes the effect of sensor noise and provides smoother, more accurate position data.

## Kalman Filter Implementation
### Steps:
1. **State Vector**: The vehicle’s position, velocity, and orientation are estimated.
2. **Process Model**: IMU data is used for motion prediction.
3. **Measurement Model**: GPS data provides position updates.
4. **UKF Algorithm**: The algorithm predicts and corrects the state vector using sensor inputs.

Key features of the UKF include:
- Use of sigma points to handle non-linearity.
- Handling of both process and measurement noise.

## Setup and Usage
### Hardware Setup:
1. Connect the **NEO-6M** GPS module to the ESP32 using UART (TX, RX).
2. Connect the **MPU6050** IMU to the ESP32 via I2C (SCL, SDA).
3. Connect the **OLED-Display** IMU to the ESP32 via I2C (SCL, SDA).
4. Power both modules using the 3.3V or 5V pins from the ESP32.

### Software Setup:
1. Install the required libraries in Arduino IDE.
2. Clone this repository:  
3. Open the `main.ino` file in Arduino IDE.
4. Upload the code to the ESP32 board.
5. Open the Serial Monitor to see the real-time position estimates.

## Results
- The UKF-based position estimation outperforms raw GPS data in terms of accuracy and stability.
- IMU sensor fusion improves the continuity of position tracking even in areas with poor GPS signal.

### Example Output:
- **Raw GPS Data**: Latitude, Longitude (with noticeable noise)
- **Filtered Data**: Smooth position estimates with reduced noise

## Future Improvements
- Add magnetometer data for better orientation estimation.
- Implement altitude estimation using a barometer.
- Optimize the UKF parameters for higher accuracy.
- Expand to multiple sensor fusion for additional inputs like LIDAR or cameras.

## Contributing
Contributions are welcome! Please open an issue or submit a pull request.

## License
This project is licensed under the MIT License - see the `LICENSE` file for details.

## Acknowledgements
Special thanks to [Prof.Rohit Kalyani, Rohit Waddar, Anchal Aravind Patil, Sharath Patil, KLE Technological University] for their support and contributions to this project.

