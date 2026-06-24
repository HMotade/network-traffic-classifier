<<<<<<< HEAD
# Network Traffic Classifier — Streamlit Dashboard

A 3-tab dashboard (EDA → Model Performance → Live Prediction) built from
your `packet_classification_improved.ipynb` notebook. The ML logic is
unchanged — this just wraps it in a UI.

## How it fits together

```
export_artifacts.py   →   artifacts/          →   app.py
(run once, trains      (model.pkl, scaler.pkl,   (Streamlit dashboard,
 the model — same       metadata.json,            loads artifacts,
 logic as your           eda_sample.csv)           no training)
 notebook)
```

The app never trains a model — it just loads what `export_artifacts.py`
saved. This keeps the app fast to start and avoids re-downloading the
344k-row dataset every time someone opens it.

## Setup

```bash
pip install -r requirements.txt
```

## Step 1 — Generate the artifacts (run once)

```bash
python export_artifacts.py
```

This downloads the UCDavis QUIC dataset via `kagglehub` (same as your
notebook — make sure your Kaggle credentials are set up, e.g.
`~/.kaggle/kaggle.json` or the `KAGGLE_USERNAME` / `KAGGLE_KEY` env vars),
trains the Random Forest with the same `GridSearchCV` settings as the
notebook, and writes everything the app needs into `./artifacts/`:

- `model.pkl` — the trained Random Forest pipeline
- `scaler.pkl` — the fitted `StandardScaler`
- `metadata.json` — accuracy, confusion matrix, feature importances, class names
- `eda_sample.csv` — a 20k-row sample of the dataset for the EDA charts

This step takes a few minutes (dataset download + GridSearchCV). You only
need to re-run it if you change the model or want to refresh on new data.

## Step 2 — Run the app

```bash
streamlit run app.py
```

Opens at `http://localhost:8501`. Three tabs in the sidebar:

- **📊 EDA** — class distribution, packet size & time delta distributions
- **🧠 Model Performance** — accuracy, confusion matrix, feature importance, per-class report
- **🔮 Live Prediction** — sliders for `packet_size` / `time_delta`, instant prediction + simulated SD-WAN routing decision, with one-click traffic-type presets

## Deploying it

Once it runs locally, the easiest free hosting is
[Streamlit Community Cloud](https://streamlit.io/cloud):

1. Push this folder (including the `artifacts/` directory — commit the
   `.pkl`/`.json`/`.csv` files, they're small) to a GitHub repo.
2. Connect the repo at share.streamlit.io, point it at `app.py`.
3. Done — no need to run `export_artifacts.py` on the server, since the
   trained artifacts are already committed.

If you'd rather not commit binary model files to git, you can instead
have the Streamlit Cloud app run `export_artifacts.py` on first boot
(add it to a `@st.cache_resource`-wrapped startup function) — but that
requires Kaggle credentials as Streamlit Cloud secrets and adds a few
minutes to cold start.

## Notes

- Only `time_delta` and `packet_size` are used as model features —
  matching your notebook's EDA conclusion that `timestamp` and
  `direction` weren't useful.
- The routing policy in the Live Prediction tab mirrors the
  `routing_policy` dict from your notebook's final demo cell.
- If you tweak the model (different algorithm, new features), only
  `export_artifacts.py` needs to change — `app.py` reads whatever is in
  `metadata.json`, so it adapts automatically as long as the keys stay
  the same.
=======
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
>>>>>>> 649543d005997d7028a815ea825653717e616f41
