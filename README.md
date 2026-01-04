# RentVerse AI Service

Layanan AI/ML microservice yang menyediakan kecerdasan buatan untuk ekosistem RentVerse, khususnya dalam prediksi harga properti.

## 🤖 Fitur Utama

- **Prediksi Harga Sewa:** Menggunakan algoritma Machine Learning (Random Forest) untuk merekomendasikan harga sewa harian yang optimal berdasarkan fitur properti (lokasi, jumlah kamar, luas, dll).
- **Preprocessing Data:** Pipeline otomatis untuk membersihkan dan normalisasi data input.
- **Model API:** REST API cepat berbasis FastAPI untuk melayani request prediksi.

## 🛠️ Teknologi Stack

- **Framework:** FastAPI (Python)
- **ML Library:** scikit-learn, pandas, numpy, joblib
- **Server:** Uvicorn
- **Containerization:** Docker support

## 🚀 Cara Menjalankan

### Prasyarat
- Python 3.12 atau lebih baru
- pip (Python package manager)

### Instalasi & Setup Lokal

1. **Masuk ke direktori AI:**
   ```bash
   cd rentverse-ai-service
   ```

2. **Buat Virtual Environment (Recommended):**
   ```bash
   # Windows
   python -m venv venv
   venv\Scripts\activate

   # macOS/Linux
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Konfigurasi Environment:**
   Salin `.env.example` ke `.env`.
   ```bash
   cp .env.example .env
   ```
   Biasanya konfigurasi default sudah cukup untuk development lokal.

5. **Train Model (Jika diperlukan):**
   Jika file model `.pkl` belum ada atau ingin di-update:
   *(Script training biasanya tersedia di folder `notebooks` atau script terpisah, pastikan model tersimpan di `rentverse/models/`)*

6. **Jalankan Server:**
   ```bash
   uvicorn main:app --reload --host 0.0.0.0 --port 8000
   ```
   
   Server akan aktif di `http://localhost:8000`.

### Dokumentasi API

Cek endpoint yang tersedia dan coba langsung via Swagger UI bawaan FastAPI:
👉 **http://localhost:8000/docs**

## 📁 Struktur Direktori

```
rentverse-ai-service/
├── rentverse/
│   ├── models/             # File model ML (.pkl)
│   ├── routers/            # Defines API routings
│   ├── schemas/            # Pydantic models (Request/Response schemas)
│   ├── services/           # Logic ML dan prediksi
│   └── core/               # Config dan settings
├── main.py                 # Entry point aplikasi FastAPI
├── requirements.txt        # Python dependencies
└── .env.example            # Template environment variables
```

## 📡 Integrasi

Service ini diakses oleh **Backend Service** (bukan langsung oleh Mobile App). Backend akan mengirim request HTTP ke AI Service saat user atau landlord meminta rekomendasi harga.

Contoh payload request:
```json
POST /api/v1/predict/price
{
  "latitude": -6.2088,
  "longitude": 106.8456,
  "bedrooms": 2,
  "bathrooms": 1,
  "surface_area": 45,
  "property_type": "apartment"
}
```

---
Happy Coding! 🚀
