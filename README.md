# Bot Kantin PCR (Frontend)

Project ini adalah antarmuka frontend untuk **Bot Kantin PCR**, sebuah aplikasi web cerdas yang memungkinkan pengguna berinteraksi dengan layanan kantin menggunakan teks maupun suara.

Aplikasi ini dibangun menggunakan teknologi web modern, integrasi AI lokal di browser, dan backend berbasis workflow n8n.

## 🚀 Fitur Utama

-   **Interaksi Multimoda**: Dukungan fleksibel untuk berbagai cara komunikasi:
    -   **Text-to-Text**: Chatting menggunakan teks seperti biasa.
    -   **Voice-to-Text**: Input suara dikonversi menjadi teks menggunakan **Whisper AI**.
    -   **Text-to-Voice (TTS)**: Bot dapat membacakan balasan teks menjadi suara.
    -   **Voice-to-Voice**: Percakapan langsung dua arah dengan bot menggunakan suara.
-   **Kecerdasan Buatan (LLM)**: Menggunakan model **Gemma 2 9B SahabatAI** (`gmonsoon/gemma2-9b-cpt-sahabatai-v1-instruct-GGUF:Q2_K`) yang canggih untuk pemahaman konteks Bahasa Indonesia yang lebih natural.
-   **Client-side Processing**: Pemrosesan suara (Speech-to-Text) dilakukan sebagian di sisi klien untuk responsivitas tinggi.

## 🛠️ Teknologi yang Digunakan

### Frontend (User Interface)
-   **[Svelte 5](https://svelte.dev/)**: Framework UI reaktif generasi terbaru.
-   **[Vite](https://vitejs.dev/)**: Build tool yang sangat cepat.
-   **[Tailwind CSS v4](https://tailwindcss.com/)**: Utility-first CSS framework.

### AI & Logic
-   **Orchestrator / Backend**: **[n8n](https://n8n.io/)** (Workflow automation tool) untuk mengatur logika alur percakapan.
-   **LLM Model**: `hf.co/gmonsoon/gemma2-9b-cpt-sahabatai-v1-instruct-GGUF:Q2_K`.
-   **Speech-to-Text**: **[@xenova/transformers](https://huggingface.co/docs/transformers.js/index)** (Whisper) berjalan di browser.

## 📂 Struktur Project

```
/
├── backend/            # Resource terkait backend (n8n workflows, data, dll)
│   ├── MLOPS.postman_collection.json  # Dokumentasi API / Testing
│   └── BotKantinPCR.json              # Data/Schema referensi
├── public/             # Aset statis
├── src/                # Kode sumber aplikasi frontend
│   ├── lib/            # Komponen Svelte, utilitas, dan worker
│   │   ├── components/ # Atom, Molecule, Organism (Atomic Design)
│   │   └── whisper-worker.js # Web Worker untuk memproses suara (Whisper)
│   └── ...
├── index.html          # Entry point aplikasi
└── package.json        # Dependensi project
```

## 📦 Cara Instalasi dan Penggunaan

Ikuti langkah-langkah berikut untuk menjalankan project ini di komputer Anda:

### 1. Prasyarat
Pastikan Anda sudah menginstal:
-   [Node.js](https://nodejs.org/) (Versi LTS disarankan, misal v18 atau v20)
-   Git

### 2. Instalasi Dependensi
Buka terminal di folder project, lalu jalankan perintah:

```bash
npm install
```

### 3. Menjalankan Aplikasi (Development Mode)
Untuk menjalankan server lokal:

```bash
npm run dev
```

Buka browser dan kunjungi alamat yang muncul di terminal (biasanya `http://localhost:5173`).

### 4. Build untuk Produksi
Jika ingin membuat versi siap deploy:

```bash
npm run build
```
File hasil build akan berada di folder `dist/`.

## 🔌 Integrasi Backend (n8n)

Sistem backend menggunakan **n8n** sebagai orchestrator utama yang menghubungkan:
1.  Input dari Frontend (Teks/Suara terjemahan).
2.  Pemrosesan LLM (Gemma 2 SahabatAI).
3.  Respon kembali ke Frontend.

File koleksi Postman di folder `backend/` dapat digunakan untuk menguji endpoint n8n webhook secara terpisah.

## 📝 Catatan Tambahan

-   **Penggunaan Whisper AI**: Saat pertama kali fitur suara digunakan, aplikasi akan mengunduh model Whisper kecil dari HuggingFace Hub. Pastikan koneksi internet stabil saat penggunaan pertama.
