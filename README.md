# 🌐 Network Traffic Classification Engine

> Classifying network traffic by application/site using 
> Machine Learning — replicating SD-WAN application 
> visibility using Random Forest

---

## 🔍 Problem Statement

Enterprise SD-WAN systems need to identify what application 
or site a user is accessing — to apply smart routing, 
QoS policies, and security rules.

This is traditionally done by expensive hardware (DPI).

This project replicates that capability using Machine Learning 
on network flow data.

---

## 📊 Results

| Metric | Value |
|--------|-------|
| Model | Random Forest |
| Accuracy | 90% |
| Features Used | Packet Size, Flow Duration |
| Dataset | Kaggle Network Flow Dataset |

---

## 🛠️ Tech Stack

- Python 3.x
- Scikit-learn
- Pandas
- Matplotlib / Seaborn
- Jupyter Notebook

---

## 📁 Project Structure
```
network-traffic-classifier/
├── notebook/
│   └── traffic_classifier.ipynb
├── data/
│   └── README.md
├── results/
│   └── confusion_matrix.png
├── requirements.txt
└── README.md
```

## ▶️ How to Run

1. Clone the repository
git clone https://github.com/[yourusername]/network-traffic-classifier

2. Install dependencies
pip install -r requirements.txt

3. Open Jupyter Notebook
jupyter notebook notebook/traffic_classifier.ipynb


---

## 📈 Key Findings

- Flow duration was the strongest predictor of traffic category
- Random Forest outperformed baseline Logistic Regression
- Model classifies [X] application/site categories

---

## 🔗 How This Connects to SD-WAN

In real SD-WAN systems:
- Application visibility identifies traffic type
- Policies route traffic based on application
- QoS rules prioritize critical apps

This model automates the **identification step** using ML
instead of manual DPI signatures.

---

## 🚀 Future Improvements

- [ ] Add real-time packet capture using Scapy
- [ ] Build Streamlit dashboard for live demo
- [ ] Compare XGBoost vs Neural Network
- [ ] Integrate with SD-WAN controller API

---

## 👤 Author

Hanmant Motade — Network Engineer | SD-WAN | AIOps  
www.linkedin.com/in/hmotade
