# Real-Time Oil Spill Detection Using SAR–AIS Data Fusion
## AI-Powered Maritime Environmental Monitoring

## Overview

This system provides real-time oil spill detection by combining Synthetic Aperture Radar (SAR) satellite imagery with Automatic Identification System (AIS) vessel tracking data. Deep learning models classify spills from radar images, anomaly detection evaluates vessel behavior, and a multi-channel alerting framework enables quick responses in maritime environments.

## Problem Statement

Oil spills often go unnoticed for long periods because traditional detection depends heavily on manual reports or infrequent satellite checks. SAR-only surveillance generates many false positives because natural phenomena can resemble oil slicks. Existing systems also cannot predict vessel behavior before a spill happens. Remote maritime zones often lack connectivity, preventing timely communication. Manual verification slows down response workflows, and conventional architectures struggle to scale across large ocean regions.
Objective: Build an AI-driven, automated, scalable system that detects spills accurately and delivers alerts instantly.

## How This System Addresses the Problem
### Late Detection & Slow Response

Traditional monitoring systems often detect spills long after they occur because they rely heavily on manual observation, patrol reports, or infrequent satellite imagery. During this delay, oil spreads across the water surface, making containment harder and increasing environmental damage. The lack of continuous sensing means early warning signs are missed, and response teams lose valuable time. This delay also weakens the ability to trace spills back to responsible vessels.

#### Solution:
Live SAR imagery is captured at frequent intervals and processed immediately upon arrival, while AIS streams update vessel data in real time. Serverless cloud functions automatically trigger analysis as soon as new data is available, removing the need for human intervention. This enables spill detection within seconds or minutes rather than hours. By dramatically reducing the detection window, the system improves response speed, accuracy, and overall environmental protection.

### High False Positives from SAR Alone

Radar-based satellite imagery, while powerful, often struggles to differentiate true oil slicks from natural ocean surface variations. Calm-water patches, biological films, low-wind areas, or ship wakes can appear visually similar to oil spills in SAR images. When SAR is used alone, these look-alikes create a large number of false detections that waste time and require manual verification. This reduces trust in automated monitoring systems and slows down response operations.

#### Solution:
A CNN model processes SAR patches to identify potential spill regions with improved precision based on learned texture features. These detections are then cross-checked with AIS vessel behavior to determine whether any nearby ship was moving suspiciously, such as slowing abruptly or deviating from its route. By confirming spills only when both visual and behavioral signals align, the system drastically reduces false positives. This dual-validation approach ensures that alerts are reliable and actionable.

### No Early Prediction of Spill Risk

Conventional spill detection systems operate reactively, meaning they only recognize a spill once oil has already surfaced and become visible in satellite imagery. This leaves no opportunity to anticipate risky vessel behavior or intervene before environmental damage begins. Many illegal discharges or accidental leaks are preceded by abnormal ship movements that go unnoticed using traditional tools. Without predictive monitoring, authorities lose the chance to prevent incidents rather than merely respond to them.

#### Solution:
LSTM models continuously analyze vessel movement sequences, learning normal patterns and identifying deviations that signal potential risk. Behaviors such as abrupt stops, sharp course changes, prolonged loitering, or unexpected detours are detected as early warning indicators. When a vessel behaves unpredictably, the system generates a pre-spill alert, allowing authorities to investigate before any oil is discharged. This predictive capability transforms monitoring from reactive detection to proactive prevention.

### Connectivity Issues in Offshore Regions

A large portion of maritime activity occurs far from coastal infrastructure, where traditional communication networks—such as mobile data or broadband internet—are unavailable. When spills occur in these remote areas, alerts often fail to reach authorities promptly, delaying response efforts and increasing environmental impact. Limited connectivity also prevents ships in the vicinity from receiving hazard warnings, increasing the risk of vessel contamination or navigation hazards. This communication gap is one of the biggest operational challenges in large-scale ocean monitoring.

