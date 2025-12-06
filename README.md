# LayerByLayer

---

#  Real-Time Oil Spill Detection Using SAR–AIS Data Fusion

### AI-Powered Maritime Environmental Monitoring

![Python](https://img.shields.io/badge/Python-3.10-blue.svg)

---

##  Overview

This project introduces a **real-time oil spill detection system** that fuses **Synthetic Aperture Radar (SAR)** satellite imagery with **Automatic Identification System (AIS)** vessel tracking data. The framework applies **deep learning**, **anomaly detection**, and **multi-channel alerting** to deliver accurate and scalable spill detection for maritime environmental protection.

---

##  Problem Statement

Traditional oil spill monitoring methods face significant constraints:

* Slow, manual reporting
* High false positives due to single-source detection
* Lack of predictive vessel behavior monitoring
* Insufficient connectivity in offshore areas
* Limited automation in existing surveillance systems

**Objective:** Develop an **AI-driven, automated** system capable of detecting spills with high precision in real time.

## How This System Addresses the Problem

Traditional oil spill monitoring systems fail mainly due to delayed detection, single-source dependency, and lack of automation. The LayerByLayer Real-Time SAR–AIS Fusion System solves these limitations through a multilayered, intelligent workflow:

### 1. Overcoming Slow & Manual Detection

Problem:
Oil spills are often detected hours or days later through manual observation, patrol reports, or delayed satellite analysis.

Solution:

The system ingests live SAR satellite imagery at frequent intervals.

AIS streams update every few seconds.

Serverless cloud functions ensure instant processing once new data arrives.

Result: Near real-time detection (seconds to minutes) instead of manual delays.

### 2. Reducing False Positives in SAR-Only Detection

Problem:
SAR images alone often misclassify look-alike phenomena such as:

Low wind areas

Algal blooms

Ship wakes

Calm water shadows

This leads to high false alarm rates.

Solution:

A dedicated CNN classifier detects spill patterns with higher precision.

Detections are further validated using AIS anomalies (vessel slowing, erratic motion, route deviation).

Cross-verification only triggers a spill when both sources agree.

Result: High-confidence spill detection with drastically reduced false positives.

### 3. Predicting Spill-Risk Before It Happens

Problem:
Existing systems only detect spills after they occur—no early warning.

Solution:

LSTM models analyze vessel behavior and flag suspicious patterns:

Abrupt halts

Unusual U-turns

Speed oscillations

Loitering in non-designated zones

Result: Early identification of vessels likely to discharge oil → proactive prevention.

### 4. Operating Reliably in Low-Connectivity Maritime Zones

Problem:
Offshore areas lack stable internet or cellular coverage, preventing timely reporting.

Solution:
A multi-layered alert delivery system ensures uninterrupted communication through:

AIS broadcast messages

VHF maritime radio

Satellite Short Burst Data (SBD)

SMS & email when connectivity is available

**Result: Alerts reach vessels & authorities even in remote, network-dark regions.

### 5. Automating the Entire Detection → Alert Flow

Problem:
Current workflows require human verification, leading to delays and inconsistencies.

Solution:
Every component is automated:

SAR classification

AIS anomaly scoring

Fusion-based confirmation

Auto-triggered alerts

Dashboard updates

Serverless architecture removes the need for continuous human monitoring.

Result: Fully automated, hands-free, real-time environmental surveillance.

### 6. Supporting Scalable, Global Maritime Monitoring

Problem:
National-scale detection systems struggle to scale to international waters.

Solution:

Serverless compute (Lambda / Cloud Functions)

Docker microservices

Modular plug-and-play architecture

Transfer learning for regional adaptation

Result: The system scales from local coastal zones to global coverage with minimal configuration.

---

##  System Architecture

### **1️ Data Acquisition**

* **SAR Image Feed:** Sentinel-1 (ESA Copernicus)
* **AIS Vessel Feed:** MarineTraffic / Spire Maritime

### **2️ Data Fusion**

Combines SAR detections with AIS anomalies using:

* Spatial correlation
* Temporal synchronization
* Vessel proximity and movement patterns

### **3️ Detection Models**

* **CNN** → SAR spill classification
* **Isolation Forest** → AIS outlier movement detection
* **LSTM** → Temporal vessel behavior prediction

### **4️ Alert Engine**

* Email
* SMS
* Mobile push
* Dashboard notifications
* VHF maritime radio
* AIS broadcast messages
* Satellite Short Burst Data (SBD)

### **5️ Deployment**

* Serverless architecture (AWS Lambda / GCP Functions)
* Docker-based microservices
* Cloud storage + message queues

---

##  Algorithms Used

###  AIS Anomaly Detection

| Algorithm          | Purpose                                          |
| ------------------ | ------------------------------------------------ |
| Isolation Forest   | Detects abnormal patterns in vessel trajectories |
| LSTM               | Predictive vessel behavior analysis              |
| Rule-Based Filters | Validates proximity, timestamps, speed profiles  |

---

###  SAR Image Classification

| Algorithm                   | Purpose                                        |
| --------------------------- | ---------------------------------------------- |
| CNN                         | Distinguishes oil spill vs non-spill regions   |
| Transfer Learning           | Adapts pre-trained models for new regions      |
| Synthetic Data Augmentation | Compensates for low spill dataset availability |

---

##  Data Pipeline

### **1. SAR Image Workflow**

* Noise reduction
* Geometric correction
* Patch extraction
* CNN classification

### **2. AIS Workflow**

* Continuous AIS ingestion
* Outlier detection (Isolation Forest)
* Trajectory prediction (LSTM)

### **3. Fusion Layer**

A spill is validated **only when both SAR and AIS indicators align** spatially and temporally.

### **4. Alert Dispatch**

Alerts include:

* Coordinates
* Detected spill region
* Vessel IDs
* Confidence score
* Timestamp

---

##  Alerting System

A multi-layered notification architecture ensures redundancy.

### Channels:

*  **Email Alerts** (with SAR snapshots)
*  **SMS Alerts**
*  **Push Notifications**
*  **Live Dashboard Updates**
*  **VHF Maritime Broadcasts**
*  **AIS Safety Message Broadcasts**
*  **Iridium SBD Satellite Alerts**

---

##  Innovation & Uniqueness

* **SAR + AIS multimodal fusion** → drastically reduced false positives
* **Predictive anomaly detection** with LSTM for early warning
* **Synthetic spill generation** for better model generalization
* **Serverless cloud-native architecture** for high scalability
* **Drone-based verification module** for real-time confirmation
* **Edge-device compatibility** for onboard vessel deployment
* **Modular microservice design** for easy extension

---

##  Tech Stack

### **Languages**

* Python
* JavaScript (Dashboard)

### **AI / ML**

* PyTorch
* Scikit-learn
* OpenCV
* GeoPandas

### **Data Providers**

* Sentinel-1 SAR
* MarineTraffic AIS
* Spire Maritime AIS

---

##  Future Enhancements 

###  AI-Based Spill Severity Estimation

Use U-Net or Mask R-CNN to assess spill area, spread rate, and thickness.

###  Spill Drift & Weather Forecasting

Integrate:

* Wind fields
* Tide models
* Ocean currents

###  Blockchain Event Logging

Ensures tamper-proof evidence for insurance and legal claims.

###  Federated Learning Support

Enables international agencies to train models without sharing raw data.

###  On-Vessel Edge AI

Runs lightweight CNN + AIS anomaly detection locally on ships.

---

## Figures 

<img width="279" height="803" alt="image" src="https://github.com/user-attachments/assets/9f878d84-9e0b-4ba2-afb8-8aa28a974bf6" />

* Sentinel-1 SAR example scene 
<img width="516" height="251" alt="image" src="https://github.com/user-attachments/assets/15eb7f64-8880-49a7-84ff-92bbf8c33b80" />

* Satellite SBD block diagram 
<img width="508" height="227" alt="image" src="https://github.com/user-attachments/assets/14ad7017-2a04-456d-985f-64038d46ed1e" />

---

##  Contributors

* **Sri Varshan P**
* **Shriram S**
* **Mr. Dinesh Babu G L** (Assistant Professor, Guide)
* **Kanishkar M**




