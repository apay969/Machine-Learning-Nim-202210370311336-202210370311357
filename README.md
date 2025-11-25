# Machine-Learning-Nim-202210370311336-202210370311357
# Pengembangan Model ML untuk Ekstraksi & Identifikasi Peristiwa Bencana Alam (Bahasa Indonesia)

**Nama proyek**: Pengembangan Model Machine Learning untuk Ekstraksi Informasi dan Identifikasi Peristiwa Bencana Alam dari Teks Berita Bahasa Indonesia
**Penulis**: Muhammad Nur Iman (202210370311357), Muhammad Akbar Ghaffari (202210370311336)
**Tanggal**: 2025

---

## Ringkasan proyek

Proyek ini mengembangkan pipeline machine learning untuk menganalisis berita berbahasa Indonesia (sumber: Kompas.com) dengan tujuan otomatisasi *information extraction* dan identifikasi jenis peristiwa bencana alam. Output utama meliputi: (1) klasifikasi jenis bencana (banjir, gempa, longsor, dsb.) dan (2) ekstraksi entitas penting seperti lokasi, waktu, penanganan, dan korban/dampak.

---

## Business objective

Meningkatkan efisiensi dan akurasi pemantauan bencana dengan:

* Mengotomatisasi ekstraksi informasi dari berita.
* Mempercepat penyampaian informasi ke pemangku kepentingan (BNPB, BPBD, organisasi kemanusiaan).
* Menyediakan data terstruktur untuk analisis spasial dan temporal serta respons yang lebih cepat.

---

## Dataset

**File utama (digunakan dalam laporan)**: `kompas_bencana_nasional_2025.xlsx` — 1.429 entri berita kanal Nasional Kompas sepanjang 2025 (kolom: `title`, `url`, `author`, `section`, `published_local`, `summary`).

> **Catatan penting**: Dataset sumber berita berasal dari Kompas.com (konten berhak cipta). Repositori ini **tidak** menyertakan file asli. Jika ingin mereproduksi eksperimen, siapkan file dataset Anda sendiri dengan format kolom di atas atau gunakan cara scraping/ekstraksi data yang sesuai dengan kebijakan penyajian sumber.
---

## Target / Label (Output)

Model dirancang untuk mengekstraksi / memprediksi:

1. **Event (jenis bencana)** — e.g. `banjir`, `gempa`, `longsor`, `kebakaran`, `tsunami`, `lainnya`.
2. **Lokasi kejadian** — tingkat desa/kabupaten/kota/provinsi.
3. **Waktu kejadian** — tanggal atau periode yang disebutkan di teks.
4. **Penyelesaian / penanganan** — tindakan (evakuasi, bantuan, rehabilitasi).
5. **Korban & dampak** — jumlah meninggal/luka/mengungsi/terdampak.

---

## Arsitektur & Metode (yang digunakan di laporan)

* **Pre-processing**: case-folding, cleansing (regex), tokenization, stopword removal (Sastrawi), stemming (Sastrawi), reconstruction.
* **Feature selection**:

  * TF-IDF (1–2 gram, `max_features=5000`, `sublinear_tf=True`)
  * FastText (embedding / similarity untuk menambah fitur semantik)
* **Klasifikasi**:

  * Logistic Regression (`class_weight='balanced'`, terbaik C=10)
  * Linear SVM (best C=1)
* **Evaluasi**:

  * Accuracy, F1-macro, confusion matrix. Hasil eksperimen: LR akurasi 0.8287 (F1-macro 0.6061), SVM akurasi 0.8217 (F1-macro 0.5969).

---
Tahapan yang Digunakan
1. Akuisisi & Penyimpanan Data

Mengumpulkan artikel berita dari Kompas (kanal Nasional) tahun 2025.

Data disimpan dalam format tabular (Excel/CSV) berisi: title, summary, url, section, author, published_local.

2. Eksplorasi Data (EDA)

Memahami distribusi jenis bencana.

Melihat missing values, outlier, dan pola teks.

Visualisasi: bar chart jenis bencana, histogram tanggal, wordcloud kata dominan.

3. Anotasi / Labeling (Jika Menggunakan NER)

Memberikan label token untuk entitas: lokasi, waktu, korban, penanganan.

Dilakukan secara manual atau dengan tool labeler.

4. Pre-processing Teks

Meliputi:

Case folding (lowercase)

Cleansing (hapus URL, HTML, emoji, simbol)

Tokenization

Stopword removal

Stemming (Sastrawi)

Rekonstruksi kalimat bersih

Output berupa teks bersih siap digunakan.

5. Feature Engineering & Representasi Fitur

Digunakan untuk mengubah teks menjadi bentuk numerik:

a. TF-IDF

Menggunakan unigram & bigram

Membatasi jumlah fitur (misal 5000)

Menggunakan sublinear_tf=True

b. FastText

Menghasilkan embedding kata

Bisa digunakan untuk similarity atau menambah fitur dense

c. Kombinasi Fitur

Bisa menggabungkan fitur sparse (TF-IDF) dan dense (FastText)

6. Pembagian Dataset (Train / Validasi / Test)

Menggunakan stratified split agar distribusi label tetap seimbang.

Umumnya 70% train, 10% validasi, 20% test.

7. Training Model Klasifikasi

Model yang digunakan:

Logistic Regression

Linear SVM

Pengaturan:

class_weight='balanced' untuk mengatasi ketidakseimbangan label

Hyperparameter tuning menggunakan GridSearchCV dengan k-fold cross validation

Output:

Model terbaik berdasarkan hasil validasi.

8. Evaluasi Model

Evaluasi menggunakan:

Accuracy

Precision

Recall

F1-score (macro)

Confusion matrix

Per-class performance

Tujuannya untuk melihat performa tiap kelas bencana dan mendeteksi kesalahan model.

## Evaluasi & Hasil (ringkasan dari laporan)

* Logistic Regression: **Akurasi** = 0.8287, **F1-macro** = 0.6061 (C=10)
* Linear SVM: **Akurasi** = 0.8217, **F1-macro** = 0.5969 (C=1)
  Analisis confusion matrix menunjukkan kelas mayor (`lainnya`, `banjir`) dikenali baik; kelas minor (`tsunami`, `kekeringan`) kurang baik karena imbalanced dataset.

---

## Catatan etis & legal

* Pastikan menghormati hak cipta sumber berita. Jika menyiapkan dataset publik, verifikasi kebijakan penggunaan Kompas.com dan beri atribusi sebagaimana diperlukan.
* Saat menyebarkan model/layanan, pertimbangkan potensi **kesalahan prediksi** yang dapat memengaruhi respons kebencanaan — selalu sertakan human-in-the-loop untuk verifikasi.

---

## Referensi & bahan bacaan

Dokumentasi terkait:

* Library: scikit-learn, Sastrawi, fastText, Hugging Face Transformers (jika melakukan fine-tune).
* Paper / artikel terkait NER, transformer, dan ekstraksi informasi (cantumkan di paper/laporan Anda sesuai kebutuhan).

---

## Kontak

Muhammad Nur Iman — (202210370311357)
Muhammad Akbar Ghaffari — (202210370311336)
