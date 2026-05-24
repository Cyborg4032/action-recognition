🤟 Sign Language Action Recognition
A real-time sign language detection system using MediaPipe, LSTM deep learning, and OpenCV. This project recognizes hand gestures and sign language actions from live webcam input by extracting pose/hand/face keypoints and classifying sequences using a trained neural network.

📌 Overview
This project uses computer vision and sequence modeling to detect and classify sign language gestures in real time. It captures keypoint data from video frames using MediaPipe Holistic, trains an LSTM-based model on the collected sequences, and performs live inference via webcam.
The model achieves ~90% accuracy on the validation set.

🗂️ Repository Structure
action-recognition/
│
├── Action Detection.ipynb               # Main notebook: data collection, training & inference
├── Sign_recognition.ipynb               # Sign recognition variant (v1)
├── Sign_recognition_2.ipynb             # Sign recognition variant (v2)
│
├── MP_Data/                             # Collected MediaPipe keypoint sequences (.npy)
├── Logs/train/                          # TensorBoard training logs
│
├── action.h5                            # Trained Keras LSTM model weights
├── 0.npy                                # Sample keypoint array
├── 90%                                  # Model checkpoint at ~90% accuracy
│
├── create_ppt.py                        # Script to auto-generate the project presentation
└── Sign_Language_Detection_Presentation.pptx         # Project presentation slides
    Sign_Language_Detection_Technical_Documentation.docx  # Technical documentation

🧠 How It Works

Keypoint Extraction — MediaPipe Holistic detects face, pose, left-hand, and right-hand landmarks from each video frame.
Data Collection — For each action/sign, 30 video sequences of 30 frames each are captured and saved as .npy arrays in MP_Data/.
Model Training — A stacked LSTM network is trained on the sequences to learn temporal patterns in gestures.
Real-Time Inference — The trained model (action.h5) is loaded for live webcam detection with visual probability overlays.


🛠️ Tech Stack
ComponentLibrary / ToolKeypoint DetectionMediaPipe HolisticDeep LearningTensorFlow / KerasComputer VisionOpenCVData HandlingNumPyVisualizationMatplotlib, TensorBoardNotebookJupyter

⚙️ Installation
bash# Clone the repository
git clone https://github.com/Cyborg4032/action-recognition.git
cd action-recognition

# Install dependencies
pip install tensorflow opencv-python mediapipe numpy matplotlib scikit-learn

Python 3.8–3.10 is recommended for compatibility with TensorFlow and MediaPipe.


🚀 Usage
1. Collect Training Data
Open Action Detection.ipynb and run the Data Collection section. It will launch your webcam and record keypoint sequences for each defined action/sign.
2. Train the Model
Run the Model Training section in the notebook. Training logs are saved to Logs/train/ and can be viewed with TensorBoard:
bashtensorboard --logdir Logs/train
3. Run Real-Time Detection
Run the Real-Time Detection section. The webcam will open and the model will classify sign gestures live with on-screen probability bars.
4. Use a Pre-trained Model
The included action.h5 file is a pre-trained model ready for inference — skip straight to the detection section.

📊 Model Architecture
Input: (30 frames × 1662 keypoints)
    ↓
LSTM(64, return_sequences=True)
    ↓
LSTM(128, return_sequences=True)
    ↓
LSTM(64)
    ↓
Dense(64, relu) → Dense(32, relu)
    ↓
Dense(num_actions, softmax)

📁 Data Format
Each action is stored as:
MP_Data/
  └── <action_name>/
        └── <sequence_number>/
              └── 0.npy ... 29.npy   # one file per frame
Each .npy file contains the flattened MediaPipe keypoints for that frame (pose + face + hands = 1662 values).

📄 Documentation

Technical Documentation — detailed system design and methodology
Presentation Slides — project overview and results


🤝 Contributing
Pull requests are welcome! For significant changes, please open an issue first to discuss what you'd like to change.

📜 License
This project is open source. See LICENSE for details (if applicable).
