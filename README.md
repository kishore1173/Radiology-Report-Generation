# 🏥 MedRad-KG: Radiology Report Generation

## 📄 Abstract
Abstract— Radiology report generation aims to automate 
the generation of diagnostic descriptions from radiographic 
images, reducing the workload of radiologists and assisting in 
the early detection of abnormalities. However, the existing 
report-generation models face several challenges. First, 
abnormal regions in radiology images often occupy only a 
small portion of the scan, making it difficult for models to 
focus on critical areas. Second, Insufficient alignment between 
image features. Third, a lack of medical knowledge integration. 
To address these limitations, we propose MedRad-KG, a 
multimodal knowledge-guided radiology report generation 
framework. Our model leverages the Region-Based Swin 
Transformer to extract detailed image features and predict 
diagnosis labels. Then, the RoBERT model generates initial 
findings and impressions based on image features. A Meditron 
model will cross-check the findings against the predicted 
diagnosis and either refine or regenerate the report to ensure 
consistency and accuracy. Additionally, we incorporate a 
medical knowledge graph (KG) to enhance interpretability and 
support clinical reasoning. By leveraging cross-modal 
interaction and knowledge-guided verification, our approach 
improves report completeness and reduces the risk of missing 
critical abnormalities. We evaluate MedRad-KG on the IU X
Ray and MIMIC-CXR datasets, demonstrating superior 
performance in clinical accuracy, coherence, and abnormality 
detection. Experimental results highlight its potential for real
world applications, showcasing the effectiveness of multimodal 
learning and medical knowledge integration in automated 
radiology reporting.  
## 🌟 Key Features
- **Multimodal Learning**: Combines image (X-ray) and text (findings, impressions) for enhanced report generation.
- **Transformer-Based Approach**: Uses Swin Transformer for image feature extraction and RoBERTa/Meditron for text generation.
- **Knowledge Integration**: Ensures consistency between predicted diagnosis and report content.
- **Grad-CAM Visualization**: Generates heatmaps to highlight critical areas in the X-ray image.
- **Improved Coherence & Accuracy**: Outperforms baseline models in BLEU, ROUGE, and METEOR scores.

## 📂 Dataset
MedRad-KG is trained on two publicly available medical datasets:

1. **IU Chest X-ray**:
   - Contains **7,470** chest X-ray images paired with corresponding radiology reports.
   - Each report includes **Findings** (detailed observations) and **Impression** (summary diagnosis).
   
2. **MIMIC-CXR**:
   - A large-scale dataset with **377,110** chest X-ray images linked to structured radiology reports.
   - Includes metadata such as **view position, patient history, and radiologist annotations**.
   - Text data consists of **Findings** and **Impression** sections.

## 🏗️ Model Architecture
The MedRad-KG pipeline consists of:

1. **Image Feature Extraction (Swin Transformer)**:
   - Swin Transformer processes chest X-ray images and extracts region-aware feature embeddings.
   
2. **Diagnosis Prediction (RoBERTa-based Classifier)**:
   - RoBERTa predicts disease labels from extracted features and findings.
   
3. **Cross-Attention Layer**:
   - Aligns Swin Transformer’s image embeddings with RoBERTa’s text embeddings.
   
4. **Final Report Generation (Meditron LLM)**:
   - Takes the diagnosis and findings to generate a structured radiology report.

## 🚀 Training Pipeline

### **Preprocessing Steps**:
- **Image Preprocessing**:
  - Resize images to **224×224** pixels.
  - Normalize pixel values and apply data augmentation.

- **Text Preprocessing**:
  - Tokenization using **WordPiece (for Meditron) and Byte-Pair Encoding (for RoBERTa)**.
  - Remove stop words, punctuation, and special characters.

### **Hyperparameters (from Paper)**:
- **Batch Size**: 16
- **Learning Rate**: 5e-5 (with warmup and AdamW optimizer)
- **Dropout**: 0.3
- **Training Epochs**: 30 (early stopping if validation loss doesn’t improve for 5 epochs)

## 📊 Results
The performance of MedRad-KG is evaluated using BLEU, ROUGE, and METEOR scores.

### **Comparison with Other Models**

| Model         | Dataset       | BLEU-1 | ROUGE-L | METEOR |
|--------------|-------------|--------|---------|--------|
| MedRad-KG    | IU-CXR      | **0.58** | **0.44**  | **0.23**  |
| Baseline (R2Gen) | IU-CXR      | 0.47   | 0.37    | 0.18   |
| MedRad-KG    | MIMIC-CXR   | **0.49** | **0.41**  | **0.20**  |
| Baseline (ADAATT) | MIMIC-CXR   | 0.29   | 0.26    | 0.11   |

## ⚖️ License
This project utilizes:
- **Swin Transformer** (MIT License)
- **RoBERTa** (Apache 2.0 License)
- **Meditron** (CC-BY 4.0 License)

## 👨‍💻 Developer
**Kishore M & Aravindraj R** 

---

