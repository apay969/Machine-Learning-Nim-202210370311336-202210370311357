README:
  ============================================================
  📛 INFORMASI PROYEK
  ============================================================
  project_info:
    project_title: "Natural Disaster Information Extraction"
    subtitle: "Ekstraksi Informasi & Klasifikasi Bencana Alam dari Teks Berita Bahasa Indonesia"
    topic: "Natural Language Processing (NLP) – Disaster Event Mining"
    language: "Bahasa Indonesia"
    source_document: "Machine Learning C – Natural Disaster Information Extraction"

  authors:
    - name: "Muhammad Nur Iman"
      nim: "202210370311357"
      email: "muhammadnuriman357@webmail.umm.ac.id"

    - name: "Muhammad Akbar Ghaffari"
      nim: "202210370311336"
      email: "akbargaffari336@webmail.umm.ac.id"

  ============================================================
  📌 RINGKASAN PROYEK
  ============================================================
  summary: >
    Proyek ini bertujuan mengembangkan model Machine Learning untuk
    mendeteksi, mengklasifikasikan, dan mengekstraksi informasi penting
    terkait bencana alam dari teks berita Bahasa Indonesia yang bersumber
    dari Kompas.com tahun 2025.

    Output utama meliputi:
      - Jenis bencana
      - Lokasi kejadian
      - Waktu kejadian
      - Dampak & korban
      - Tindakan penanganan

  business_objectives:
    - Otomatisasi ekstraksi informasi bencana
    - Meningkatkan kecepatan respon lembaga kebencanaan
    - Mengurangi proses manual
    - Mendukung pengambilan keputusan berbasis data
    - Meningkatkan kesiapsiagaan bencana nasional

  urgency_context: >
    Indonesia merupakan salah satu negara paling rawan bencana di dunia.
    Terjadi peningkatan signifikan jumlah bencana setiap tahun, sehingga
    dibutuhkan sistem otomatis untuk mendeteksi dan mengekstraksi informasi
    bencana secara cepat dan akurat dari teks berita.

  ============================================================
  📂 INFORMASI DATASET
  ============================================================
  dataset_info:
    source: "Kompas.com – Kanal Nasional (2025)"
    file_name: "kompas_bencana_nasional_2025.xlsx"
    total_data: 1429
    focus_disaster:
      - Hidrometeorologi (banjir, longsor, cuaca ekstrem)
      - Geologi (gempa, erupsi gunung)

  dataset_schema:
    - column: title
      type: text
      description: "Judul berita"

    - column: url
      type: link
      description: "Tautan berita"

    - column: author
      type: text
      description: "Nama penulis"

    - column: section
      type: text
      description: "Kategori berita (Nasional)"

    - column: published_local
      type: datetime
      description: "Tanggal publikasi"

    - column: summary
      type: text
      description: "Ringkasan artikel (fitur utama model)"

  ============================================================
  🎯 TARGET EKSTRAKSI (OUTPUT MODEL)
  ============================================================
  extraction_targets:
    - field: Event
      description: "Jenis bencana (banjir, gempa, longsor, dll)"

    - field: Location
      description: "Lokasi kejadian bencana"

    - field: Time
      description: "Waktu kejadian bencana"

    - field: Handling
      description: "Penanganan dan respon bencana"

    - field: Impact
      description: "Korban dan dampak kerusakan"

  ============================================================
  ⚙️ PRE-PROCESSING PIPELINE
  ============================================================
  preprocessing:
    steps:
      - Case Folding
      - Cleansing character & simbol
      - Tokenization
      - Stopword Removal
      - Stemming (Sastrawi)
      - Reconstruction

  preprocessing_examples:
    table:
      - before: "Banjir besar melanda Jakarta akibat hujan deras."
        after: "banjir besar melanda jakarta hujan deras"

      - before: "BMKG mengimbau masyarakat waspada potensi gempa."
        after: "bmkg imbau masyarakat waspada potensi gempa"

      - before: "Evakuasi korban longsor dilakukan oleh tim SAR."
        after: "evakuasi korban longsor lakukan tim sar"

  ============================================================
  🔍 FEATURE SELECTION
  ============================================================
  feature_selection_methods:
    - TF-IDF
    - FastText

  tfidf_top_features:
    table:
      - no: 1
        word: "banjir"
        score: 0.0403

      - no: 2
        word: "korban"
        score: 0.0323

      - no: 3
        word: "gempa"
        score: 0.0310

      - no: 4
        word: "bencana"
        score: 0.0300

      - no: 5
        word: "hujan"
        score: 0.0245

  fasttext_top_similarity:
    table:
      - word: "longsor"
        similarity: 0.4975

      - word: "gempabumi"
        similarity: 0.4909

      - word: "pascabanjir"
        similarity: 0.4761

      - word: "tsunami"
        similarity: 0.4634

  comparison_tfidf_vs_fasttext:
    table:
      - aspect: "Pendekatan"
        tfidf: "Frekuensi kata"
        fasttext: "Makna kata"

      - aspect: "Kelebihan"
        tfidf: "Sederhana & cepat"
        fasttext: "Paham konteks"

      - aspect: "Kekurangan"
        tfidf: "Tidak mengenali makna"
        fasttext: "Butuh data banyak"

  ============================================================
  🤖 MODEL YANG DIGUNAKAN
  ============================================================
  classical_models:
    table:
      - model: "Logistic Regression"
        best_parameter: C = 10
        accuracy: 0.8287
        f1_macro: 0.6061

      - model: "Linear SVM"
        best_parameter: C = 1
        accuracy: 0.8217
        f1_macro: 0.5969

  advanced_models:
    table:
      - model: "LSTM"
        type: "Deep Learning"
        accuracy: 0.622
        f1_macro: 0.550
        issue: "Overfitting"

      - model: "IndoBERT"
        type: "Transformer"
        accuracy: 0.689
        f1_macro: 0.530
        issue: "Fine-tuning terbatas"

      - model: "LoRA"
        type: "Parameter Efficient"
        accuracy: 0.3077
        f1_macro: 0.3347
        issue: "Imbalance data ekstrem"

  ============================================================
  📊 DISTRIBUSI LABEL
  ============================================================
  label_distribution:
    table:
      - label: "lainnya"
        total: 715

      - label: "banjir"
        total: 370

      - label: "gempa"
        total: 140

      - label: "kebakaran"
        total: 70

      - label: "longsor"
        total: 50

      - label: "tsunami"
        total: "< 20"

      - label: "kekeringan"
        total: "< 20"

  imbalance_note: >
    Dataset sangat tidak seimbang.
    Kelas minor (tsunami, kekeringan) memiliki performa sangat rendah.

  ============================================================
  🧠 EXPLAINABLE AI (XAI)
  ============================================================
  xai_methods:
    - SHAP
    - LIME

  shap_keywords:
    table:
      - keyword: "banjir"
        impact: "Meningkatkan prediksi banjir"

      - keyword: "gempa"
        impact: "Meningkatkan prediksi gempa"

      - keyword: "erupsi"
        impact: "Meningkatkan prediksi erupsi"

  lime_example:
    table:
      - word: "banjir"
        contribution: +0.33

      - word: "hujan deras"
        contribution: +0.24

      - word: "meluap"
        contribution: +0.19

      - word: "kawasan"
        contribution: -0.02

  ============================================================
  ✅ KESIMPULAN AKHIR
  ============================================================
  final_conclusion:
    - Model terbaik: TF-IDF + Linear SVM
    - Cocok untuk dataset kecil & imbalanced
    - Deep Learning butuh data lebih besar
    - LoRA kurang cocok untuk dataset ini
    - XAI membuktikan model bekerja rasional

  recommendations:
    - Gunakan SMOTE / Oversampling
    - Tambahkan data kelas minor
    - Integrasi data real-time
    - Implementasi sistem early warning

  project_status:
    status: "Completed"
    type: "Academic Research Project"
    version: "1.0"
    license: "Education / Academic Only"
