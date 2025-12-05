# Food Freshness Detection Using YOLOv8
### Deep Learning Model for Fresh vs Spoiled Tomato Classification

## Introduction
This project uses a YOLOv8 object detection model to classify tomatoes as **Fresh** or **Spoiled** using image input.  
The system includes a Flask backend, React frontend, custom dataset, augmentation pipeline, and real-time prediction capability.

---

## Features
- YOLOv8-Small model for fast and accurate classification  
- Real-time detection from image upload or live camera  
- Custom self-captured dataset  
- Augmentation for dataset balancing and robustness  
- Flask API for inference  
- React-based user interface  
- Model export: `.pt`, `.onnx`, `.tflite`  
- Deployable on laptops, cloud, and Raspberry Pi  

---

## Dataset
- **310 raw images** captured manually  
- **Approximately 762 images** after augmentation  
- Dataset split:
  - 87% Training (666 images)  
  - 8% Validation (63 images)  
  - 4% Testing (33 images)  
- Augmentation methods:
  - Rotation  
  - Horizontal flip  
  - Brightness and saturation adjustments  
  - Blur and Gaussian noise  
  - Shear and affine transforms  

---

## Model Training
- Model: **YOLOv8-Small**  
- Epochs: 100  
- Image size: 640×640  
- Batch size: 16  
- Optimizer: Adam (lr = 0.001)  
- Loss functions: CIoU, BCE, Distribution Focal Loss

### Performance Metrics
- Precision: **0.934**  
- Recall: **0.936**  
- mAP50: **0.984**  
- mAP50-95: **0.926**  
- Fitness score: **0.926**

---

## Workflow
1. User uploads an image or uses browser camera  
2. Frontend converts image to base64  
3. Flask backend decodes image and runs YOLOv8 inference  
4. Model predicts bounding boxes + class (Fresh/Spoiled) + confidence  
5. JSON response returned to frontend  
6. Frontend overlays bounding boxes on the image  
7. Sensor logger records prediction events for IoT integration  

---

## Project Structure

```text
food-freshness-detection/
├── README.md
├── .gitignore
├── requirements.txt
│
├── scripts/
│   └── download_weights.sh
│
├── src/
│   ├── backend/
│   │   ├── app.py
│   │   ├── predict.py
│   │   └── sensor_logger.py
│   │
│   └── preprocessing/
│       └── augment_spoilt.py
│
├── web/
│   ├── package.json
│   └── src/
│
├── notebooks/
│   └── DL_Food_Freshness_Model_Training.ipynb
│
└── models/
    └── (weights downloaded here)



## Setup Instructions

### 1. Create virtual environment
python -m venv venv
source venv/bin/activate # Linux/Mac
venv\Scripts\activate # Windows

### 2. Install backend dependencies
pip install -r requirements.txt

### 3. Download model weights
bash scripts/download_weights.sh

### 4. Run Flask backend
python src/backend/app.py

### 5. Run React frontend
cd web
npm install
npm start

---

## Future Scope
- Extend to more fruits, vegetables, and packaged food items  
- Mobile application for household use  
- Integration with IoT hardware sensors  
- Deployment in factories for automated quality checks  
- Multimodal AI combining vision + sensor data  

---

## License
Add a license such as MIT or Apache 2.0.