#### Solution:
To ensure uninterrupted communication, the system uses maritime-grade channels that function independently of cellular networks. AIS safety broadcasts can immediately warn nearby vessels, while VHF radio provides short-range emergency messaging widely supported by ships. For global coverage, satellite Short Burst Data (SBD) delivers alerts directly to command centers regardless of location. This multi-path alert strategy guarantees that critical spill notifications reach responders even in the most remote ocean regions.

### Manual Verification Delays

Traditional spill monitoring workflows depend heavily on human operators to review satellite images, validate vessel activity, and confirm potential incidents. This manual process is slow, labor-intensive, and prone to human error, especially when analysts must handle large volumes of data. As a result, genuine spills may be confirmed too late, while inconsistent decision-making across operators can lead to missed detections or unnecessary false alarms. Manual verification also limits the scalability of monitoring operations, since human capacity becomes the bottleneck.

#### Solution:
The system automates the entire verification pipeline by combining SAR-based CNN classification with AIS anomaly scoring and rule-based fusion logic. Each new data input triggers automatic processing and spill confirmation without waiting for human review. High-confidence events are immediately forwarded to the alert engine, ensuring rapid response times. This automated approach eliminates delays, standardizes detection quality, and allows the system to operate continuously at a large scale.

### Lack of Scalability & Regional Adaptation

Traditional spill detection systems often rely on fixed infrastructure, monolithic software, or region-specific models that do not generalize well beyond their original deployment area. When these systems are expanded to larger ocean regions, they struggle with increased data volumes, diverse environmental conditions, and varying vessel traffic patterns. Models trained for one coastline may fail when applied to different climates, sea states, or operational behaviors. This lack of scalability limits their usefulness for countries or organizations responsible for monitoring wide maritime zones.

#### Solution:
A cloud-native microservice architecture enables the system to scale automatically with data load, allowing real-time processing even across large geographic areas. Transfer learning techniques let the detection models adapt quickly to new maritime regions using small amounts of local data. The modular design allows components such as SAR processing, AIS analysis, and fusion logic to be customized independently. This flexibility ensures consistent performance regardless of location or environmental variability, making the system suitable for global deployment.

## System Architecture
### Data Acquisition

SAR data from the Sentinel-1 satellites is collected to capture radar-based imagery of the ocean surface under all weather and lighting conditions. These images reveal surface roughness variations that help identify potential oil slicks. At the same time, AIS data streams provide live vessel information such as position, speed, and heading. The combination of continuous SAR and AIS input creates a rich, real-time dataset for monitoring maritime activity. This dual-source acquisition ensures that both environmental patterns and vessel movements are observed simultaneously.

### Data Fusion

In the fusion stage, SAR-based spill detections are matched with AIS vessel movements based on both spatial proximity and timestamp alignment. By correlating radar anomalies with nearby vessel behavior, the system determines whether a suspicious slick might be linked to a specific ship. This cross-analysis reduces false positives because natural ocean features rarely coincide with abnormal vessel activity. Data fusion creates a stronger, more reliable signal than either SAR or AIS alone. It forms the central decision layer that validates true spill events.

### Detection Models

The system uses a CNN to analyze SAR image patches and classify them as either spill or non-spill based on learned texture and pattern features. Isolation Forest examines AIS records to spot vessels behaving differently from the norm, such as sudden speed changes or unexpected stopping. LSTM models evaluate long-term vessel motion sequences and detect deviations from predicted behavior. Together, these models provide both visual detection and behavioral analysis. This multi-model approach enhances accuracy and enables predictive spill-risk assessment.

### Alert Engine

Once a spill is confirmed, alerts are automatically generated and sent through multiple communication channels to ensure rapid delivery. Email and SMS convey detailed notifications, while mobile push alerts reach users through connected applications. Dashboard updates provide live visualization for monitoring centers, and maritime-standard channels like VHF radio and AIS broadcasts warn nearby vessels. Satellite Short Burst Data ensures that alerts reach authorities even in remote ocean regions with no network coverage. This redundancy guarantees timely awareness and response.

