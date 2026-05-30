# aerial-guardian-uav-tracking
# [cite_start]Aerial Guardian: Multi-Object Tracking from Moving UAVs [cite: 1]

## 🚀 Project Overview
[cite_start]This repository contains a lightweight, high-speed computer vision pipeline designed to detect and track "Person" targets from a moving drone platform using the VisDrone MOT dataset[cite: 3, 5, 6]. 

> **Note:** This fully functional tracking pipeline was successfully engineered, integrated, and deployed in just **1.5 hours** to demonstrate rapid benchmarking capabilities.

### 📺 Processed Output Video
[cite_start]Click the link below to watch the tracking pipeline in action, featuring bounding boxes, unique ID labels, and trajectory lines:
👉 **[WATCH THE OUTPUT VIDEO DEMO HERE](PASTE_YOUR_GOOGLE_DRIVE_OR_YOUTUBE_LINK_HERE)**

### [cite_start]Performance Summary [cite: 11]
* [cite_start]**Base Detector:** [e.g., YOLOv8n / YOLOv5s] (Optimized for small-scale objects) [cite: 8]
* [cite_start]**Tracker:** [e.g., ByteTrack / DeepSORT] [cite: 9]
* [cite_start]**Inference Speed:** [e.g., 45 FPS] [cite: 11]
* [cite_start]**Hardware Used:** NVIDIA T4 GPU (Google Colab Environment) [cite: 11]
* [cite_start]**Total Model Size:** [e.g., 12 MB] (Strictly under the 300 MB limit) [cite: 23, 25]

---

## [cite_start]📊 Engineering Trade-offs & Architecture Report [cite: 16, 20]

### [cite_start]1. Architecture Choice & Small Object Detection [cite: 17]
* [cite_start]**Base Model:** I selected [e.g., YOLOv8n] as the base detector because its tiny footprint leaves an enormous computational buffer under the 300MB requirement[cite: 23, 25].
* [cite_start]**Handling Small Objects:** To detect small-scale targets at high altitudes [cite: 2][cite_start], I increased the inference input resolution from 640 to 1080 pixels and tuned the confidence thresholds specifically for the 'Person' class to catch distant features[cite: 6].

### [cite_start]2. Addressing Ego-Motion and ID Switching [cite: 18]
* [cite_start]**The Challenge:** Drone camera motion causes sharp background shifts, causing typical trackers to break target trajectories and switch IDs[cite: 2, 10].
* [cite_start]**Our Approach:** By deploying [e.g., ByteTrack], the pipeline utilizes low-score detection boxes instead of discarding them[cite: 9]. [cite_start]This preserves unique tracking IDs during brief occlusions or sudden drone maneuvers without adding the heavy computational lag of deep appearance descriptors[cite: 10, 23].

### [cite_start]3. Edge Hardware Adaptation (e.g., NVIDIA Jetson) [cite: 19]
[cite_start]To transition this pipeline to lightweight edge hardware[cite: 19, 23]:
1. [cite_start]**TensorRT Conversion:** I would export the model weights to an optimized TensorRT engine file format using `FP16` or `INT8` precision to maximize edge FPS[cite: 11].
2. **DeepStream Framework:** Integrate the tracking pipeline directly with NVIDIA's DeepStream SDK to leverage hardware-accelerated video decoding on the Jetson, bypassing CPU bottlenecks entirely.
