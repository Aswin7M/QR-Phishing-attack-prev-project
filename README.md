# QR Code Phishing Attack Detection Using Generative AI

An AI-powered cybersecurity project for detecting malicious and phishing QR codes using deep learning and computer vision.

The system classifies QR-code images into two categories:

* **Benign QR Code**
* **Malicious QR Code**

The project uses **Transfer Learning with EfficientNetB3** to learn visual patterns from QR-code images and classify them as benign or malicious.

---

## Project Overview

QR codes are widely used for payments, authentication, website access, and information sharing. However, attackers can use malicious QR codes to redirect users to phishing websites, fraudulent payment pages, malware downloads, or other malicious resources.

This project explores an AI-based approach for identifying potentially malicious QR codes from their visual characteristics.

The primary objective is to build a deep-learning-based image classification system capable of distinguishing between benign and malicious QR codes.

---

## Objectives

* Detect potentially malicious QR codes using AI.
* Classify QR-code images into benign and malicious categories.
* Apply computer vision preprocessing techniques.
* Use transfer learning to improve classification performance.
* Evaluate the model using standard classification metrics.
* Explore the use of Generative AI and deep learning techniques in cybersecurity.
* Build a foundation that can later be extended into a real-time QR security scanner.

---

## Approach

The project follows the following pipeline:

```text
QR Code Image
      |
      v
Image Loading
      |
      v
Image Preprocessing
      |
      +-- Resize
      +-- RGB Conversion
      +-- Normalization / Preprocessing
      |
      v
Data Augmentation
      |
      +-- Random Flip
      +-- Random Rotation
      +-- Random Zoom
      +-- Random Contrast
      +-- Random Translation
      |
      v
EfficientNetB3
(Transfer Learning)
      |
      v
Feature Extraction
      |
      v
Dense Layer
      |
      v
Softmax Classification
      |
      v
+---------------------+
| Benign / Malicious  |
+---------------------+
```

---

## Model Architecture

The project uses **EfficientNetB3** as the backbone model.

### Architecture

```text
Input Image
   |
   v
300 x 300 x 3
   |
   v
Data Augmentation
   |
   v
EfficientNetB3
(pretrained on ImageNet)
   |
   v
Global Average Pooling
   |
   v
Dropout (0.5)
   |
   v
Dense Layer (256)
ReLU Activation
   |
   v
Dropout (0.3)
   |
   v
Dense Layer (2)
Softmax Activation
   |
   v
Prediction
```

Initially, the pretrained EfficientNetB3 layers are frozen and used as a feature extractor.

---

## Dataset

The model expects a directory structure containing two classes:

```text
QR codes/
├── benign/
│   ├── image1.png
│   ├── image2.png
│   └── ...
│
└── malicious/
    ├── image1.png
    ├── image2.png
    └── ...
```

### Classes

| Label | Class     | Description                                                     |
| ----- | --------- | --------------------------------------------------------------- |
| `0`   | Benign    | Legitimate/non-malicious QR codes                               |
| `1`   | Malicious | QR codes associated with potentially malicious/phishing content |

The dataset is not included in the repository. Users should ensure that they have the appropriate rights to use any dataset added to the project.

---

## Technologies Used

### Programming Language

* Python

### Deep Learning

* TensorFlow
* Keras
* EfficientNetB3
* Transfer Learning

### Computer Vision

* OpenCV
* Pillow (PIL)

### Machine Learning

* Scikit-learn

### Data Processing

* NumPy
* Pandas

### Visualization

* Matplotlib

### Development Environment

* Google Colab
* Jupyter Notebook
* Python

---

## Installation

Clone the repository:

```bash
git clone https://github.com/<your-username>/Phishing-Attack-GenAI.git
cd Phishing-Attack-GenAI
```

Create a virtual environment:

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

Install the required packages:

```bash
pip install tensorflow numpy pandas matplotlib scikit-learn opencv-python pillow
```

These installation steps follow the environment and dependencies specified in the project reference.

---

## Running the Project

The current implementation was developed primarily for **Google Colab**.

### Option 1 — Google Colab

1. Open the Python or notebook file in Google Colab.
2. Upload the QR-code dataset.
3. Arrange the dataset into `benign` and `malicious` directories.
4. Update the dataset paths in the code.
5. Run the cells sequentially.
6. Train the EfficientNetB3-based classifier.
7. Evaluate the model using the generated metrics.

### Option 2 — Local Python Environment

