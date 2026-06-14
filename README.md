# 🔐 Biometric Authentication System

A comprehensive Python-based biometric authentication system combining **facial recognition** and **hand gesture recognition** for secure multi-factor authentication. The system includes attendance logging, user registration, and real-time verification capabilities.

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![OpenCV](https://img.shields.io/badge/OpenCV-4.0+-green.svg)
![MediaPipe](https://img.shields.io/badge/MediaPipe-Latest-orange.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)


## 📋 Table of Contents

- [Features](#features)
- [System Architecture](#system-architecture)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Usage](#usage)
- [Modules](#modules)
- [How It Works](#how-it-works)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

### 🎭 Facial Recognition
- **Real-time Face Detection**: Live camera feed for face recognition
- **Multi-User Support**: Recognize multiple registered users
- **Face Encoding**: Uses 128-dimensional face embeddings
- **Unknown Face Detection**: Identifies unregistered individuals

### ✋ Hand Gesture Recognition
- **MediaPipe Integration**: Advanced hand landmark detection
- **3D Landmark Tracking**: 21 hand landmarks with x, y, z coordinates
- **Gesture Matching**: Similarity-based gesture verification
- **Real-time Comparison**: Live gesture matching with 50%+ accuracy threshold

### 📊 Attendance System
- **Automated Logging**: Automatic attendance recording upon face recognition
- **Daily Excel Reports**: Generates date-stamped Excel files
- **Duplicate Prevention**: 1-hour cooldown between log entries
- **Timestamp Recording**: Logs date and time of each attendance

### 🔒 Security Features
- **Multi-Factor Authentication**: Combines face + gesture recognition
- **Registration System**: Secure user and gesture enrollment
- **Similarity Threshold**: Configurable matching accuracy (default: 50%)
- **Time-based Access Control**: Prevents duplicate entries within 1 hour

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   User Interface                         │
│            (Sign In / Register Options)                  │
└────────────────────┬────────────────────────────────────┘
                     │
        ┌────────────┴────────────┐
        │                         │
        ▼                         ▼
┌───────────────┐         ┌──────────────┐
│ Face Recognition│       │Hand Gesture   │
│    Module      │       │Recognition    │
└───────┬───────┘         └──────┬───────┘
        │                         │
        │   ┌─────────────────┐   │
        └───►  Verification   ◄───┘
            │    Engine      │
            └────────┬───────┘
                     │
        ┌────────────┴────────────┐
        ▼                         ▼
┌───────────────┐         ┌──────────────┐
│  Attendance   │         │  Excel       │
│   Logger      │────────►│  Reports     │
└───────────────┘         └──────────────┘
```

## 🛠️ Tech Stack

### Core Libraries
- **OpenCV** - Computer vision and camera interface
- **face_recognition** - Facial recognition (based on dlib)
- **MediaPipe** - Hand landmark detection
- **NumPy** - Numerical computing and array operations
- **openpyxl** - Excel file generation and manipulation

### Python Version
- Python 3.8 or higher

## 📦 Prerequisites

Before running this application, ensure you have:

- Python 3.8 or higher
- Webcam/camera device
- Windows/Linux/macOS operating system
- Minimum 4GB RAM (8GB recommended)
- pip (Python package manager)

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone 
cd biometric-authentication
```

### 2. Create Virtual Environment

```bash
python -m venv venv

# Activate on Windows
venv\Scripts\activate

# Activate on macOS/Linux
source venv/bin/activate
```

### 3. Install Dependencies

```bash
# Install core libraries
pip install opencv-python
pip install face-recognition
pip install mediapipe
pip install numpy
pip install openpyxl

# For face_recognition dependencies (if needed)
pip install cmake
pip install dlib
```

Or use requirements.txt:

```bash
pip install -r requirements.txt
```

### 4. Set Up Directory Structure

Create the following directories:

```bash
mkdir pics          # For storing face images
mkdir hg            # For storing hand gesture data
```

### 5. Update File Paths

Update the folder paths in the code to match your system:

**In main authentication script:**
```python
folder_path = r"path/to/your/pics"
gesture_folder_path = r"path/to/your/hg"
```

**In attendance script:**
```python
folder_path = r"path/to/your/pics"
```

### 6. Register Users

**For Face Recognition:**
- Place user photos in the `pics` folder
- Name format: `/images/FaceRecognition.jpg` or `username.png`
- Ensure clear, front-facing photos

**For Gesture Recognition:**
- Run the registration option
- Provide an image with your hand gesture
- Save with a unique name

## 📁 Project Structure

```
biometric-authentication/
├── main_auth.py                # Main authentication system
├── attendance_logger.py        # Attendance tracking system
├── gesture_recognition.py      # Standalone gesture recognition
├── pics/                       # Face images directory
│   ├── /images/Attendance.jpg
│   ├── /images/photo1762422918.jpg
│   └── ...
├── hg/                         # Hand gesture data directory
│   ├── gesture1.npy
│   ├── gesture2.npy
│   └── ...
├── attendance_YYYY-MM-DD.xlsx  # Daily attendance logs
├── requirements.txt            # Python dependencies
├── README.md                   # This file
└── .gitignore
```

## 📖 Usage

### Module 1: Main Authentication System

This module combines face and gesture recognition for secure sign-in.

**Run the script:**
```bash
python main_auth.py
```

**Options:**

1. **Sign In (Option 1)**
   - System activates camera for face recognition
   - Upon face match, prompts for gesture verification
   - Enter registered gesture file name
   - Show gesture to camera for verification
   - Access granted if both match

2. **Register (Option 2)**
   - Provide path to hand gesture image
   - Enter a unique name for the gesture
   - Gesture saved as `.npy` file in `hg` folder

**Example Workflow:**
```
Choose an option (1: Sign In, 2: Register): 1

[Camera activates for face recognition]
Face detected: john_doe

Enter the name of the registered gesture file: gesture1
Show your hand gesture in front of the camera...

Gesture matched with 87.50% similarity
Authentication successful!
```

### Module 2: Attendance Logger

Automatically logs attendance when faces are recognized.

**Run the script:**
```bash
python attendance_logger.py
```

**Features:**
- Creates daily Excel file: `attendance_YYYY-MM-DD.xlsx`
- Logs name, date, and time
- Prevents duplicate entries within 1 hour
- Press 'q' to quit

**Excel Output Example:**

| Name | Date | Time |
|------|------|------|
| john_doe | 2024-01-15 | 09:30:45 |
| jane_smith | 2024-01-15 | 09:35:12 |
| john_doe | 2024-01-15 | 10:45:30 |

### Module 3: Standalone Gesture Recognition

Test hand gesture recognition independently.

**Run the script:**
```bash
python gesture_recognition.py
```

**Usage:**
```
Enter the path to the image file with your hand gesture: /images/GestureRecognition.jpg
Camera will now start. Show your hand gesture.

[Camera activates]
Show your hand gesture in front of the camera. Capturing for 10 seconds...

Gesture matched with 92.30% similarity
```

## 🔧 Modules

### 1. Face Recognition Module

**Functions:**

- `load_known_faces(folder_path)`: Loads face encodings from image files
  - Reads all `.jpg` and `.png` files
  - Generates 128-D face encodings
  - Extracts names from filenames

- `recognize_faces(known_face_encodings, known_face_names)`: Real-time face recognition
  - Opens webcam feed
  - Detects faces in each frame
  - Compares with known encodings
  - Displays name on video feed

**How Face Recognition Works:**

1. **Face Detection**: Locates faces in the image
2. **Face Encoding**: Converts face to 128-dimensional vector
3. **Comparison**: Calculates distance between encodings
4. **Matching**: Identifies closest match if within threshold

### 2. Hand Gesture Recognition Module

**Functions:**

- `extract_hand_landmarks(image)`: Extracts 21 hand landmarks
  - Converts image to RGB
  - Processes with MediaPipe
  - Returns 3D coordinates (x, y, z)

- `calculate_similarity(landmarks1, landmarks2)`: Computes gesture similarity
  - Calculates Euclidean distance
  - Normalizes to 0-1 range
  - Returns similarity percentage

- `process_image(image_path)`: Processes static gesture image
  - Loads image from file
  - Extracts hand landmarks
  - Returns landmark array

- `recognize_gesture(static_landmarks)`: Real-time gesture matching
  - Captures live camera feed
  - Compares with registered gesture
  - Matches if similarity ≥ 50%

**Hand Landmarks (21 points):**
```
0: Wrist
1-4: Thumb (CMC, MCP, IP, Tip)
5-8: Index finger (MCP, PIP, DIP, Tip)
9-12: Middle finger (MCP, PIP, DIP, Tip)
13-16: Ring finger (MCP, PIP, DIP, Tip)
17-20: Pinky (MCP, PIP, DIP, Tip)
```

### 3. Attendance Logger Module

**Functions:**

- `create_daily_excel_file()`: Creates/loads daily Excel file
  - Generates filename with current date
  - Creates file if doesn't exist
  - Adds headers (Name, Date, Time)

- `recognize_faces_and_log()`: Face recognition + attendance logging
  - Recognizes faces in real-time
  - Logs attendance to Excel
  - Prevents duplicate entries (1-hour cooldown)

**Attendance Logic:**

1. Face detected → Name identified
2. Check last log time for this person
3. If > 1 hour since last log → Record attendance
4. If < 1 hour → Skip (prevent duplicates)

## ⚙️ Configuration

### Adjusting Detection Confidence

**Face Recognition:**
```python
# In face_recognition library (default settings)
tolerance = 0.6  # Lower = stricter matching (0.0 - 1.0)
```

**Hand Gesture Recognition:**
```python
# In MediaPipe initialization
hands = mpHands.Hands(
    static_image_mode=True,
    max_num_hands=1,
    min_detection_confidence=0.7  # Increase for stricter detection
)
```

### Adjusting Similarity Threshold

```python
# In recognize_gesture function
if similarity_percentage >= 50:  # Change this value (0-100)
    # Gesture matched
```

**Recommended Values:**
- **50-60%**: Lenient (easier to match)
- **70-80%**: Moderate (balanced)
- **85-95%**: Strict (very precise matching)

### Adjusting Attendance Cooldown

```python
# In recognize_faces_and_log function
if name not in last_log_time or now - last_log_time[name] > timedelta(hours=1):
    # Change hours=1 to desired cooldown period
```

### Camera Settings

```python
# Change camera index if multiple cameras
video_capture = cv2.VideoCapture(0)  # 0 = default, 1 = second camera, etc.
```

## 🎯 How It Works

### Face Recognition Process

1. **Enrollment Phase:**
   - User photo placed in `pics` folder
   - Face detected and encoded (128-D vector)
   - Encoding stored with username

2. **Recognition Phase:**
   - Camera captures live video
   - Each frame processed for faces
   - Face encodings compared with known faces
   - Best match displayed (if within threshold)

**Mathematical Approach:**
```
Face Encoding: f(face) → R^128
Distance: d(f1, f2) = ||f1 - f2||
Match: d < threshold (typically 0.6)
```

### Hand Gesture Recognition Process

1. **Enrollment Phase:**
   - Static gesture image provided
   - MediaPipe extracts 21 landmarks (x, y, z)
   - Landmarks saved as NumPy array

2. **Recognition Phase:**
   - Live camera feed captures hand
   - Landmarks extracted in real-time
   - Euclidean distance calculated
   - Similarity = 1 - (distance / max_distance)

**Mathematical Approach:**
```
Landmarks: L = [(x₁, y₁, z₁), (x₂, y₂, z₂), ..., (x₂₁, y₂₁, z₂₁)]
Distance: d = √(Σ(L₁ᵢ - L₂ᵢ)²)
Similarity: s = 1 - (d / d_max)
Match: s ≥ 0.5 (50%)
```

### Attendance Logging Process

1. **Face Detection:**
   - Camera feed analyzed continuously
   - Faces detected and recognized

2. **Time Check:**
   - Current time compared with last log time
   - If > 1 hour → Proceed to log

3. **Excel Logging:**
   - Open/create daily Excel file
   - Append new row: [Name, Date, Time]
   - Save and close file

4. **Cooldown Update:**
   - Update last log time for user
   - Prevent duplicate entries

## 🐛 Troubleshooting

### Common Issues and Solutions

#### 1. Camera Not Opening

**Error**: `Error: Could not open webcam`

**Solutions:**
- Check camera permissions
- Try different camera index: `cv2.VideoCapture(1)`
- Ensure no other application is using the camera
- Restart the application

#### 2. Face Not Detected

**Error**: No face detected or "Unknown" displayed

**Solutions:**
- Ensure good lighting conditions
- Face the camera directly
- Remove glasses or accessories (if applicable)
- Use high-quality reference images
- Adjust `tolerance` parameter (increase for lenient matching)

#### 3. Hand Gesture Not Recognized

**Error**: "No hand gesture detected in the image"

**Solutions:**
- Ensure hand is clearly visible
- Use plain background
- Proper lighting
- Hand should be within camera frame
- Increase `min_detection_confidence` if too many false positives

#### 4. Low Similarity Score

**Error**: Gesture similarity < 50%

**Solutions:**
- Replicate exact hand position from registration
- Ensure same hand orientation
- Maintain consistent distance from camera
- Lower similarity threshold (if acceptable)

#### 5. Module Import Errors

**Error**: `ModuleNotFoundError: No module named 'face_recognition'`

**Solutions:**
```bash
# Install missing dependencies
pip install face-recognition
pip install cmake dlib  # Required for face_recognition

# For MediaPipe
pip install mediapipe

# For OpenCV
pip install opencv-python
```

#### 6. Excel File Permission Error

**Error**: `PermissionError: [Errno 13] Permission denied`

**Solutions:**
- Close Excel file if open
- Check file permissions
- Run with administrator privileges
- Change file save location

#### 7. Path Not Found

**Error**: `FileNotFoundError: [Errno 2] No such file or directory`

**Solutions:**
- Verify folder paths exist
- Use absolute paths (e.g., `r"C:\Users\...\pics"`)
- Create missing directories
- Check for typos in path names

## 🔒 Security Considerations

### Best Practices

1. **Face Image Storage:**
   - Store face images securely
   - Use encrypted storage for sensitive data
   - Implement access controls

2. **Gesture Data:**
   - Encrypt `.npy` gesture files
   - Store in secure directory
   - Implement file integrity checks

3. **Attendance Logs:**
   - Restrict Excel file access
   - Implement audit trails
   - Regular backups

4. **Camera Access:**
   - Request user permission
   - Indicator when camera is active
   - Secure camera feed transmission

5. **Threshold Tuning:**
   - Balance security vs usability
   - Higher thresholds = more secure
   - Lower thresholds = easier access

### Privacy Recommendations

- Inform users about biometric data collection
- Obtain explicit consent
- Provide data deletion options
- Comply with GDPR/local privacy laws
- Implement data retention policies

## 🚀 Deployment

### Running as a Service (Windows)

Create a batch file `start_attendance.bat`:
```batch
@echo off
cd /d "C:\path\to\project"
call venv\Scripts\activate
python attendance_logger.py
pause
```

### Running as a Service (Linux)

Create a systemd service file:
```ini
[Unit]
Description=Biometric Attendance System
After=network.target

[Service]
Type=simple
User=your_username
WorkingDirectory=/path/to/project
ExecStart=/path/to/venv/bin/python attendance_logger.py
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

### Scheduling with Task Scheduler (Windows)

1. Open Task Scheduler
2. Create Basic Task
3. Set trigger (e.g., At startup)
4. Action: Start a program
5. Program: `python.exe`
6. Arguments: `attendance_logger.py`
7. Start in: Project directory

## 📊 Performance Optimization

### Tips for Better Performance

1. **Reduce Frame Size:**
```python
small_frame = cv2.resize(frame, (0, 0), fx=0.25, fy=0.25)
```

2. **Skip Frames:**
```python
frame_count = 0
if frame_count % 3 == 0:  # Process every 3rd frame
    # Face recognition code
frame_count += 1
```

3. **Use GPU Acceleration:**
```python
# For dlib (face_recognition)
# Compile with CUDA support
```

4. **Optimize MediaPipe:**
```python
hands = mpHands.Hands(
    static_image_mode=False,  # Faster for video
    max_num_hands=1,
    min_detection_confidence=0.5
)
```

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit your changes**
   ```bash
   git commit -m 'Add amazing feature'
   ```
4. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open a Pull Request**

### Contribution Ideas

- [ ] Add iris recognition
- [ ] Implement voice authentication
- [ ] Create web-based interface
- [ ] Add database support (MySQL/PostgreSQL)
- [ ] Mobile app integration
- [ ] Multi-language support
- [ ] Enhanced security features
- [ ] Cloud storage integration
- [ ] Real-time notifications

## 📝 Future Enhancements

- [ ] **Liveness Detection**: Prevent photo-based spoofing
- [ ] **Multi-Modal Fusion**: Combine face + gesture + voice
- [ ] **Deep Learning Models**: Use CNNs for improved accuracy
- [ ] **Cloud Integration**: Store data in cloud databases
- [ ] **Mobile App**: Android/iOS companion app
- [ ] **Dashboard**: Web-based admin panel
- [ ] **Analytics**: Attendance reports and statistics
- [ ] **API**: RESTful API for third-party integration
- [ ] **Notifications**: Email/SMS alerts for attendance
- [ ] **Access Control**: Integration with door locks

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [face_recognition](https://github.com/ageitgey/face_recognition) by Adam Geitgey
- [MediaPipe](https://mediapipe.dev/) by Google
- [OpenCV](https://opencv.org/) community
- [dlib](http://dlib.net/) by Davis King