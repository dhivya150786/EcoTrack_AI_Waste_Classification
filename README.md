#  EcoTrack AI — Smart Waste Classification and Recycling Assistant

**EcoTrack AI** is a deep learning-based waste classification system that identifies waste categories from images and provides general recycling guidance. It uses **MobileNetV2 transfer learning** to classify waste into six categories and a **Gradio web interface** to make predictions accessible to users.

The project aims to encourage proper waste segregation, improve recycling awareness, and support more responsible waste management.

##  Overview

Waste segregation is an important step toward reducing environmental pollution and improving recycling efficiency. However, identifying the correct waste category can be challenging for people who are unfamiliar with recycling practices.

EcoTrack AI addresses this problem by analyzing an uploaded image and predicting its waste category using a trained deep learning model. After classification, the system displays the prediction scores and provides general recycling guidance relevant to the predicted category.

##  Features

-  **Image-Based Classification:** Upload a waste image for automatic classification.
-  **Deep Learning:** Uses MobileNetV2 with transfer learning.
-  **Six Waste Categories:** Recognizes cardboard, glass, metal, paper, plastic, and trash.
-  **Prediction Scores:** Displays the model's top predicted categories and associated scores.
-  **Recycling Assistant:** Provides general waste-handling and recycling recommendations.
-  **Interactive Web Interface:** Built using Gradio.
-  **Efficient Inference:** Uses a pre-trained convolutional neural network for image feature extraction.
-  **Prediction Disclaimer:** Reminds users to verify the result and follow local waste disposal rules.

##  Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| TensorFlow | Deep learning framework |
| Keras | Model construction and training |
| MobileNetV2 | Pre-trained image classification backbone |
| NumPy | Numerical operations and image arrays |
| Scikit-learn | Stratified dataset splitting and evaluation metrics |
| Pillow (PIL) | Image processing |
| Gradio | Web interface |
| Google Colab | Model development and training |
| Git and GitHub | Version control and project hosting |

##  Dataset

The project uses a waste image dataset obtained from Kaggle.

**Dataset characteristics:**

- Total images: **2,527**
- Number of categories: **6**
- Input image size: **224 × 224 pixels**
- Image input channels: **3 (RGB)**

### Waste categories

| Category | Number of Images |
|---|---:|
| Cardboard | 403 |
| Glass | 501 |
| Metal | 410 |
| Paper | 594 |
| Plastic | 482 |
| Trash | 137 |
| **Total** | **2,527** |

The dataset was divided into training, validation, and testing sets using stratified sampling.

| Split | Percentage | Images |
|---|---:|---:|
| Training | 70% | 1,768 |
| Validation | 15% | 379 |
| Testing | 15% | 380 |

