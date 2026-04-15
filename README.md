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
### 01_meidan_denat
1. Run [`01_meidan_denat/aucpr.ipynb`](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/01_meidan_denat/aucpr.ipynb) to observe the benchmark performance.
2. Run [`01_meidan_denat/idle mix active.ipynb`](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/01_meidan_denat/idle%20mix%20active.ipynb) to observe the stability of the model under dynamic behavior.
#### Programming Logic
1. After loading the dataset, the code immediately performs a "blinding" process, removing strong identifying features such as src_ip, dst_ip, src_port, and dst_port. This forces the model to learn traffic behavior patterns.
2. Stream-level metadata was selected: duration, src_bytes, dst_bytes, src_pkts, dst_pkts, as well as service and proto.
3. In idle mix active.ipynb, we mix traffic from different lifecycles of the device to verify whether the model can penetrate state interference and accurately pinpoint the device model.
#### Results   
1. In binary classification tasks (normal vs. fragile), the model's AUCPR on the test set typically exceeds 0.95.
2. When identifying specific device models, the accuracy rate remains above 90%, even when behind NAT and with the IP address hidden.

### 02_Okui_IPFIX_Aggregation
[`02_Okui_IPFIX_Aggregation/aucpr+idle mix active.ipynb`](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/02_Okui_IPFIX_Aggregation/aucpr%2Bidle%20mix%20active.ipynb)
#### Programming Logic
1. The code first maps network traffic to specific service types based on the target port (dst_port) and protocol.
2. Grouping and aggregating by [time window, source IP, service type], the statistics (maximum, minimum, mean, sum) of packet count and byte count for each service are calculated. Then, the service type is pivoted as a column to generate a highly interpretable feature matrix of hundreds of dimensions, such as DNS_src_bytes_sum.
#### Results
![image/IDLE ACTIVE MIX.png](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/image/IDLE%20ACTIVE%20MIX.png) 
![image/Reproduced AUCPR.png](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/image/Reproduced%20AUCPR.png)

### 03_Sivanathan_Behavioral_Profiling
[`03_Sivanathan_Behavioral_Profiling/Sivanathan.ipynb`](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/03_Sivanathan_Behavioral_Profiling/Sivanathan.ipynb)
#### Programming Logic
1. Calculate the time difference between two adjacent streams to generate the Sleep Time feature.
2. The number of unique ports (dst_port_nunique) and specific signaling frequencies within the statistics window.
#### Results
![image/3.1.jpg](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/image/3.1.jpg) 
![image/3.2.jpg](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/image/3.2.jpg)
![image/3.3.jpg](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/image/3.3.jpg)

### 04_Pinheiro_Packet_Length
[`04_Pinheiro_Packet_Length/AUCPR+IDLE MIX ACTIVE.ipynb`](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/04_Pinheiro_Packet_Length/AUCPR%2BIDLE%20MIX%20ACTIVE.ipynb)
#### Programming Logic
1. Strictly slice the timestamps in 1-second windows.
2. Within one second, only four core dimensions are extracted: total number of packets, total number of bytes, mean packet length, and standard deviation of packet length (Std Dev). These are then fed into the random forest model.
#### Results
![image/4.jpg](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/image/4.jpg)

### 05_Yang_Semantic
1. AUCPR: [`05_Yang_Semantic/test4.ipynb`](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/05_Yang_Semantic/test4.ipynb)
2. Dynamic life cycle assessment: [`05_Yang_Semantic/idle mix active.ipynb`](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/05_Yang_Semantic/idle%20mix%20active.ipynb)
#### Programming Logic
1. GroupShuffleSplit is used to split the network according to Groups to ensure that the model encounters truly "unseen" network states on the test set.
2. When the validation set loss (val_loss) stops decreasing, the learning rate is automatically halved (factor=0.5) to help the model escape local optima in the complex high-dimensional fingerprint space.
3. During training, class_weight is passed to model.fit to force the neural network to focus on the "minority" devices with a very small traffic share.
#### Results
![image/5.jpg](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/image/5.jpg)

### 06_Fan_AutoIoT_SemiSupervised
[`06_Fan_AutoIoT_SemiSupervised/Fan.ipynb`](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/06_Fan_AutoIoT_SemiSupervised/Fan.ipynb)
#### Programming Logic
1. Instead of using fully labeled training data, the code deliberately masks 92% of the training labels. It creates a scenario where only 8% of the data is labeled (X_L), and the vast majority remains unlabeled (X_U). This perfectly mimics a dynamic IoT environment where new, unlabeled traffic constantly flows in.
2. The model (AutoIoTClassifier) treats the statistical feature vector as a 1D sequence and uses a Convolutional Neural Network (Conv1D and MaxPool1D) backbone to extract a high-dimensional latent representation ($Z$). The network then splits into two multi-task branches:
   1. Head 1 (Specific IoT Classes): A multi-class output for pinpointing specific device types or behaviors.   
   2. Head 2 (Binary/Broad Category): A binary output.
4. To utilize the 92% unlabeled data, the code implements a CCLP (Consistent Classification with Label Propagation) loss mechanism:
   1. It calculates cosine similarities (compute_H) between the latent representations of labeled and unlabeled data in each batch.
   2. It performs graph-based label propagation (label_propagation_FU) to automatically assign "pseudo-labels" to the unlabeled data based on their distance to the labeled data.
   3. It computes a specialized CCLP loss that forces the neural network's predictions for the unlabeled data to align with these pseudo-labels.  
#### Results
![image/6.jpg](https://github.com/001mol264561-jpg/IoT-Reproduction/blob/9de009ac544ec0ada7eb0a30647398b9769ecb21/image/6.jpg)

## Compare
| Notebook | Core Technology Path | feature |
|---|---|---|
| 01_meidan_denat | IP Blinding+LightGBM Stream Level Classification | Accurately identify internal vulnerable assets through NAT |
| 02_Okui_IPFIX_Aggregation | 15 minute window+business port expansion | High Interpretability |
| 03_Sivanathan_Behavioral_Profiling | Sleep cycle calculation | Identify high imitation/similar devices through long-term behavioral image recognition |
| 04_Pinheiro_Packet_Length | 1-second window statistics+random forest | Anti encryption, precise and lightweight, millisecond response |
| 05_Yang_Semantic | Pyshark(DPI) + TF-IDF + MLP | Identifying specific manufacturers and models |
| 06_Fan_AutoIoT_SemiSupervised | CNN extraction+KS test | Automatically discover new devices, Semi-supervised evolution |



