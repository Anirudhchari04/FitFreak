
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



## ✍️ Author

**FitFreak Project** – AI-powered exercise classification for smarter workout feedback.
