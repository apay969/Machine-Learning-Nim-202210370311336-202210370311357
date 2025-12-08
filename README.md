📘 Pengembangan Model Machine Learning untuk Ekstraksi Informasi & Identifikasi Peristiwa Bencana Alam dari Teks Berita Bahasa Indonesia

Penulis:

Muhammad Nur Iman (202210370311357)

Muhammad Akbar Ghaffari (202210370311336)
Tahun: 2025

🔍 Ringkasan Proyek

Proyek ini membangun pipeline Machine Learning untuk menganalisis teks berita Kompas.com (kanal Nasional, tahun 2025) dengan tujuan:

Klasifikasi jenis bencana (banjir, gempa, erupsi, longsor, cuaca ekstrem, dll.)

Information Extraction / NER untuk mengekstraksi:

Lokasi kejadian

Waktu kejadian

Penanganan bencana

Korban & dampak

Pendekatan yang digunakan meliputi Machine Learning klasik (SVM, LR), Deep Learning (LSTM), Transformer (IndoBERT), dan LoRA. Termasuk juga tahap Explainable AI (SHAP & LIME).

1. 🎯 Business Objective

Tujuan utama proyek ini adalah meningkatkan efisiensi dan akurasi pemantauan bencana di Indonesia dengan:

Mengotomatisasi ekstraksi informasi dari berita dalam jumlah besar.

Memberikan data terstruktur untuk BNPB/BPBD.

Mempercepat deteksi tren bencana secara spasial & temporal.

Mengurangi ketergantungan proses manual yang lambat dan sulit diskalakan.

2. 📂 Dataset
2.1 Deskripsi Dataset

Dataset utama berada dalam file:
kompas_bencana_nasional_2025.xlsx berisi 1.429 berita bencana dengan atribut:

Kolom	Deskripsi
title	Judul berita
summary	Ringkasan isi berita
url	Sumber berita
section	Kanal berita (Nasional)
author	Penulis
published_local	Waktu publikasi

Catatan: File asli tidak disertakan di repo karena hak cipta, namun format tabel telah disediakan.

3. 🧭 Machine Learning Tasks
3.1 Text Classification

Tujuan: memprediksi jenis bencana dari teks.

3.2 Information Extraction (NER)

Model mengekstraksi:

Event (jenis bencana)

Lokasi

Waktu kejadian

Penanganan

Korban & dampak

4. 🔥 Urgensi Topik

Indonesia termasuk negara dengan risiko bencana tertinggi:

Periode Januari–Oktober 2025 terdapat 2.590 kejadian bencana.

99.03% merupakan bencana hidrometeorologi.

Frekuensi bencana meningkat 82% dalam 2010–2022.

Dampak ekonomi & sosial signifikan.

Data valid dari BNPB, BPS, dan GoodStats.

5. ⚙️ Tahap Pre-processing

Proses pembersihan data menggunakan Python + Sastrawi. Langkah:

Case folding

Cleansing (regex, hapus angka, simbol, URL, emoji)

Tokenization

Stopword removal

Stemming (Sastrawi)

Reconstruction

Contoh hasil sebelum–sesudah disediakan dalam tabel (lihat PDF / notebook).

6. 🧮 Feature Selection
6.1 TF-IDF (statistical features)

ngram (1–2)

max_features=5000

sublinear_tf = True

10 kata tertinggi TF-IDF antara lain:
banjir, korban, gempa, bencana, bantu, dll.

6.2 FastText (semantic features)

Menangkap makna kedekatan kata:

Contoh hasil similarity tertinggi:
pascagempa, gempabumi, pascabanjir, longsor, tsunami.

6.3 Perbandingan TF-IDF vs FastText
Aspek	TF-IDF	FastText
Pendekatan	Statistik	Embedding semantik
Kelebihan	Mudah diinterpretasi	Tangkap sinonim & konteks
Kekurangan	Tidak mengenali makna	Butuh data besar
Kegunaan	Fitur penting	Makna & relevansi
7. 🏗️ Model & Eksperimen
7.1 Model Klasik
1. Logistic Regression

class_weight='balanced'

C terbaik = 10

2. Linear SVM

Linear SVM dengan C = 1

grid search + stratified 3-fold CV

📊 Hasil Model Klasik
Model	Akurasi	F1-Macro	C
Logistic Regression	0.8287	0.6061	10
Linear SVM	0.8217	0.5969	1
8. 📉 Confusion Matrix & Analisis

Kedua model baik dalam kelas besar:
✔ banjir
✔ gempa
✔ lainnya

Lemah pada kelas minor:
✘ tsunami
✘ kekeringan
✘ puting beliung

Penyebab: imbalanced dataset.

9. 🤖 Model Lanjutan: LSTM & IndoBERT
9.1 Hasil LSTM
Metric	Nilai
Akurasi	0.622
F1-Macro	0.550

❗ Overfitting parah → Train naik, Validation stagnan.

9.2 Hasil IndoBERT
Metric	Nilai
Akurasi	0.689
F1-Macro	0.530

Masalah utama:

fine-tuning terbatas

dataset kecil

kelas tidak seimbang

10. ⚡ LoRA (Low-Rank Adaptation)
Hasil Epoch 7
Metric	Nilai
Train Loss	0.3353
Validation Accuracy	0.3077
Validation F1-Macro	0.3347
Performa per Kelas (Ringkas)

Kelas besar → lumayan
Kelas kecil → gagal total

11. 🧠 Explainable AI (XAI)

Metode:

SHAP

LIME

Hasil Utama XAI
SHAP (Global)

Fitur penting:

“banjir”, “hujan deras”, “meluap”

“gempa”, “magnitudo”, “BMKG”

“erupsi”, “luncuran lava”

Model terbukti tidak asal menebak, tetapi mengikuti kata relevan.

LIME (Local)

Menunjukkan kata pendorong keputusan per berita, warna:

hijau → positif

merah → negatif

12. 🏆 Perbandingan Semua Model
Model	Accuracy	F1-Macro	Pendekatan
TF-IDF + SVM	0.787	0.700	klasik
LSTM	0.622	0.550	deep learning
IndoBERT	0.689	0.530	pretrained
LoRA	0.3077	0.3347	PEFT

📌 Model klasik TF-IDF + SVM adalah yang terbaik.

Alasan:

Dataset kecil

Imbalanced

Fitur TF-IDF sangat kuat untuk teks berita bahasa Indonesia

13. 📌 Kelemahan & Tantangan

Kelas minor sangat sedikit → model kesulitan

Data dari satu portal media → kurang bervariasi

Beberapa bencana jarang terjadi (tsunami, puting beliung)

14. 📚 Referensi

Sertakan 8–15 referensi jurnal:

NER Indonesia

FastText

IndoBERT

Disaster NLP

Model SVM klasik untuk teks

Paper XAI SHAP & LIME
(sudah kamu siapkan pada laporan)

15. 📞 Kontak

Muhammad Nur Iman – 202210370311357

Muhammad Akbar Ghaffari – 202210370311336
