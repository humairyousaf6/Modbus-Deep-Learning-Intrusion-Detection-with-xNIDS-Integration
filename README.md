# 🛡️ Modbus Deep Learning Intrusion Detection with xNIDS Integration

A deep learning-based intrusion detection project designed to identify malicious network traffic targeting industrial systems that use the **Modbus communication protocol**.

The project combines a Convolutional Neural Network (CNN) intrusion detection model with **xNIDS-inspired explainability techniques** to classify network traffic and investigate which features contribute to suspicious activity.

The notebook implements a workflow for Modbus dataset preprocessing, CNN model training, xNIDS setup, explainable detection, and interactive custom packet analysis.

The primary goal is to explore how deep learning and explainable AI can support intrusion detection in Industrial Control Systems (ICS) and operational technology (OT) environments.

---

## ✨ Features

- 🛡️ Deep learning-based intrusion detection
- 🏭 Focus on the Modbus industrial communication protocol
- 🧠 CNN-based network traffic classification
- 📦 Modbus dataset preprocessing
- 🔍 PCAP file inspection and Modbus packet filtering
- ⚙️ Network feature normalization
- 🚨 Detection of multiple attack categories
- 🧩 xNIDS framework integration attempts
- 🔬 Feature importance analysis
- 📊 Explainable detection results
- 🎯 Attack classification and confidence reporting
- 📈 Feature importance visualizations
- 🧪 Custom Modbus packet analysis
- 💾 Model and preprocessing parameter loading
- 🛑 Training with early stopping to help reduce overfitting

---

## 🎯 Project Objective

Industrial Control Systems use communication protocols such as Modbus to exchange commands and data between controllers, sensors, and industrial devices.

Malicious network traffic targeting these systems can disrupt operations, manipulate commands, or compromise industrial infrastructure.

Traditional detection methods may identify suspicious traffic without clearly explaining which network characteristics contributed to an alert.

This project explores a deep learning approach that combines intrusion detection with feature-level explanations.

The main objectives are:

- Detect suspicious Modbus network traffic.
- Classify traffic into normal and malicious categories.
- Identify potential attack types.
- Examine features that contribute to model predictions.
- Investigate explainability using xNIDS and a fallback explanation mechanism.
- Analyze custom Modbus packet parameters to demonstrate the detection workflow.

---

## 🏗️ Project Architecture

```text
       Modbus Network Traffic
                 │
                 ▼
          PCAP Dataset
                 │
                 ▼
       Packet Filtering
                 │
                 ▼
       Data Preprocessing
                 │
                 ▼
       Feature Extraction
                 │
                 ▼
       Feature Normalization
                 │
                 ▼
         CNN Classifier
                 │
                 ▼
       Traffic Classification
                 │
          ┌──────┴──────┐
          ▼             ▼
       Normal        Malicious
                        │
                        ▼
               Attack Classification
                        │
                        ▼
             xNIDS / Fallback Explainer
                        │
                        ▼
              Feature Importance
                 & Explanation
```

---

## 🚨 Attack Categories

The notebook identifies seven attack categories in its project description:

1. **C&C Uploading EXE** — associated with uploading an executable to a command-and-control environment.
2. **Moving Two Files** — a file-movement-related attack scenario.
3. **Send Fake Command** — sending unauthorized or manipulated commands.
4. **Exploit MS08 NetAPI** — an attack associated with exploiting the MS08-067 NetAPI vulnerability.
5. **Characterization** — a dataset-defined attack category.
6. **Least Significant Bit Exfiltration** — a data-exfiltration-related attack category.
7. **Reconnaissance** — activity associated with discovering or probing a target environment.

These are the attack categories named in the notebook. Their successful classification and individual detection performance must be verified using the actual evaluation results.

---

## 🧠 CNN-Based Intrusion Detection

The notebook defines a CNN architecture for classifying preprocessed network traffic.

### Model Architecture

The CNN includes:

- Two-dimensional convolutional layers
- ReLU activation functions
- Batch normalization
- Max pooling
- Dropout regularization
- Fully connected layers
- Softmax output for multiclass classification

