# Innovasure: AI-Powered Medical Document Processing System

## 1. Business Introduction

### 1.1. Managing Medical Documents with Handwritten Annotations
Managing medical documents with handwritten annotations remains a major challenge due to the time-consuming nature of manual processing and the risk of human errors. The variability of handwriting styles further complicates accurate data extraction, making it difficult for healthcare providers to efficiently manage patient records and administrative tasks.

### 1.2. Proposed AI-Powered Solution
To address these challenges, we propose Innovasure - an AI-powered solution that automates the extraction of handwritten data, ensuring accuracy, efficiency, and seamless integration into existing healthcare systems.

## 2. Business Understanding

### 2.1. Problem Statement
- **Manual Processing Challenges**: Medical care documents often contain handwritten annotations that are crucial for traceability. However, the current manual processing of these documents is time-consuming and prone to human errors. This is due to the complexity and variability of handwriting styles, leading to potential misinterpretations and critical errors in patient care or administrative follow-up.

### 2.2. Objectives
- **Automate Handwritten Data Extraction**: The primary goal is to develop an advanced AI model capable of accurately extracting handwritten information from medical care documents including dates, financial amounts, and medical references.
- **Handle Handwriting Variability**: The solution must adapt to the diversity of handwriting styles and document structures to ensure high accuracy.
- **Minimize human errors** in claim processing by ensuring precise data extraction and reimbursement calculations.

### 2.3. Solution Architecture
- **Data Collection and Preprocessing**: Collect care documents containing handwritten annotations and use techniques like filtering, image normalization, and noise removal.
- **AI Model**: OCR for text detection, CNNs for visual feature extraction, and RNNs for contextual understanding.
- **API for System Interaction**: Facilitate seamless integration with existing healthcare systems.
- **Data Storage**: Store extraction results and metadata in a secure database.
- **Security and Compliance**: Ensure encryption and compliance with HIPAA and GDPR standards.

### 2.4. Business Value
- **Efficiency**: Significant reduction in time and effort for managing handwritten data
- **Accuracy**: Reduced human errors through advanced AI models
- **Scalability**: Designed to handle increasing volumes of medical documents
- **Security**: Compliance with medical data security regulations
- **Integration**: Web-based platform with intuitive UI and API capabilities

### 2.5. Market Opportunity
- **Healthcare Providers**: Hospitals, clinics, and other facilities dealing with large volumes of medical documents
- **Regulatory Compliance**: Growing demand for solutions ensuring compliance with data security regulations
- **Technological Advancement**: Increasing adoption of AI and machine learning in healthcare

### 2.6. Conclusion
Automating handwritten data extraction in medical care documents enhances efficiency, accuracy, and scalability while ensuring compliance with data security regulations. This solution minimizes human errors, streamlines administrative workflows, and integrates seamlessly into existing healthcare systems.

## 3. Data Understanding

### 3.1. Overview of the Dataset
The dataset consists of medical documents including prescriptions (ordonnances) and care reports (bulletins de soins) in image format with manual annotations.

### 3.2. Structure of the Dataset
#### 3.2.1. Data Content
- Mix of printed and handwritten texts
- Annotations include bounding boxes and class labels

#### 3.2.2. Targeted Entities (Fields Annotated)
- Medication names
- Dosages
- Specialties (e.g., General Practitioner, Cardiologist)

### 3.3. Challenges of the Dataset
- Mixed printed and handwritten content
- Handwriting variability in styles, slants, and quality
- Document layout variability
- Complex annotations with overlapping entities

### 3.4. Strengths of the Dataset
- Real-world complexity mimicking medical document diversity
- Diversity of writing styles and layouts
- Rich annotation targeting both structured and unstructured content

## 4. Data Acquisition

### 4.1. Data Sources
- Medical prescriptions
- Medical care reports

### 4.2. Data Collection
- 3,000 medical document images collected
- Balanced dataset including both prescriptions and care reports

### 4.3. Data Annotation
- Manual annotation using Roboflow platform
- Global labels and specific bounding boxes for key fields
- Exported in structured formats (CSV, JSON)

## 5. Data Preparation

### 5.1. DSO1 – Binary Document Classification
#### 5.1.1. Objective
Build a binary classification model to distinguish between "Prescription" and "Medical Care Report"

#### 5.1.2. Dataset Organization
- Prescriptions folder
- Medical Care Reports folder
- Other Documents folder

#### 5.1.3. Label Assignment and Path Structuring
- "Prescription" → class 0
- "Medical Care Report" → class 1

