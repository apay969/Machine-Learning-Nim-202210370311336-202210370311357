Machine-Learning-Nim-202210370311336-202210370311357
Pengembangan Model ML untuk Ekstraksi & Identifikasi Peristiwa Bencana Alam (Bahasa Indonesia)

Nama Proyek: Pengembangan Model Machine Learning untuk Ekstraksi Informasi dan Identifikasi Peristiwa Bencana Alam dari Teks Berita Bahasa Indonesia
Penulis: Muhammad Nur Iman (202210370311357), Muhammad Akbar Ghaffari (202210370311336)
Tahun: 2025

1. Ringkasan Proyek

Proyek ini mengembangkan pipeline machine learning untuk menganalisis berita berbahasa Indonesia (sumber: Kompas.com) dengan tujuan:

Otomatisasi information extraction (lokasi, waktu, korban, dampak, penanganan).

Identifikasi jenis bencana (banjir, gempa, longsor, erupsi, dsb.).

Proyek mencakup pre-processing teks, ekstraksi fitur, pemodelan ML klasik, perbandingan dengan model DL/Transformer, serta evaluasi menggunakan confusion matrix dan F1-macro.

2. Business Objective

Proyek ini bertujuan untuk meningkatkan efisiensi proses pemantauan bencana dengan cara:

Mengotomatisasi ekstraksi informasi penting dari berita.

Mempercepat penyampaian informasi ke BNPB/BPBD dan pihak terkait.

Menyediakan data terstruktur untuk analisis spasial dan temporal.

Mengurangi ketergantungan terhadap proses manual yang lambat.

3. Dataset

File utama: kompas_bencana_nasional_2025.xlsx
Jumlah data: 1.429 berita kanal Nasional Kompas (tahun 2025).

Atribut dataset:

Kolom	Deskripsi
title	Judul berita
summary	Ringkasan berita
url	Tautan sumber
author	Penulis
section	Kanal berita
published_local	Waktu publikasi

Catatan penting:
Dataset asli tidak dibagikan karena berasal dari konten berhak cipta (Kompas.com). Format tabel disediakan untuk replikasi.

4. Target / Label (Output)

Model dikembangkan untuk mengekstraksi atau memprediksi:

Event / jenis bencana (banjir, gempa, longsor, erupsi, kebakaran, tsunami, dll.)

Lokasi kejadian (desa/kabupaten/kota/provinsi).

Waktu kejadian (tanggal/periode).

Penyelesaian / penanganan (evakuasi, bantuan, pemulihan).

Korban & dampak (meninggal, luka, pengungsi, terdampak).

5. Arsitektur & Metode
Pre-processing

Case folding

Cleansing (regex)

Tokenization

Stopword removal (Sastrawi)

Stemming (Sastrawi)

Reconstruction

Feature Selection

TF-IDF:

n-gram: 1–2

max_features=5000

sublinear_tf=True

FastText:

Embedding + semantic similarity

Model Klasifikasi

Logistic Regression

class_weight='balanced'

Nilai C terbaik: 10

Linear SVM

C terbaik: 1

Evaluasi

Accuracy

Precision

Recall

F1-macro

Confusion matrix

Hasil terbaik:

Logistic Regression: akurasi 0.8287 (F1-macro 0.6061)

Linear SVM: akurasi 0.8217 (F1-macro 0.5969)

Model bekerja baik pada kelas mayor, tetapi lemah pada kelas minor (tsunami, kekeringan) akibat imbalanced dataset.

6. Tahapan Proyek
1. Akuisisi & Penyimpanan Data

Mengambil artikel Kompas kanal Nasional 2025

Disimpan dalam format Excel/CSV: title, summary, url, section, author, published_local

2. Eksplorasi Data (EDA)

Analisis distribusi jenis bencana

Wordcloud, histogram tanggal, missing values

3. Anotasi / Labeling (jika menggunakan NER)

Pelabelan token untuk: lokasi, waktu, korban, penanganan

4. Pre-processing

Membersihkan teks mentah agar siap diproses

5. Feature Engineering

TF-IDF unigram & bigram

FastText embedding

Kombinasi sparse + dense

6. Pembagian Dataset

Train: 70%

Validasi: 10%

Test: 20%

Stratified split

7. Training Model

Logistic Regression

Linear SVM

Hyperparameter tuning dengan GridSearchCV

8. Evaluasi

Accuracy, F1-macro

Analisis confusion matrix

Performa per kelas

7. Evaluasi & Hasil (ringkas)
Model	Akurasi	F1-macro	Catatan
Logistic Regression	0.8287	0.6061	Terbaik
Linear SVM	0.8217	0.5969	Stabil

Temuan utama:

Kelas mayor seperti banjir dan lainnya dikenali sangat baik.

Kelas minor sering salah prediksi akibat ketidakseimbangan dataset.

8. Catatan Etis & Legal

Konten berita Kompas.com dilindungi hak cipta.

Repositori tidak menyertakan teks asli.

Pastikan penggunaan data sesuai kebijakan penyedia.

Sistem ML untuk kebencanaan harus disertai verifikasi manusia (human-in-the-loop).

9. Referensi & Bahan Bacaan

Scikit-learn documentation

Sastrawi stemmer

fastText documentation

HuggingFace Transformers

Jurnal terkait NER & Information Extraction

Paper TF-IDF, SVM, Logistic Regression, dsb.

10. Kontak

Muhammad Nur Iman — 202210370311357

Muhammad Akbar Ghaffari — 202210370311336