The dataset paths in the original development code are environment-specific.

Update paths such as:

```python
benign_path = "/path/to/QR codes/benign"
malicious_path = "/path/to/QR codes/malicious"
```

to match the location of your dataset before execution.

---

## Data Preprocessing

Images are processed before being passed to the model.

The preprocessing pipeline includes:

* Loading image files.
* Converting images to RGB.
* Resizing images.
* Handling unreadable or corrupted images.
* Normalizing and preprocessing image values.
* Creating training and validation datasets.

The primary model configuration uses:

```text
Image Size: 300 x 300
Channels: 3
Batch Size: 32
Epochs: 30
Random Seed: 42
```

---

## Data Augmentation

To improve model generalization, the training pipeline applies image augmentation:

```text
Random Flip
Random Rotation
Random Zoom
Random Contrast
Random Translation
```

These techniques help the model learn robust visual representations rather than memorizing specific training images.

---

## Model Evaluation

The project supports several standard evaluation metrics:

* Accuracy
* Precision
* Recall
* F1-Score
* Confusion Matrix

Example:

```python
accuracy_score(y_true, y_pred)
precision_score(y_true, y_pred)
recall_score(y_true, y_pred)
f1_score(y_true, y_pred)
confusion_matrix(y_true, y_pred)
```

These metrics can be used to evaluate how effectively the model distinguishes malicious QR codes from benign QR codes.

---

## Why EfficientNetB3?

EfficientNetB3 is used as the feature-extraction backbone because it provides a balance between:

* Model capacity
* Computational efficiency
* Image classification performance
* Transfer-learning capability

Using ImageNet-pretrained weights allows the model to start with learned visual features instead of training an entire convolutional network from scratch.

---

## Cybersecurity Relevance

Malicious QR codes can be used in attacks such as:

* Phishing
* Fake payment pages
* Credential theft
* Malicious website redirection
* Fraudulent campaigns
* Malware distribution

An automated QR-code classification system can serve as an additional security layer before a user interacts with a QR code.

However, visual classification alone should not be considered a complete security solution. A production system should also inspect the decoded URL, domain reputation, redirects, SSL/TLS information, and other security signals.

---

## Project Structure

The current repository contains the main project implementation:

```text
Phishing-Attack-GenAI/
│
├── project_1_oct12 (1).py
│
└── README.md
```

A cleaner production-oriented structure could later be organized as:

```text
Phishing-Attack-GenAI/
│
├── data/
│   ├── benign/
│   └── malicious/
│
├── models/
│   └── efficientnet_qr_classifier/
│
├── src/
│   ├── preprocessing.py
│   ├── train.py
│   ├── evaluate.py
│   └── predict.py
│
├── notebooks/
│   └── qr_phishing_detection.ipynb
│
├── requirements.txt
├── README.md
└── .gitignore
```

---

## Future Enhancements

The project can be extended into a complete QR security system.

### 1. Real-Time QR Scanner

Integrate OpenCV with a webcam or mobile camera to detect and classify QR codes in real time.

### 2. QR Content Extraction

Decode the QR code and extract the underlying URL or payload:

```text
QR Image
   |
   v
QR Decoder
   |
   v
URL / Payload
   |
   v
Security Analysis
```

### 3. URL-Based Threat Detection

Combine image classification with:

* URL reputation
* Domain age
* WHOIS information
* DNS analysis
* Redirect detection
* SSL certificate information
* Phishing URL classification

### 4. Hybrid AI Security Model

A future architecture could combine:

```text
QR Image Features
        +
Decoded URL Features
        +
Domain Reputation
        +
Threat Intelligence
        |
        v
     AI Model
        |
        v
    Risk Score
        |
        v
Safe / Suspicious / Malicious
```

### 5. Generative AI Explanation

A Generative AI layer could explain why a QR code was classified as suspicious and provide human-readable security recommendations.

---

## Disclaimer

This project is intended for educational, research, and cybersecurity experimentation purposes.

A machine-learning prediction should not be treated as definitive proof that a QR code is safe or malicious. False positives and false negatives are possible.

Do not use the system as the sole security mechanism for financial transactions, authentication, or other security-critical activities.

---

## Author

**Aswin M**

B.Tech — Computer Science and Engineering

Areas of Interest:

* Cybersecurity
* Artificial Intelligence
* Machine Learning
* Computer Vision
* Generative AI

---

## Project Goal

> Build an AI-powered security layer capable of identifying potentially malicious QR codes before users interact with them.
