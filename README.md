# IoT-Reproduction
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


#### Reproduction Guide
笔记本文件,核心技术路径,亮点/解决的痛点
04_Pinheiro_Packet_Length.ipynb,1秒窗口统计+随机森林,抗加密，精准轻量，毫秒级响应。
01_Meidan_DeNAT.ipynb,IP盲化+LightGBM流级分类,通过NAT，精准识别内部脆弱资产。
02_Okui_IPFIX_Aggregation.ipynb,15分钟窗口 + 业务端口展开,强解释性，对设备小巩固增强免疫力。
03_Sivanathan_Profiling.ipynb,1小时窗口+休眠周期计算,通过长期行为图像识别高仿/相似设备。
05_Yang_Semantic_Fingerprinting.ipynb,Pyshark(DPI) + TF-IDF + MLP,细粒度极高，识别具体到制造商和型号。
06_Fan_AutoIoT_SemiSupervised.ipynb,CNN提取+ KS检验,自动发现新设备，半监督引人注目的自演进。