The model is compiled using the Adam optimizer and sparse categorical cross-entropy loss.

### Training Configuration

The notebook configures training with:

- Maximum epochs: 20
- Batch size: 32
- Early stopping based on validation loss
- Restoration of the best validation weights

Early stopping is intended to reduce unnecessary training and help limit overfitting.

**Note:** These are the model settings defined in the notebook, not a claim that training completed successfully or achieved a particular accuracy.

---

## 🔬 xNIDS Explainability Integration

The project attempts to integrate the xNIDS framework to explain intrusion detection predictions.

The notebook references the xNIDS repository:

https://github.com/CactiLab/code-xNIDS

The integration includes an `IntegratedXNIDSExplainer` class that attempts to initialize the xNIDS explainer and use its available components.

### Explainability Workflow

```text
CNN Prediction
      │
      ▼
Identify Predicted Class
      │
      ▼
Analyze Contributing Features
      │
      ▼
Calculate Feature Importance
      │
      ▼
Display Explanation
```

The implementation attempts to provide:

- Predicted attack category
- Malicious versus normal classification
- Prediction confidence
- Important contributing features
- Protocol-related feature analysis
- Feature importance visualizations

If the real xNIDS components cannot be initialized, the notebook attempts to fall back to an activation-based explanation mechanism.

**Important:** The notebook includes fallback logic, so the presence of an explanation does not necessarily mean the original xNIDS explainer was successfully used. The active explanation method should be verified during execution.

---

## 📦 Dataset and Preprocessing

The notebook contains a preprocessing workflow intended to obtain and prepare Modbus network traffic data.

### Processing Steps

1. Create the required data directories.
2. Download or clone the referenced Modbus dataset.
3. Inspect PCAP files for Modbus traffic.
4. Filter files that contain Modbus packets.
5. Extract or prepare the features needed for model training.
6. Normalize features for the CNN.
7. Save processed data for subsequent training and inference.

The notebook also includes a PCAP validation step using `tshark` to count packets matching the Modbus protocol filter.

### Data Sources

The project references a Modbus dataset hosted through GitHub. The exact dataset source, labels, and preprocessing output should be checked against the notebook's execution results before publishing dataset statistics.

---

## 🔍 Custom Packet Analysis

The notebook includes an interactive function named `explain_custom_packet()` for demonstrating the analysis workflow with manually entered packet fields.

The user can enter parameters such as:

- Source port
- Destination port
- TCP payload length
- Modbus transaction ID
- Protocol ID
- Message length
- Unit ID
- Modbus function code
- Reference number
- Word count
- Byte count
- Exception code
- MEI type
- Read count
- Response time

The entered values are normalized using saved preprocessing parameters and passed to the model explanation workflow.

The notebook then attempts to display whether the packet is classified as malicious, the predicted attack type, confidence, and contributing features.

**Limitation:** Manually entered field values are a demonstration of the analysis interface. They do not constitute a complete PCAP parser or guarantee that a packet can be classified accurately. The input feature order and normalization must match the model's training pipeline.

---

## 📊 Explainability Visualizations

The notebook includes feature-importance visualization functionality using Plotly and Matplotlib.

The intended outputs include:

- Overall feature importance
- Protocol-field importance
- Ranked contributing features
- Attack explanation summaries
- Detection status and confidence
- Visual comparison of important features

These visualizations are intended to make model predictions easier to inspect than a class label alone.

---

## 🛠️ Tech Stack

### Machine Learning and Deep Learning

- Python
- TensorFlow
- Keras
- Convolutional Neural Networks
- Scikit-learn
- NumPy
- Pandas

### Network Traffic Analysis

- Modbus protocol
- PCAP files
- Wireshark command-line utility (`tshark`)
- TCP packet fields

### Explainable AI

- xNIDS framework integration
- Sparse Group Lasso-related components
- Feature importance analysis
- Activation-based fallback explanation

### Visualization

- Matplotlib
- Plotly
- Rich

### Development Environment