## Algorithms Used

### AIS Anomaly Detection

Isolation Forest detects abnormal vessel trajectories, LSTM models analyze motion patterns over time, and rule-based filters validate vessel proximity and timing.


| Algorithm          | Purpose                                          |
| ------------------ | ------------------------------------------------ |
| Isolation Forest   | Detects abnormal patterns in vessel trajectories |
| LSTM               | Predictive vessel behavior analysis              |
| Rule-Based Filters | Validates proximity, timestamps, speed profiles  |

---

### SAR Image Classification

A CNN distinguishes spill-like textures from background ocean patterns, transfer learning improves performance across different regions, and synthetic augmentation compensates for limited spill datasets.


| Algorithm                   | Purpose                                        |
| --------------------------- | ---------------------------------------------- |
| CNN                         | Distinguishes oil spill vs non-spill regions   |
| Transfer Learning           | Adapts pre-trained models for new regions      |
| Synthetic Data Augmentation | Compensates for low spill dataset availability |

---

## Data Pipeline
### SAR Workflow

* Noise Reduction

SAR images often contain speckle noise due to the coherent nature of radar signals. Noise reduction filters smooth the image while preserving important structural details. This improves the clarity of ocean-surface patterns so the model can detect spills more accurately.

* Geometric Correction

SAR imagery is affected by distortions caused by satellite angle, Earth curvature, and terrain geometry. Geometric correction aligns the image to real-world coordinates. This ensures accurate mapping between detected spills and actual ocean locations.

* Patch Extraction

Large SAR scenes are divided into smaller image patches to make processing faster and more efficient. Each patch is analyzed independently by the CNN. This method increases precision and enables localized detection of small or early-stage spills.

* CNN Classification

A Convolutional Neural Network (CNN) examines each image patch and classifies it as “spill” or “non-spill.” The CNN learns to distinguish radar texture patterns associated with oil slicks. This automated classification is the core of the visual detection system.

### AIS Workflow

* Continuous AIS Ingestion

AIS data from vessels is streamed continuously, providing real-time updates on ship location, speed, heading, and identity. This constant flow of information allows the system to monitor vessel behavior as it happens. It forms the behavioral baseline needed for anomaly and spill-risk detection.

* Outlier Detection (Isolation Forest)

The Isolation Forest algorithm analyzes AIS movement patterns to identify vessels behaving abnormally compared to others in the region. It isolates unusual speed changes, abrupt stops, or unexpected route deviations. These anomalies often correlate with illegal discharges or suspicious maritime activity.

* Trajectory Prediction (LSTM)

An LSTM model learns temporal sequences in vessel motion to predict expected future paths and behavior. When actual movements deviate significantly from predictions, the system recognizes potential risk or pre-spill behavior. This provides early warning before visual spill evidence appears.

### Fusion Layer

A spill is confirmed only when SAR classification and AIS anomalies occur at the same location and time, ensuring high-confidence detection.

### Alert Dispatch

Alerts include:

* Coordinates
* Detected spill region
* Vessel IDs
* Confidence score
* Timestamp
  
### Alerting System

Alerts are delivered through multiple channels to maintain reliability. When networks are available, email, SMS, mobile notifications, and dashboards are used. In remote areas, VHF radio, AIS broadcasts, and satellite SBD ensure uninterrupted communication.

### Innovation & Uniqueness

The system combines SAR and AIS data to significantly reduce false positives. Predictive vessel modeling identifies risk before spills occur. Synthetic datasets improve training despite limited real examples. A serverless cloud-native structure supports global scaling. The system can integrate drone-based verification and operate on edge devices such as onboard ship computers.

##  Tech Stack

### **Languages**

