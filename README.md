# Crowd Detection and Tracking System

This project implements a real-time **people detection, tracking, and entry/exit counting system** using YOLOv5 and the SORT algorithm. It supports both webcam and video file inputs and includes a Streamlit dashboard for user-friendly interaction.

## 🚀 Features

- Real-time object detection using **YOLOv5**
- Identity-preserving object tracking via **SORT (Simple Online and Realtime Tracking)**
- **Entry/Exit counting** of people based on defined virtual boundaries
- **Live Streamlit dashboard** for video upload, webcam access, and system metrics
- Output video generation with bounding boxes, IDs, trails, and count overlays

## 🧠 Tech Stack

- YOLOv5 (PyTorch-based object detection)
- SORT (Kalman Filter + Hungarian Algorithm)
- OpenCV, NumPy, filterpy
- Streamlit for interactive dashboard
- psutil for system monitoring

## 📁 Project Structure

```
crowdDetection/
├── app.py                          # Streamlit dashboard
├── obj_det_and_trk.py             # Core detection and tracking logic
├── person_in_out_count.py         # Entry/exit counting logic
├── sort/                          # SORT tracking algorithm
├── models/, utils/, data/         # YOLOv5 modules
├── weights/                       # Pretrained YOLOv5 weights
├── requirements.txt               # Python dependencies
└── README.md                      # Project documentation
```

## 📦 Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/Marmik01/crowdDetection.git
   cd crowdDetection
   ```

2. **(Optional) Create a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate   # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Download YOLOv5 model weights**
   - Default: `yolov5n.pt`
   - You can use other variants (`yolov5s.pt`, `yolov5m.pt`, etc.) and place them in the `weights/` folder.
   - Download from: https://github.com/ultralytics/yolov5

## ▶️ Usage

### Option 1: Run with Streamlit (UI Dashboard)

```bash
streamlit run app.py
```

- Upload a video or select webcam
- Set detection threshold
- Enable/disable saving output
- Click **Start Tracking** to begin

### Option 2: Run with Counting via Script

```bash
python person_in_out_count.py --source path/to/video.mp4 --weights weights/yolov5n.pt --view-img --save-txt
```

### Common Arguments

- `--source`: Input source (`0` for webcam or path to video)
- `--weights`: Path to YOLO model weights
- `--conf-thres`: Confidence threshold (default: 0.25)
- `--view-img`: Show annotated video in real-time
- `--save-txt`: Save detection results to text files

## 📊 Entry/Exit Counting

- Uses a horizontal center line in the frame
- Counts a person as **entering** or **exiting** based on motion direction
- Results are overlaid on the video feed in real time

## 📌 Output

- Video with annotated bounding boxes, unique track IDs, and movement trails
- Entry and exit statistics overlaid on frames
- Optionally saved output video to disk
