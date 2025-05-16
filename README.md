
# 🏋️‍♂️ FitFreak – Exercise Form Classification Using Pose Landmarks

This project is designed to classify common fitness exercises using pose landmarks extracted from video frames. It leverages **MediaPipe** for landmark detection and prepares data suitable for deep learning models like LSTM or CNN.

---

## 📌 Project Summary

The goal is to build a pipeline that:
1. Extracts pose landmarks from videos using MediaPipe.
2. Stores landmark sequences in `.csv` format.
3. Loads and preprocesses this data into padded sequences for training.
4. Supports multi-class classification to identify different exercises.

---

## 🗂️ Project Structure

```
fitfreak/
├── data/
│   ├── 5exercise/             # Training video folders (per exercise)
│   ├── 5exertest/             # Test video folders (per exercise)
│   ├── landmarks/             # Output: CSV files with landmarks from training videos
│   └── test_landmarks/        # Output: CSV files with landmarks from test videos
├── extracting_landmarks.py    # Extracts landmarks from training videos
├── test_landmark extraction.py# Extracts landmarks from test videos
├── [*.py scripts]             # CSV processing/classification-related scripts
└── README.md                  # Project documentation
```

---

## ⚙️ How It Works

### ✅ `extracting_landmarks.py`  
- Extracts pose landmarks from videos in `data/5exercise`.
- Saves them as `.csv` files in `data/landmarks`.
- Each row in the CSV corresponds to a frame and contains 33 keypoints × 4 attributes (x, y, z, visibility).
  
### ✅ `test_landmark extraction.py`
- Does the same as above but for test videos in `data/5exertest`, saving output to `data/test_landmarks`.

### ✅ `landmark_loader_and_padding.py` *(assumed logic from your original message)*  
- Loads `.csv` files from the landmark folders.
- Skips the frame index column.
- Pads sequences to ensure equal length across samples.
- One-hot encodes exercise labels for model training.

---

## 🧠 Supported Exercises

Each exercise is assigned a unique numeric label:
- `0` – Barbell Row  
- `1` – Dumbbell Biceps Curl  
- `2` – Dumbbell Overhead Shoulder Press  
- `3` – Pushups  
- `4` – Side Lateral Raise

---

## 📦 Requirements

Install required libraries:
```bash
pip install mediapipe opencv-python pandas tensorflow
```

---

## 🚀 Usage Guide

### 1. Extract Landmarks from Videos
```bash
python extracting_landmarks.py
python test_landmark\ extraction.py
```

### 2. Preprocess and Prepare Data
Use a script to load the `.csv` files, pad sequences, and encode labels.  
Example (based on your original logic):
```python
X, y = load_data("data/landmarks")
X_padded = pad_sequences(X, padding="post", dtype="float32")
y_encoded = to_categorical(y, num_classes=5)
```

### 3. Train Your Model
You can now feed `X_padded` and `y_encoded` to a deep learning model (e.g., LSTM, GRU, or CNN).




# 🏋️‍♂️ Exercise Form Correction Modules – Code Overview

This document explains the purpose and workings of the three key Python scripts in this project, which implement **live form correction** using pose estimation for different exercises.

---

## 📘 1. `bicur_offc1.py` – Bicep Curl Form Correction

### 🔧 Functionality:
- Uses **MediaPipe** for real-time pose detection from webcam.
- Loads **reference landmark CSVs** to define correct form.
- Tracks reps, analyzes form (elbow position, shoulder elevation, wrist alignment).
- Computes:
  - **Rep Accuracy**
  - **Consistency**
  - **Tempo Score**
  - **Motion Smoothness**
- Provides **real-time visual feedback** and guidance.
- Draws bounding box around tracked person to focus analysis.

### ✅ Improvements in this version:
- Handles multiple people but tracks one main subject.
- Uses **priority-based feedback** and dynamic error weighting.
- Introduces **stability counters** to prevent flickering rep states.
- Adds **perfect rep detection** and feedback queues.

---

## 📘 2. `lateral_raiseoffc2.py` – Side Lateral Raise Form Correction

### 🔧 Functionality:
- Focuses on **side lateral raise** movement using pose landmarks.
- Monitors arm extension, balance, wrist alignment, and elbow bend.
- Computes:
  - **Range of Motion (ROM)**
  - **Accuracy per Rep**
  - **Tempo Score**
  - **Consistency Score**
- Draws the pose and bounding box using OpenCV.
- Saves per-frame landmark data to a CSV.

### ✅ Key Highlights:
- More lenient thresholds to reduce false errors.
- Tracks **good form streaks** to reward consistency.
- Smooth motion tracking to penalize jerky movements.
- Uses **form feedback priority** to show the most relevant suggestions.

---

## 📘 3. `overhead2.py` – Overhead Shoulder Press Form Correction

### 🔧 Functionality:
- Designed for **overhead dumbbell/barbell shoulder press**.
- Loads **reference CSVs** and separates them into "up" and "down" position templates.
- Tracks:
  - **Joint angles (elbow/shoulder/hip)**
  - **Exercise state transitions (up/down)**
  - **Reps and form errors**
- Provides real-time **feedback** and overlays accuracy and rep counts.

### ✅ Key Features:
- Accurate **angle-based rep detection**.
- Error tracking includes:
  - Incomplete extension
  - Raised shoulders
  - Back arching
  - Reference mismatch
- Feedback shows suggestions and average accuracy scores.
- Uses bounding box and visibility thresholding to isolate the main subject.

---

## 🚀 What Can Be Improved

- [ ] Add sound or vibration cues for feedback.
- [ ] Implement **smoother visual overlays** using a GUI framework (e.g., Tkinter, PyQt).
- [ ] Integrate with a mobile app or stream to cloud dashboard.
- [ ] Use **machine learning models** to learn correct vs. incorrect patterns instead of rule-based logic.
- [ ] Expand feedback to include suggestions for progression or weight.

---

Each of these scripts brings **intelligent real-time coaching** into fitness tracking. With MediaPipe's efficiency and a structured feedback system, these modules are ideal for AI-powered personal training applications.



## ✍️ Author

**FitFreak Project** – AI-powered exercise classification for smarter workout feedback.
