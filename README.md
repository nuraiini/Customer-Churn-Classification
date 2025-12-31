# 📉 Customer Churn Prediction  
**Strategic Retention Analysis with Machine Learning**

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat&logo=python)
![Scikit-Learn](https://img.shields.io/badge/Library-Scikit--Learn-orange?style=flat&logo=scikitlearn)
![Pandas](https://img.shields.io/badge/Library-Pandas-150458?style=flat&logo=pandas)
![Status](https://img.shields.io/badge/Status-Completed-success)

---

## 📌 Project Overview
Dalam bisnis berbasis langganan (*subscription-based business*), mempertahankan pelanggan lama jauh lebih efisien dari sisi biaya dibandingkan mengakuisisi pelanggan baru.  
Proyek ini bertujuan membangun model **Machine Learning** untuk memprediksi **Customer Churn** serta mengidentifikasi faktor utama penyebab pelanggan berhenti berlangganan.

### ⚠️ Tantangan Utama
Dataset memiliki **class imbalance ekstrem**, di mana hanya **10.2% pelanggan yang churn**.  
Model prediksi konvensional cenderung bias ke kelas mayoritas (*non-churn*). Oleh karena itu, proyek ini menekankan pendekatan **cost-sensitive learning** dan evaluasi berbasis **Recall** serta **ROC-AUC**, bukan sekadar akurasi.

---

## 📂 Business Understanding
- **Objective**  
  Mendeteksi pelanggan berisiko tinggi sedini mungkin untuk memungkinkan intervensi proaktif.

- **Target Variable**  
  `Churn`  
  - `1` = Berhenti berlangganan  
  - `0` = Tetap berlangganan  

- **Key Metrics**  
  - Recall (Churn)  
  - ROC-AUC Score  

---

## ⚙️ Methodology (End-to-End Workflow)

### 1️⃣ Data Cleaning & Preprocessing
- **Missing Values**  
  Nilai kosong pada kolom `complaint_type` diisi dengan kategori **"No Complaint"**.
- **Non-Predictive Features**  
  Kolom `customer_id` dihapus untuk mencegah overfitting berbasis identitas.

---

### 2️⃣ Exploratory Data Analysis (EDA)
Pola penting yang ditemukan:

| Faktor | Hubungan dengan Churn |
|------|-----------------------|
| `payment_failures` | Positif (+0.11) |
| `last_login_days_ago` | Positif |
| `csat_score` | Negatif (-0.15) |
| `tenure_months` | Negatif |

---

### 3️⃣ Modeling Strategy
Model utama yang digunakan adalah **Random Forest Classifier** dengan pendekatan **cost-sensitive learning** untuk menangani data tidak seimbang.

```python
RandomForestClassifier(
    n_estimators=100,
    max_depth=10,
    class_weight="balanced",
    random_state=42
)
```

---
**Penjelasan Teknis:**  
Parameter `class_weight="balanced"` memberikan penalti lebih besar saat model gagal mendeteksi kelas minoritas (*churn*), sehingga meningkatkan sensitivitas model terhadap pelanggan berisiko tinggi.

---

## 📊 Model Evaluation

Evaluasi model difokuskan pada kemampuan mendeteksi pelanggan **Churn**, bukan hanya akurasi keseluruhan.

| Metric | Score | Interpretasi |
|------|------|-------------|
| **ROC-AUC** | **0.79** | Model memiliki kemampuan diskriminasi yang baik |
| **Accuracy** | **85%** | Tinggi, namun bias ke kelas mayoritas |
| **Recall (Churn)** | **34%** | Model mampu menangkap 34% pelanggan churn |
| **Precision (Churn)** | **29%** | 29% prediksi churn benar-benar churn |

**Catatan:**  
Recall masih dapat ditingkatkan melalui **threshold tuning** sesuai kebutuhan bisnis.

---

## 💡 Key Business Insights

Berdasarkan analisis **Feature Importance**, diperoleh tiga faktor utama penyebab churn:

### 1️⃣ Payment Failures (Masalah Teknis)
Merupakan prediktor paling kuat.  
Banyak pelanggan berhenti bukan karena tidak puas, melainkan karena kegagalan pembayaran seperti kartu kedaluwarsa atau error sistem.

### 2️⃣ Low CSAT Score (Ketidakpuasan Pelanggan)
Skor kepuasan pelanggan berbanding terbalik dengan risiko churn.  
Semakin rendah CSAT, semakin besar kemungkinan pelanggan berhenti.

### 3️⃣ Early Tenure (Pelanggan Baru)
Risiko churn tertinggi terjadi pada **1–3 bulan pertama** berlangganan.  
Pelanggan dengan masa langganan panjang cenderung lebih loyal.

---

## 📢 Business Recommendations (Action Plan)

### 🔹 1. Optimasi Sistem Billing (Prioritas Utama)
- Notifikasi pembayaran otomatis (Email / WhatsApp) **3 hari sebelum jatuh tempo**
- Fitur **Retry Payment** yang mudah diakses setelah transaksi gagal

### 🔹 2. Program Onboarding Intensif
- Fokus pada pelanggan dengan **tenure < 3 bulan**
- Edukasi produk dan pendampingan awal untuk meningkatkan engagement

### 🔹 3. Percepat Penanganan Komplain
- Prioritaskan tiket pelanggan berisiko tinggi
- Menjaga skor CSAT tetap tinggi

---

## 🛠️ Tools & Libraries

- **Language:** Python 3.10  
- **Libraries:**  
  - Pandas  
  - NumPy  
  - Scikit-Learn  
  - Matplotlib  
  - Seaborn

---
## 🚀 How to Run

1. Clone repository:
```bash
git clone https://github.com/username/customer-churn-prediction.git
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```


3. Jalankan notebook:
```bash
notebooks/customer_churn_model.ipynb
```

## 📬 Contact

Dibuat oleh **Nur'aini**  
🔗 LinkedIn: https://www.linkedin.com/in/nuraiinii01