- Jupyter Notebook
- Google Colab or a compatible Python environment
- Git

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/humairyousaf6/Modbus-Deep-Learning-Intrusion-Detection-xNIDS.git
cd Modbus-Deep-Learning-Intrusion-Detection-xNIDS
```

### 2. Install Required Tools

Install the Python packages required by the notebook and the system-level `tshark` utility.

Typical Python dependencies include:

```bash
pip install numpy pandas tensorflow scikit-learn matplotlib plotly rich
```

Additional packages may be required by the xNIDS integration and dataset preprocessing code. The exact compatible versions should be determined from a successful notebook run.

### 3. Prepare the Dataset

The notebook creates directories for raw PCAP files and processed data.

The intended structure is:

```text
project/
│
├── data/
│   └── processed/
│
├── pcaps/
│
├── model/
│
├── xnids/
│
└── results/
```

The notebook attempts to download the dataset and set up xNIDS. Verify that these steps complete successfully before proceeding.

### 4. Run the Notebook

Open the notebook:

`Modbus_Deep_Learning_Intrusion_Detection_with_xNIDS_Integration.ipynb`

Execute the cells in sequence:

1. Environment and dataset setup
2. PCAP validation and preprocessing
3. CNN training
4. xNIDS installation and setup
5. Integrated explanation initialization
6. Detection testing and integration
7. Custom packet analysis

Some cells depend on files, model checkpoints, or variables created by earlier cells.

---

## 📁 Project Structure

```text
Modbus-Deep-Learning-Intrusion-Detection-xNIDS/
│
├── Modbus_Deep_Learning_Intrusion_Detection_with_xNIDS_Integration.ipynb
├── data/
│   └── processed/
├── pcaps/
├── model/
├── xnids/
├── results/
└── README.md
```

This represents the intended working structure. Some directories and files are created during notebook execution and may not be present in the repository initially.

Avoid committing large datasets, sensitive network captures, credentials, or proprietary industrial traffic.

---

## 🔮 Future Improvements

- [ ] Add a reproducible dependency file with tested package versions.
- [ ] Verify successful CNN training and checkpoint creation.
- [ ] Document the dataset source, feature schema, and attack-label mapping.
- [ ] Evaluate accuracy, precision, recall, F1-score, and confusion matrix.
- [ ] Report per-attack detection and false-positive rates.
- [ ] Verify xNIDS initialization and explainability output.
- [ ] Distinguish genuine xNIDS explanations from fallback explanations.
- [ ] Validate feature importance against known attack characteristics.
- [ ] Integrate a complete PCAP-to-prediction inference pipeline.
- [ ] Validate custom packet fields against the training feature schema.
- [ ] Add tests for malformed, incomplete, and out-of-range inputs.
- [ ] Evaluate performance on unseen network captures.
- [ ] Improve robustness against class imbalance and previously unseen attacks.
- [ ] Add a dashboard for detection events and explanation summaries.

---

## ⚠️ Limitations and Security Disclaimer

This project is an experimental intrusion detection implementation intended for educational and research purposes.

The notebook's code alone does not establish a verified detection accuracy, real-time monitoring capability, or production readiness. Model performance and xNIDS integration must be validated through successful execution and appropriate testing.

The custom packet analysis function accepts manually entered fields and should not be considered a complete network monitoring solution.

Test only with network captures and systems you are authorized to analyze. Do not use this project to interfere with live industrial equipment or operational technology networks.

---

## 👨‍💻 Author

**Muhammad Humair**

AI/ML & Automation Engineer

- Python
- Machine Learning
- Deep Learning
- Network Security
- Industrial Control Systems
- Intrusion Detection
- Explainable AI
- TensorFlow
- Automation

---

## ⭐ Project Highlights

- 🛡️ Modbus intrusion detection
- 🧠 CNN-based classification
- 🏭 Industrial network security
- 🚨 Multiple attack categories
- 🔬 xNIDS integration attempt
- 📊 Feature importance analysis
- 🔍 Explainable detection workflow
- 📦 PCAP preprocessing
- 🧪 Custom packet analysis
- ⚙️ Research-oriented security experimentation
