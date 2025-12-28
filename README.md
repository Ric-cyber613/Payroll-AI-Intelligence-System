# Payroll AI Intelligence System

A comprehensive employee attendance and payroll management system powered by AI-driven facial recognition. This application automates attendance tracking using an IP camera or webcam and calculates payroll based on attendance data.

## Features

-   **AI Facial Recognition Attendance**: Automatically marks attendance (Time In/Time Out) when an employee's face is recognized.
-   **Automated Payroll Calculation**: Generates payroll reports including basic salary, late deductions, and overtime bonuses.
-   **Web Dashboard**: A Flask-based web interface to manage staff, view attendance logs, and generate payrolls.
-   **Staff Management**: Add and manage employee details, shift timings, and departmental info.
-   **IP Camera Support**: connect to an IP camera (via RTSP) or use a local webcam for monitoring.
-   **System Logging**: Detailed logs of system events, errors, and activities.

## Tech Stack

-   **Backend**: Python, Flask
-   **Computer Vision**: OpenCV, Face Recognition (dlib)
-   **Database**: SQLite
-   **Frontend**: HTML, CSS, Jinja2

## Prerequisites

-   Python 3.8+
-   CMake (required for compiling `dlib`)
-   Visual Studio Build Tools (C++ CMake tools for Windows if installing `dlib` from source)

## Installation

1.  **Clone the repository** (if applicable) or navigate to the project directory.

2.  **Install Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```
    *Note: Installing `dlib` and `face-recognition` on Windows might require CMake and C++ build tools installed. If you face issues, try installing a pre-built `.whl` for dlib.*

3.  **Database Setup**:
    The application automatically initializes the SQLite database (`payroll.db`) on first run if it doesn't exist.

## Usage

1.  **Start the Application**:
    Run the main entry script which starts both the camera capture thread and the Flask web server.
    ```bash
    python run.py
    ```
    The application will act as the server `http://localhost:5001`.

2.  **Access the Dashboard**:
    Open your browser and navigate to `http://localhost:5001`.

3.  **Add Staff**:
    -   Go to the **Staff** section.
    -   Add new employee details.
    -   **Important**: You need to upload a face image for the employee for the recognition system to work.

4.  **Mark Attendance**:
    -   Ensure the camera is running.
    -   When an employee walks in front of the camera, their attendance is logged automatically.
    -   Late minutes are calculated based on their shift start time.

5.  **Generate Payroll**:
    -   Go to the **Payroll** section.
    -   Select the month and generate payroll. The system calculates net salary after deductions and bonuses.

## Project Structure

-   `app.py`: Main Flask application handling routes and API endpoints.
-   `run.py`: Entry point to start the app and camera threads.
-   `camera.py`: Handles video capture and frame processing.
-   `facial_recognition.py`: Core logic for face detection and encoding using `face_recognition` library.
-   `database.py`: Database connection and logging utilities.
-   `templates/`: HTML templates for the web interface.
-   `payroll.db`: SQLite database storing staff, attendance, and payroll data.

## Configuration

-   **Camera URL**: Update `camera_url` in `camera.py` (line 12) or instantiate `IPCameraSystem` with an RTSP URL (e.g., `rtsp://user:pass@ip:port/stream`) in `app.py`. Default is `0` for local webcam.
