Vehicle and Motorcycle Detection on Jetson Nano
This repository contains the necessary code and resources to execute a vehicle and motorcycle detection model on a Jetson Nano. The project uses a trained PHT model to perform real-time inference using the Jetson Nano's processing capabilities, leveraging OpenCV to display the detection results.

Table of Contents
Overview
Installation
Usage
Model Information
Converting Models to ONNX
Running Inference
Docker Setup
Acknowledgments
Overview
This project focuses on detecting front and back views of vehicles and motorcycles using a deep learning model trained for Jetson Nano. The repository includes:

Pre-trained models (PHT format) with different numbers of epochs.
Code for real-time detection using OpenCV (cv2).
Instructions for converting PHT models to ONNX for optimized inference on Jetson Nano.
We use the model trained with 14 epochs for inference, as it provides the best balance between performance and accuracy.

Installation
Clone this repository:

bash
Copiar código
git clone https://github.com/AlejoVargasO/programacion.git
cd programacion
Install the required Python packages:

bash
Copiar código
pip install -r requirements.txt
Ensure that you have Docker installed and set up on your Jetson Nano.

Usage
Running the Detection Model
The code is configured to run the model and display the bounding boxes on a video stream using OpenCV.

The default model used for inference is the one trained with 14 epochs. You can modify the code to use a different model if needed.

To run the detection script:

bash
Copiar código
python detect.py
The script will load the ONNX model and start detecting vehicles and motorcycles in the video feed, showing bounding boxes around detected objects.

Model Information
The repository includes several trained models in PHT format. Each model was trained for a different number of epochs:

3 epochs: Basic training, low accuracy.
48 epochs: Higher accuracy but slower performance on Jetson Nano.
18 epochs: A balance between training time and accuracy.
14 epochs: The most efficient model, used for real-time inference.
We recommend using the 14-epoch model for Jetson Nano due to its efficiency.

Converting Models to ONNX
To improve inference speed on Jetson Nano, the PHT models must be converted to ONNX format. This process is handled within a Docker container on Jetson Nano.

Pull the Docker image:

bash
Copiar código
docker pull <your-docker-image>
Run the Docker container:

bash
Copiar código
docker run -it --runtime nvidia <your-docker-image>
Convert the PHT model to ONNX inside the Docker container:

bash
Copiar código
python convert_to_onnx.py --model_path models/model_14_epochs.pth --output_path models/model_14_epochs.onnx
Running Inference
After converting the PHT model to ONNX, you can run the inference:

Execute the ONNX model on Jetson Nano:

bash
Copiar código
python run_inference.py --model models/model_14_epochs.onnx
The script will open a video feed and show real-time detection results, displaying bounding boxes around detected vehicles and motorcycles.

Docker Setup
Make sure Docker is installed and configured on your Jetson Nano. The Docker setup is essential for handling model conversion and optimizing inference performance.

For more details on Docker installation and configuration, visit the NVIDIA Docker documentation.

Acknowledgments
Special thanks to the open-source community and NVIDIA for providing tools and libraries to support deep learning on Jetson Nano.

This README outlines the essential steps and documentation needed to help users understand how to set up and run your vehicle detection model on Jetson Nano. You can modify any specific sections to better fit your project structure.
