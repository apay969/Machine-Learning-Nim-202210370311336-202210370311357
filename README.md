# Machine-Learning-Nim-202210370311336-202210370311357
# Pengembangan Model ML untuk Ekstraksi dan Identifikasi Peristiwa Bencana Alam (Bahasa Indonesia)

Nama Proyek: Pengembangan Model Machine Learning untuk Ekstraksi Informasi dan Identifikasi Peristiwa Bencana Alam dari Teks Berita Bahasa Indonesia  
Penulis: Muhammad Nur Iman (202210370311357), Muhammad Akbar Ghaffari (202210370311336)  
Tahun: 2025  

---

## Ringkasan Proyek

Proyek ini mengembangkan pipeline machine learning untuk menganalisis berita berbahasa Indonesia dari Kompas.com. Tujuan utamanya adalah melakukan klasifikasi jenis bencana serta mengekstraksi entitas penting seperti lokasi kejadian, waktu kejadian, korban, dampak, dan penanganan.

---

## Business Objective

| Tujuan |
|--------|
| Mengotomatisasi ekstraksi informasi dari berita mengenai bencana alam. |
| Mempercepat proses analisis untuk BNPB, BPBD, dan lembaga kemanusiaan. |
| Menyediakan data terstruktur untuk analisis spasial dan temporal. |
| Meningkatkan efisiensi pemantauan bencana melalui model machine learning. |

---

## Dataset

| Informasi | Detail |
|-----------|--------|
| File utama | kompas_bencana_nasional_2025.xlsx |
| Jumlah data | 1.429 berita |
| Sumber | Kompas.com (kanal Nasional tahun 2025) |
| Atribut | title, url, author, section, published_local, summary |
| Catatan | Dataset asli tidak disertakan karena hak cipta. Format tabel disediakan untuk replikasi. |

---

## Target / Label

| Target | Deskripsi |
|--------|-----------|
| Jenis bencana | banjir, gempa, longsor, erupsi, kebakaran, tsunami, lainnya |
| Lokasi kejadian | Nama wilayah administratif |
| Waktu kejadian | Tanggal atau periode yang disebutkan di teks |
| Penanganan | Evakuasi, bantuan, rehabilitasi |
| Korban dan dampak | Data jumlah korban dan kerusakan |

---

## Arsitektur dan Metode

### Pre-processing

| Tahapan |
|---------|
| Case folding |
| Cleansing (regex) |
| Tokenization |
| Stopword removal (Sastrawi) |
| Stemming (Sastrawi) |
| Rekonstruksi kalimat |

### Feature Selection

| Metode | Detail |
|--------|--------|
| TF-IDF | Unigram-bigram, max_features=5000, sublinear_tf=True |
| FastText | Embedding dan semantic similarity |

### Model Klasifikasi

| Model | Pengaturan |
|--------|------------|
| Logistic Regression | class_weight balanced, C terbaik 10 |
| Linear SVM | Nilai C terbaik 1 |

### Evaluasi

| Metrik |
|--------|
| Accuracy |
| Precision |
| Recall |
| F1-macro |
| Confusion matrix |

---

## Tahapan Proyek

| Tahap | Penjelasan |
|--------|------------|
| Akuisisi data | Mengumpulkan berita Kompas tahun 2025 dan menyimpannya dalam format tabel. |
| Eksplorasi data (EDA) | Distribusi bencana, pola teks, wordcloud, histogram, missing values. |
| Anotasi | Pelabelan entitas seperti lokasi, waktu, korban dan penanganan (untuk NER). |
| Pre-processing | Membersihkan dan menyiapkan teks untuk model. |
| Feature engineering | TF-IDF dan FastText. |
| Pembagian dataset | Train 70%, validasi 10%, test 20% menggunakan stratified split. |
| Pelatihan model | Logistic Regression dan SVM dengan GridSearchCV. |
| Evaluasi | Menggunakan F1-macro, accuracy dan confusion matrix. |

---

## Evaluasi dan Hasil

| Model | Akurasi | F1-macro | Keterangan |
|--------|---------|-----------|-------------|
| Logistic Regression | 0.8287 | 0.6061 | Performa terbaik |
| Linear SVM | 0.8217 | 0.5969 | Stabil |

Ringkasan Temuan:

| Temuan |
|--------|
| Model bekerja baik untuk kelas mayor seperti banjir dan lainnya. |
| Kelas minor seperti tsunami dan kekeringan sulit diprediksi karena ketidakseimbangan data. |

---

## Catatan Etis dan Legal

| Catatan |
|---------|
| Dataset berasal dari sumber berhak cipta (Kompas.com). |
| Repositori tidak menyertakan teks berita asli. |
| Penggunaan data harus mengikuti kebijakan penyedia. |
| Model kebencanaan harus diverifikasi oleh manusia untuk menghindari kesalahan prediksi. |

---

## Referensi

| Sumber |
|--------|
| Dokumentasi scikit-learn |
| Sastrawi stemmer |
| fastText documentation |
| HuggingFace Transformers |
| Jurnal terkait NER dan Information Extraction |

---

## Kontak

| Nama | NIM |
|------|-----|
| Muhammad Nur Iman | 202210370311357 |
| Muhammad Akbar Ghaffari | 202210370311336 |