* Python – Used for data processing, machine learning models, and backend automation.
* JavaScript (Dashboard) – Powers the interactive front-end visualization and real-time monitoring dashboard.

### **AI / ML**

* PyTorch – Framework for training and deploying deep learning models like CNNs and LSTMs.
* Scikit-learn – Provides algorithms such as Isolation Forest for vessel anomaly detection.
* OpenCV – Used for SAR image preprocessing, filtering, and patch extraction.
* GeoPandas – Handles geospatial data operations for mapping and spatial analysis.

### **Data Providers**

* Sentinel-1 SAR – Supplies radar imagery for detecting surface anomalies and oil slick patterns.
* MarineTraffic AIS – Provides live vessel position and movement data from coastal receivers.
* Spire Maritime AIS – Delivers global satellite-based AIS feeds for offshore and remote regions.

---

##  Future Enhancements 

###  AI-Based Spill Severity Estimation

Future versions of the system can incorporate advanced segmentation models such as U-Net or Mask R-CNN to quantify the physical characteristics of detected spills. These models would produce detailed spill boundaries, allowing accurate estimation of affected area and oil thickness variations. Severity scoring helps prioritize response resources and assess ecological impact. This enhancement transforms detection from a binary alert into a full analytical assessment.

###  Spill Drift & Weather Forecasting

Integrating environmental data—such as wind fields, tide models, and ocean currents—would enable the system to predict how a spill will move over time. Drift forecasting provides early insight into which coastlines or marine habitats are at risk. Combining live meteorological feeds with fluid dynamics modeling supports better decision-making for containment and cleanup operations. This feature strengthens the system’s value during multi-day spill events.

Integrate:

* Wind fields
* Tide models
* Ocean currents

###  Blockchain Event Logging

A blockchain-backed logging system would store spill events, vessel activity, and detection timestamps in a secure, tamper-proof ledger. This ensures that all evidence related to an incident remains verifiable for legal, regulatory, and insurance purposes. Immutable records improve transparency and accountability for vessels operating in sensitive waters. Such a system strengthens compliance with international maritime environmental standards.

###  Federated Learning Support

Federated learning would allow different maritime agencies or countries to collaboratively improve detection models without sharing raw data. Each participant trains on their own datasets locally, contributing only model updates. This preserves data privacy and meets security requirements while still improving global model performance. It is especially useful for regions with restricted AIS or SAR data access.

###  On-Vessel Edge AI

Deploying lightweight CNN and AIS anomaly models directly on vessels would enable real-time, onboard detection without relying on cloud connectivity. Ships could receive immediate alerts about risky behavior or nearby spills, improving safety and situational awareness. Edge inference also reduces latency and allows monitoring even in bandwidth-limited regions. This feature expands the system’s usability beyond centralized control centers.

---

## Figures 

<img width="279" height="803" alt="image" src="https://github.com/user-attachments/assets/9f878d84-9e0b-4ba2-afb8-8aa28a974bf6" />

* Sentinel-1 SAR example scene 
<img width="516" height="251" alt="image" src="https://github.com/user-attachments/assets/15eb7f64-8880-49a7-84ff-92bbf8c33b80" />

* Satellite SBD block diagram 
<img width="508" height="227" alt="image" src="https://github.com/user-attachments/assets/14ad7017-2a04-456d-985f-64038d46ed1e" />

* Model Output
### Chennai Coast
![WhatsApp Image 2025-11-28 at 14 36 00](https://github.com/user-attachments/assets/2aab5b81-f739-421d-9f3c-32a41fcd6990)

### San Francisco Coast
<img width="411" height="512" alt="image" src="https://github.com/user-attachments/assets/9854ae0c-2254-4de8-8572-690fe76b2065" />


![WhatsApp Image 2025-11-27 at 14 57 34](https://github.com/user-attachments/assets/d165efe6-59bc-47a1-b161-3f4fec6d1d75)


---


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




