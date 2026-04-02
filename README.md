# Reproduction Report: IoT Device Identification and Classification Models

![Python](https://img.shields.io/badge/Python-3.12%2B-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![Dataset](https://img.shields.io/badge/Dataset-ToN__IoT-green)

## 1. Project Overview
This project reproduces several state-of-the-art IoT device identification and classification models using the **ToN_IoT dataset**. The objective is to evaluate the effectiveness of different network traffic characteristic-based approaches (Statistical, Behavioral, and Semantic) in identifying devices and detecting vulnerabilities.

## 2. Models Covered
This repository contains the reproduction of the following models:
1. **Pinheiro et al.** - Lightweight statistical model based on packet length (1-second window)

2. **Meidan et al.** - Vulnerable device detection model that penetrates NAT (DeNAT)

3. **Okui et al.** - Service aggregation model based on IPFIX flow records

4. **Sivanathan et al.** - Behavioral profiling model based on long-cycle traffic characteristics

5. **Yang et al.** - Automated semantic fingerprinting model for cyberspace (DPI)

6. **Fan et al.** - Semi-supervised incremental update model for the open world (AutoIoT)
## 3. Environment Setup
To run the reproduction notebooks, ensure you have Python 3.12 installed.

### Installation
1. Clone the repository:
   ```bash
   git clone [https://github.com/001mol264561-jpg/IoT-Reproduction.git](https://github.com/001mol264561-jpg/IoTReproduction.git)
   cd IoT-Reproduction

2. Create a virtual environment and install dependencies
   ```bash  
   conda create -n iot_reproduce python=3.12
   conda activate iot_reproduce
   pip install -r requirements.txt
   
## 4. Dataset preparation
Due to storage capacity, this project does not include the original dataset. Please go to the official ToN_IoT platform to download the data.
https://research.unsw.edu.au/projects/toniot-datasets

## 5. Reproduction Guide
Enter the directory, interactively open the corresponding notebook and run it. Each notebook contains detailed Markdown comments that break down the steps of feature engineering and model evaluation.
| Notebook | Core Technology Path | feature |
|---|---|---|
| 01_meidan_denat | IP Blinding+LightGBM Stream Level Classification | Accurately identify internal vulnerable assets through NAT |
| 02_Okui_IPFIX_Aggregation | 15 minute window+business port expansion | High Interpretability |
| 03_Sivanathan_Behavioral_Profiling | Sleep cycle calculation | Identify high imitation/similar devices through long-term behavioral image recognition |
| 04_Pinheiro_Packet_Length | 1-second window statistics+random forest | Anti encryption, precise and lightweight, millisecond response |
| 05_Yang_Semantic | Pyshark(DPI) + TF-IDF + MLP | Identifying specific manufacturers and models |
| 06_Fan_AutoIoT_SemiSupervised | CNN extraction+KS test | Automatically discover new devices, Semi-supervised evolution |