#### 5.1.4. Dataset Splitting
- Training set: 70%
- Validation set: 15%
- Test set: 15%
<img width="579" height="479" alt="image" src="https://github.com/user-attachments/assets/c8b41d6c-6684-4210-add8-10d9df41edd1" />

### 5.2. DSO2 – OCR Pipeline Development
#### 5.2.1. Objective
Develop an OCR pipeline to extract handwritten texts from images

#### 5.2.2. OCR Pipeline Development Stages
- Reusing Annotated Images
- Annotation and Encoding
- Deskewing
- Contrast and Brightness Enhancement
- Resize and Padding
- Normalization
- Color-Aware Thresholding
<img width="580" height="310" alt="image" src="https://github.com/user-attachments/assets/eb394bab-05dd-40df-a333-ab74dfa4e553" />

## 6. Text Analysis

### 6.1. DSO3 – Specialty Identification and Fraud Detection
#### 6.1.1. Objective
- Identify medical specialties mentioned in documents
- Detect fraudulent activities by analyzing anomalies in invoices

#### 6.1.2. Strategy for Medical Specialty Identification
- Focused Region: Header of prescriptions
- Reduction of noise and higher concentration of specialty mentions

#### 6.1.3. Strategy for Fraud Detection
- Analyze anomalies in invoices against official databases


## 7. Modeling

### 7.1. DSO1 – Document Classification Model
#### 7.1.1. Data Augmentation and Preprocessing
- Rescaling, random rotations, shifts, shearing, zooming, flipping
- ImageDataGenerator for augmentation

#### 7.1.2. Model Architecture
- MobileNetV2 backbone with custom classification head
- GlobalAveragePooling2D, Dropout(0.3), Dense(128, relu), Dense(3, softmax)

#### 7.1.3. Compilation Settings
- Optimizer: Adam
- Loss: Categorical Crossentropy
- Metrics: Accuracy

#### 7.1.4. Handling Class Imbalance
- Class weights computed using compute_class_weight('balanced')

#### 7.1.5. Training Strategy
- First Training Phase: Frozen backbone, 10 epochs
- Fine-Tuning Phase: Unfreeze last 20 layers, lower learning rate

#### 7.1.6. Summary and Key Achievements
- Effective document classification with high accuracy
- Robust to document variations

### 7.2. DSO2 – Handwritten Text Recognition
#### Approach 1: CRNN-Based OCR
##### 7.2.1. Objective
Extract handwritten text using CRNN architecture

##### 7.2.2. Data Annotation
- Bounding boxes around fields of interest using Roboflow

##### 7.2.3. Data Augmentation
- Rotation, scaling, brightness/contrast adjustment, noise injection, elastic distortions

##### 7.2.4. CRNN Architecture
- CNN for feature extraction, RNN for sequence modeling, CTC loss

##### 7.2.5. Model Training
- Adam optimizer, initial learning rate 0.001
- Early stopping and checkpointing
##Some results

<img width="556" height="240" alt="image" src="https://github.com/user-attachments/assets/b245472c-3b52-4953-8ee5-0e7b6ac24b68" />
##### 7.2.6. Evaluation & Fine-Tuning
- Character-level accuracy: ~87%
- Word-level accuracy: ~79%
<img width="355" height="355" alt="image" src="https://github.com/user-attachments/assets/24caa70e-ce4f-4d29-9263-b8e8bc814865" />

##### 7.2.7. Why CRNN?
- Combines CNN's visual feature extraction with RNN's sequence modeling

#### Approach 2: Hybrid OCR Pipeline (EasyOCR + PaddleOCR + TrOCR)
##### 7.2.8. Tools Used
- EasyOCR, PaddleOCR, TrOCR, Ollama (LLaMA 3)

##### 7.2.9. Pipeline Overview
1. Text Detection with EasyOCR and PaddleOCR
   <img width="426" height="213" alt="image" src="https://github.com/user-attachments/assets/afc63e63-e220-4710-a097-6d6d0aaa292c" />

3. Crop Extraction and preprocessing
   <img width="468" height="244" alt="image" src="https://github.com/user-attachments/assets/fb80abc0-92ec-4ad9-bd50-98e53de237ba" />

5. Text Recognition with TrOCR
6. Post-Processing with fuzzy matching and LLaMA 3
   <img width="514" height="237" alt="image" src="https://github.com/user-attachments/assets/37ffee37-4c85-41fe-9e38-4ff9bcae93d9" />

