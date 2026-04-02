# IoT-Reproduction
# Reproduction Report: IoT Device Identification and Classification Models

![Python](https://img.shields.io/badge/Python-3.12%2B-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![Dataset](https://img.shields.io/badge/Dataset-ToN__IoT-green)

## 1. Project Overview
This project reproduces several state-of-the-art IoT device identification and classification models using the **ToN_IoT dataset**. The objective is to evaluate the effectiveness of different network traffic characteristic-based approaches (Statistical, Behavioral, and Semantic) in identifying devices and detecting vulnerabilities.

## 2. Models Covered
This repository contains the reproduction of the following models:
* **Statistical Analysis (Pinheiro et al.):** Identifying devices based on packet length statistics from encrypted traffic.
* **DeNAT (Meidan et al.):** Detecting vulnerable IoT devices hidden behind a home NAT using flow-level metadata.
* **Behavioral Profiling (Sivaraman et al.):** Classifying devices using long-term network traffic characteristics (Activity cycles, ports, etc.).
* **IPFIX Records (Okui et al.):** Identifying device models in home domains using service-based aggregation of flow records.

## 3. Environment Setup
To run the reproduction notebooks, ensure you have Python 3.12 installed.

### Installation
1. Clone the repository:
   ```bash
   git clone [https://github.com/001mol264561-jpg/IoT-Reproduction.git](https://github.com/001mol264561-jpg/IoTReproduction.git)
   cd IoT-Reproduction
