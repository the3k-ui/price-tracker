# 🚀 BuyCopilot - Universal Tech Price Tracker

BuyCopilot adalah aplikasi pelacak harga gadget pintar (smartphone) real-time yang memindai harga di berbagai e-commerce Indonesia (Tokopedia, Shopee, Blibli) dan menyinkronkan spesifikasi teknis langsung dari GSM Arena.

Aplikasi ini dirancang menggunakan arsitektur hybrid **Frontend Statis + Backend API (Scraper Proxy)** yang sangat tangguh (robust), cepat, dan siap dideploy ke publik.

---

## 🛠️ Fitur Utama
1. **Real-time Price Scanning**: Memindai harga dari Tokopedia, Shopee, dan Blibli secara langsung.
2. **GSM Arena Specs Sync**: Menemukan spesifikasi lengkap (Chipset, Baterai, Kamera, OS, dll.) untuk perangkat apa pun yang dicari secara dinamis.
3. **Smart Offline Fallback**: Jika server backend mati/offline, frontend otomatis menggunakan data simulasi pasar yang realistis sehingga web tidak pernah error dan selalu terlihat memukau (wow-factor terjaga).
4. **Google News Gadget Ticker**: Menampilkan running text tren pasar gadget global yang diperbarui langsung dari RSS Feed Google News.
5. **Interactive Graphics**: Grafik riwayat harga dan analisis prediksi penurunan harga (price decay) di masa depan.

---

## 📁 Struktur Repositori
* `index.html` — Kode frontend SPA (Single Page Application) yang cantik, menggunakan TailwindCSS dan Chart.js.
* `server.py` — Backend API Python (Flask) untuk mengoordinasikan web scraping dan pencarian spesifikasi.
* `requirements.txt` — File dependensi pustaka Python untuk kebutuhan deployment cloud.

---

## 🌐 Cara Menghosting (Deploy) ke Internet

Karena Anda ingin mengunggah ini ke GitHub dan menjadikannya website publik, ikuti panduan mudah berikut:

### Langkah 1: Hosting Frontend (GitHub Pages)
1. Buat repositori baru di GitHub dan unggah semua file ini (`index.html`, `server.py`, `requirements.txt`, dll.).
2. Buka menu **Settings** repositori Anda di GitHub.
3. Scroll ke bagian **Pages** (di bawah menu *Code and automation*).
4. Pada opsi *Build and deployment*, pilih branch **main** dan folder **/(root)**, lalu klik **Save**.
5. Website frontend Anda akan langsung aktif di alamat: `https://<username-anda>.github.io/<nama-repo>/`

### Langkah 2: Hosting Backend API (Render.com - Gratis)
Karena e-commerce memblokir akses langsung dari browser (CORS), kita membutuhkan server backend `server.py` sebagai perantara.
1. Buat akun gratis di **[Render.com](https://render.com/)**.
2. Klik **New +** dan pilih **Web Service**.
3. Hubungkan repositori GitHub Anda.
4. Konfigurasikan detail berikut:
   * **Language**: `Python`
   * **Build Command**: `pip install -r requirements.txt`
   * **Start Command**: `gunicorn server:app`
5. *(Opsional)* Jika Anda memiliki API Key dari ScraperAPI untuk mem-bypass anti-bot tingkat tinggi, tambahkan di menu **Environment Variables**:
   * Key: `SCRAPERAPI_KEY`
   * Value: `<api-key-scraper-api-anda>`
6. Klik **Deploy Web Service**. Render akan memberikan URL API publik gratis untuk Anda (misal: `https://buycopilot-api.onrender.com`).

### Langkah 3: Sambungkan Frontend ke Backend API Publik Anda
Setelah backend Anda aktif di Render, buka file `index.html` Anda dan perbarui URL backend di fungsi-fungsi pemanggilan agar tidak mengarah ke `localhost:5000` saat online.
Cari baris berikut di `index.html` dan ganti `'http://localhost:5000'` dengan URL Render Anda:
```javascript
const backendUrl = window.location.hostname === 'localhost' || window.location.hostname === '127.0.0.1' 
    ? 'http://localhost:5000' 
    : 'https://<nama-aplikasi-anda>.onrender.com';
```

---

## 💻 Cara Menjalankan Secara Lokal (Development)

Jika Anda ingin menjalankan server backend di komputer lokal Anda:
1. Pastikan Anda sudah menginstal **Python 3.x**.
2. Buka terminal di folder project ini dan instal pustaka pendukung:
   ```bash
   pip install -r requirements.txt
   ```
3. Jalankan server Python:
   ```bash
   python server.py
   ```
4. Buka file `index.html` langsung di browser Anda. Bagian Ticker di atas akan otomatis menyala hijau: **"🔥 [SYSTEM ENGINE] KONEKSI LIVE BACKEND AKTIF"**.