8. Export to structured formats
   <img width="434" height="339" alt="image" src="https://github.com/user-attachments/assets/e1bf852d-8842-4bf9-b201-83aaee234e27" />



##### 7.2.10. Justification for Hybrid Pipeline
- Combines strengths of multiple OCR tools for robust performance

### 7.3. DSO3 – Specialty & Fraud Detection
#### 7.3.1. Tools & Preprocessing
- Tesseract OCR, Pytesseract, Pandas, Fuzzywuzzy, Unidecode
<img width="378" height="201" alt="image" src="https://github.com/user-attachments/assets/8da9f39a-dc98-44c5-bb3b-9fb13b7930b9" />

#### 7.3.2. CNAM Matching
- Fuzzy matching with 85% similarity threshold
- Medication validation against official database
<img width="413" height="334" alt="image" src="https://github.com/user-attachments/assets/afeb61aa-2671-4186-81c9-a30cc08a0079" />

#### 7.3.3. Anomaly Detection
- Unknown medication detection
- High price/quantity detection
- Price markup detection

#### 7.3.4. Specialty Extraction Pipeline
- Bounding box detection with PaddleOCR
- Transcription with TrOCR
- Fuzzy matching with specialty lexicon
<img width="567" height="394" alt="image" src="https://github.com/user-attachments/assets/12b63eea-090e-4ddf-be9f-9322f475108e" />

#### 7.3.5. Results & Distribution
- General Medicine: 42.3%
- ENT: 18%
- Other specialties: Neurology, Dermatology, Cardiology
<img width="558" height="426" alt="image" src="https://github.com/user-attachments/assets/3e34a52c-51d3-4569-aa4a-1778fefe19d0" />

## 8. Evaluation Phase

### 8.1. Evaluation Strategy
- Separate evaluation for CRNN and hybrid OCR approaches

### 8.2. Metrics Used
- Character-level accuracy
- Word-level accuracy
- Bounding box precision & recall

### 8.3. CRNN Evaluation Results
- Character-level accuracy: ~87%
- Word-level accuracy: ~79%

### 8.4. TrOCR Hybrid Pipeline Results
- Character accuracy > 90%
- 25% improvement in recall with PaddleOCR
- 18% reduction in false negatives with LLaMA 3

### 8.5. Human Validation
- Consistency score: ~91.4%
- Most errors from poorly scanned images

### 8.6. Key Takeaways
- Hybrid pipeline outperforms standalone CRNN
- Domain knowledge improves results significantly
- Layered architecture provides resilience to variability

## 9. Deployment Phase

### 9.1. Web Application with Flask
- User-friendly web interface for document analysis


### 9.2. Tech Stack
- Backend: Flask
- Frontend: HTML5, Bootstrap, CSS
- OCR & NLP: TrOCR, PaddleOCR, EasyOCR, Tesseract, LLaMA 3
- Export: fpdf, openpyxl
- Authentication: Social login with Facebook and Google
- Storage: Google Drive integration

### 9.3. Main Functionalities
- Document upload and classification
- Text extraction and anomaly detection
- Specialty detection
- Interactive dashboard
- Report generation

### 9.4. Interface Overview
- Main page for upload and analysis
  <img width="705" height="366" alt="image" src="https://github.com/user-attachments/assets/fe38d5b7-5e4f-4366-a1a5-f3fae6bcdfad" />
- Invoice tab for verification and reporting
  <img width="715" height="343" alt="image" src="https://github.com/user-attachments/assets/cf23fcf7-2ca3-4961-a11e-a6b44500becf" />

- About section with project details
- Login/Signup with OAuth2
<img width="711" height="320" alt="image" src="https://github.com/user-attachments/assets/fb716d0d-0e24-4cd1-a8d5-e84ab5839416" />

### 9.5. Benefits of Deployment
- Lightweight and scalable
- Easy model integration
- Real-time feedback
- Intuitive interface for non-technical users

## 10. Conclusion

The Innovasure project represents a comprehensive AI solution for medical document processing. By combining deep learning, OCR technologies, and modern deployment strategies, we've built a robust pipeline that automates classification, recognition, and validation of complex medical data. The system achieves high accuracy in recognizing handwritten content, integrates with official databases for validation, and provides a user-friendly interface for practical use.

## Perspectives

Future enhancements include:
- Real-time integration with EHR and insurance platforms
- Support for additional document types
- Improved multilingual support
- Advanced anomaly detection using unsupervised learning
- Interactive feedback loop for continuous improvement
- Mobile-friendly deployment options