**Dataset source:** [Search for waste classification datasets on Kaggle](https://www.kaggle.com/datasets?search=waste+classification)

The original dataset should be downloaded from its source. It is not included in this repository unless explicitly added.

##  Model Architecture

EcoTrack AI uses **MobileNetV2**, a convolutional neural network pre-trained on ImageNet. Transfer learning allows the project to reuse learned image features instead of training an entire deep neural network from scratch.

### Model pipeline

1. **Image input:** Accepts an RGB waste image.
2. **Image resizing:** Resizes the image to 224 × 224 pixels.
3. **Preprocessing:** Applies the preprocessing expected by MobileNetV2.
4. **Feature extraction:** Uses the pre-trained MobileNetV2 base model.
5. **Global average pooling:** Converts feature maps into a compact representation.
6. **Dropout:** Applies a dropout rate of 0.3 to help reduce overfitting.
7. **Classification layer:** Predicts probabilities for six waste categories using softmax.

### Training configuration

| Parameter | Value |
|---|---|
| Architecture | MobileNetV2 |
| Learning approach | Transfer learning |
| Input dimensions | 224 × 224 × 3 |
| Batch size | 32 |
| Initial learning rate | 0.001 |
| Maximum epochs | 10 |
| Optimizer | Adam |
| Loss function | Sparse categorical cross-entropy |
| Early stopping | Enabled |
| Number of classes | 6 |

##  Performance Results

The trained model achieved **90.53% test accuracy** on the fixed test set of 380 images.

- **Test accuracy:** 90.53%
- **Test loss:** 0.2845
- **Weighted F1-score:** Approximately 0.91

### Classification report

| Category | Precision | Recall | F1-Score |
|---|---:|---:|---:|
| Cardboard | 0.98 | 0.92 | 0.95 |
| Glass | 0.90 | 0.86 | 0.88 |
| Metal | 0.95 | 0.94 | 0.94 |
| Paper | 0.90 | 0.97 | 0.93 |
| Plastic | 0.87 | 0.85 | 0.86 |
| Trash | 0.75 | 0.90 | 0.82 |
| **Macro average** | **0.89** | **0.90** | **0.90** |
| **Weighted average** | **0.91** | **0.91** | **0.91** |

These results indicate promising performance on the current dataset. The trash category has lower precision than the other categories, indicating that further training and data improvements may be beneficial.

##  Installation

### Prerequisites

- Python 3.10 or a compatible Python version supported by the selected TensorFlow release
- pip
- Git
- The trained model and class-label files

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/EcoTrack-AI.git
cd EcoTrack-AI
```

Replace `YOUR_USERNAME` with your GitHub username.

### 2. Create a virtual environment (recommended)

**Windows:**

```bash
python -m venv venv
venv\Scripts\activate
```

**Linux or macOS:**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

If the requirements file is not yet available, install the main packages with:

```bash
pip install tensorflow gradio numpy pillow scikit-learn
```

For reproducible deployment, pin and test the package versions used by the working Colab environment.

### 4. Verify required files

Ensure that these files are available in the project directory:

- `app.py`
- `ecotrack_waste_model.keras`
- `ecotrack_class_names.json`
- `requirements.txt`

The application cannot perform predictions if the model or class-label file is missing.

##  Usage

### Run the application locally

Open a terminal in the project directory and run:

```bash
python app.py
```

Open the local URL printed by Gradio in your browser.

### Classify a waste image

1. Open the EcoTrack AI interface.
2. Upload a picture of a waste item.
3. Click **Classify Waste**.
4. View the predicted waste category and top prediction scores.
5. Read the recycling guidance.
6. Verify the material and follow the recycling rules applicable in your area.

### Example

**Input:** An image of a cardboard box.

**Expected output:**
- Predicted category: Cardboard
- Confidence score: A model-generated probability
- Recycling guidance: Flatten the cardboard, keep it dry, and check local recycling requirements.

The actual category and score depend on the uploaded image.

##  Limitations

- The model recognizes only the six categories included in its training dataset.
- The trash class does not specifically identify organic waste.
- Similar-looking materials may be misclassified.
- The dataset is relatively small and may not represent every real-world waste item.
- Prediction scores are model outputs and should not automatically be interpreted as calibrated probabilities.
- Recycling rules vary by location, and the guidance is not a substitute for local regulations.
- The system has not been established as a certified waste identification or environmental compliance tool.

##  Future Enhancements

Potential improvements include:

-  Increasing the size and diversity of the training dataset.
-  Adding separate organic waste and e-waste categories using suitable labeled images.
-  Improving classification of visually similar waste materials.
-  Comparing MobileNetV2 with EfficientNet, ResNet, and other architectures.
-  Adding confusion matrices and training-history visualizations.
-  Developing a mobile-friendly interface.
-  Integrating location-specific recycling guidance.
-  Adding waste disposal recommendations based on material type.
-  Deploying the application to a hosting service for public access.
-  Evaluating the model on a separate real-world dataset.

## Disclaimer

EcoTrack AI is an educational AI project developed for waste image classification and recycling awareness. Its predictions may be incorrect. Always verify the material and consult local recycling or waste management guidelines before disposing of an item.

##  Author

**Dhivya U.**

