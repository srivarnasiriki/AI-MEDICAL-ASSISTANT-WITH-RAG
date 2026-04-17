# 🏥 AI Medical Assistant — Complete Project

A full-stack medical AI platform with:
- **RAG Chat** — Ask medical questions, get cited answers from your documents
- **ML Training** — Train a patient risk classifier with 3 algorithms
- **ML Testing** — Batch evaluation + single patient risk prediction

---

## ⚡ Quick Start (4 Steps)

### Step 1 — Get a Free Groq API Key
1. Go to **https://console.groq.com** (free, no credit card needed)
2. Sign up and click **"Create API Key"**
3. Copy the key (starts with `gsk_...`)

### Step 2 — Set Your API Key
Open the `.env` file in the project folder and paste your key:
```
GROQ_API_KEY=gsk_your_actual_key_here
```

### Step 3 — Install Dependencies
```bash
python -m venv venv

# Windows:
venv\Scripts\activate

# Mac/Linux:
source venv/bin/activate

pip install -r requirements.txt
```

### Step 4 — Run
```bash
python app.py
```

Then open **http://localhost:5000** in your browser. ✅

---

## 📁 Project Structure

```
ai-medical-assistant/
├── app.py                          ← Flask backend (RAG + ML)
├── requirements.txt                ← Python packages
├── .env                            ← PUT YOUR API KEY HERE
├── .env.example                    ← Template for .env
├── templates/
│   └── index.html                  ← Frontend UI (3 tabs)
├── static/
│   ├── css/style.css               ← Dark theme styles
│   └── js/script.js                ← All frontend logic
└── data/
    └── medical_knowledge_base.txt  ← Medical knowledge (RAG source)
```

---

## 💬 Features

### Tab 1: Medical Chat (RAG)
- Type any medical question
- System retrieves top-4 relevant chunks from FAISS vector store
- Llama 3 (via Groq) generates a grounded answer with citations
- Click "Show sources" to see retrieved knowledge chunks

### Tab 2: Train Model
- Preview the synthetic medical dataset (up to 5000 patients)
- Choose: Random Forest / Gradient Boosting / Logistic Regression
- See accuracy, cross-validation scores, feature importance, confusion matrix

### Tab 3: Test & Predict
- **Predict**: Enter patient vitals → get Low/Medium/High risk prediction
- **Batch Test**: Evaluate model on 50–1000 synthetic patients
- Quick presets: Low Risk / Medium Risk / High Risk patient profiles

---

## 🧠 ML Model Details

**Dataset**: Synthetic patients with:
- Age, BMI, Blood Pressure, Glucose, Cholesterol, Heart Rate
- Smoking status, Diabetes history
- Labels: Low / Medium / High risk

**Algorithms**:

| Algorithm | Notes |
|---|---|
| Random Forest | Best overall accuracy (~92%) |
| Gradient Boosting | Highest precision |
| Logistic Regression | Fastest, most interpretable |

**API Endpoints**:

| Endpoint | Method | Description |
|---|---|---|
| `/ask` | POST | RAG medical chat |
| `/ml/train` | POST | Train risk classifier |
| `/ml/predict` | POST | Predict single patient risk |
| `/ml/test` | POST | Batch evaluation |
| `/ml/history` | GET | Training run history |
| `/ml/dataset-preview` | GET | Preview dataset |
| `/health` | GET | Server health check |
| `/rebuild-index` | POST | Rebuild FAISS index |

---

## 🔧 Troubleshooting

| Problem | Fix |
|---|---|
| "Invalid Groq API key" | Check .env file — key must start with gsk_ |
| Chat says "Offline" | Make sure python app.py is running |
| Slow first startup | Normal — downloads embedding model (~90MB) once |
| faiss install error | Use pip install faiss-cpu==1.7.4 with numpy < 2.0 |
| Port 5000 in use | Change in app.py: app.run(port=5001) |

---

## ⚠️ Disclaimer
Educational purposes only. Not a substitute for professional medical advice.
