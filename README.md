# RentVerse AI Service

Layanan AI/ML microservice yang menyediakan kecerdasan buatan untuk ekosistem RentVerse, khususnya dalam prediksi harga properti.

## 🤖 Fitur Utama

- **Prediksi Harga Sewa:** Menggunakan algoritma Machine Learning (Random Forest) untuk merekomendasikan harga sewa harian yang optimal berdasarkan fitur properti.
- **Preprocessing Data:** Pipeline otomatis untuk normalisasi data.
- **Model API:** REST API cepat berbasis FastAPI.
- **Health Check:** Endpoint monitoring kesehatan service.

## 🛠️ Teknologi Stack

- **Framework:** FastAPI (Python)
- **ML Library:** scikit-learn, pandas, numpy
- **Server:** Uvicorn
- **Containerization:** Docker

## 🚀 Cara Menjalankan

### Opsi 1: Menggunakan Docker (Direkomendasikan)

**Prasyarat:**
- Docker & Docker Compose terinstall.

**Langkah:**

1. **Masuk ke direktori AI:**
   ```bash
   cd rentverse-ai-service
   ```

2. **Jalankan Container:**
   ```bash
   docker-compose up -d --build
   ```

3. **Verifikasi:**
   Service akan berjalan di `http://localhost:8000`.
   Cek health status: `http://localhost:8000/api/v1/health`

### Opsi 2: Manual (Python Venv)

**Prasyarat:**
- Python 3.12+
- pip

**Langkah:**

1. **Buat Virtual Environment:**
   ```bash
   python -m venv venv
   source venv/bin/activate  # Atau venv\Scripts\activate di Windows
   ```

2. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Jalankan Server:**
   ```bash
   uvicorn main:app --reload --host 0.0.0.0 --port 8000
   ```

### Dokumentasi API

Swagger UI tersedia di:
👉 **http://localhost:8000/docs**

## 📁 Struktur Direktori

```
rentverse-ai-service/
├── rentverse/          # Main package logic
├── Dockerfile          # Config Docker image
├── docker-compose.yml  # Config Docker service
├── main.py             # Entry point FastAPI
└── requirements.txt    # Python deps
```

## 📡 Integrasi

Service ini diakses oleh **Backend Service** via HTTP request.
Pastikan `AI_SERVICE_URL` di konfigurasi Backend mengarah ke:
- `http://rentverse-ai-service:8000` (jika dalam network Docker yang sama)
- `http://localhost:8000` (jika berjalan local host-to-host)

---
Happy Coding! 🚀
