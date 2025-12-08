
  project_title: "Natural Disaster Information Extraction"
  subtitle: "Ekstraksi Informasi & Klasifikasi Bencana Alam dari Teks Berita Bahasa Indonesia"
  authors:
    - name: Muhammad Nur Iman
      nim: 202210370311357
      email: muhammadnuriman357@webmail.umm.ac.id
    - name: Muhammad Akbar Ghaffari
      nim: 202210370311336
      email: akbargaffari336@webmail.umm.ac.id
  source_document: "Machine Learning C – Natural Disaster Information Extraction"
  citation: :contentReference[oaicite:0]{index=0}
  language: "Bahasa Indonesia"

  ============================================================
  📌 RINGKASAN PROYEK
  ============================================================
  summary: >
    Proyek ini bertujuan membangun model Machine Learning untuk mendeteksi, 
    mengklasifikasikan, dan mengekstraksi informasi penting terkait bencana alam 
    dari teks berita Indonesia (Kompas.com 2025). Output utama mencakup:
    - Jenis bencana
    - Lokasi kejadian
    - Waktu kejadian
    - Dampak dan korban
    - Tindakan penanganan

  primary_objective:
    - Otomatisasi ekstraksi informasi bencana dari berita online
    - Meningkatkan kecepatan respons lembaga kebencanaan
    - Mendukung pengambilan keputusan berbasis data

  urgency_context: >
    Indonesia merupakan negara rawan bencana. Lonjakan kejadian 
    membuat proses manual tidak efisien sehingga diperlukan 
    pendekatan AI untuk identifikasi dan ekstraksi informasi cepat.
    (Sumber data dari Kompas & laporan kebencanaan nasional) :contentReference[oaicite:1]{index=1}

  ============================================================
  📂 DATASET
  ============================================================
  dataset:
    source: "Kompas.com - Kanal Nasional 2025"
    file: "kompas_bencana_nasional_2025.xlsx"
    total_records: 1429
    focus: 
      - Hidrometeorologi (banjir, longsor, cuaca ekstrem)
      - Geologi (gempa, erupsi gunung)

  schema_table:
    - column: title
      description: Judul berita
    - column: url
      description: Link sumber berita
    - column: author
      description: Nama penulis
    - column: section
      description: Kategori berita (Nasional)
    - column: published_local
      description: Waktu publikasi
    - column: summary
      description: Ringkasan isi berita (fitur utama model)

  ============================================================
  🎯 TARGET EKSTRAKSI (OUTPUT MODEL)
  ============================================================
  targets:
    table:
      - field: Event
        description: Jenis bencana (banjir, gempa, longsor, dll)
        method: Keyword + Context Detection
      - field: Location
        description: Lokasi kejadian (desa, kota, provinsi)
        method: NER (Named Entity Recognition)
      - field: Time
        description: Waktu kejadian
        method: Temporal Entity Recognition
      - field: Handling
        description: Penanganan bencana (evakuasi, distribusi logistik)
        method: Context Phrase Detection
      - field: Impact
        description: Dampak & korban
        method: Numeric Pattern Recognition + Context

  ============================================================
  ⚙️ TAHAP PRE-PROCESSING
  ============================================================
  preprocessing_pipeline:
    steps:
      - Case Folding
      - Cleansing (regex, simbol, URL, emoji)
      - Tokenization
      - Stopword Removal
      - Stemming (Sastrawi)
      - Reconstruction

  preprocessing_examples:
    table:
      - original: "Banjir besar melanda Jakarta akibat hujan deras."
        processed: "banjir besar melanda jakarta hujan deras"
      - original: "BMKG mengimbau waspada gempa dan tsunami."
        processed: "bmkg imbau waspada gempa tsunami"

  ============================================================
  🔍 FEATURE SELECTION
  ============================================================
  methods:
    - TF-IDF
    - FastText Embedding

  tfidf_top_keywords:
    table:
      - word: banjir
        score: 0.0403
      - word: korban
        score: 0.0323
      - word: gempa
        score: 0.0310
      - word: bencana
        score: 0.0300
      - word: hujan
        score: 0.0245

  fasttext_similar_terms:
    table:
      - word: longsor
        similarity: 0.4975
      - word: gempabumi
        similarity: 0.4909
      - word: pascabanjir
        similarity: 0.4761
      - word: tsunami
        similarity: 0.4634

  method_comparison:
    table:
      - aspect: Focus
        tfidf: Frekuensi statistik
        fasttext: Makna semantik
      - aspect: Advantage
        tfidf: Cepat & mudah
        fasttext: Paham konteks
      - aspect: Weakness
        tfidf: Tidak kenal makna
        fasttext: Perlu data besar

  ============================================================
  🤖 MODEL & ALGORITMA
  ============================================================
  classical_models:
    table:
      - model: Logistic Regression
        best_C: 10
        accuracy: 0.8287
        f1_macro: 0.6061
      - model: Linear SVM
        best_C: 1
        accuracy: 0.8217
        f1_macro: 0.5969

  advanced_models:
    table:
      - model: LSTM
        accuracy: 0.622
        f1_macro: 0.550
        comment: Overfitting
      - model: IndoBERT
        accuracy: 0.689
        f1_macro: 0.530
        comment: Fine-tuning terbatas
      - model: LoRA
        accuracy: 0.3077
        f1_macro: 0.3347
        comment: Sangat terpengaruh imbalance

  ============================================================
  📊 DISTRIBUSI LABEL
  ============================================================
  label_distribution:
    table:
      - label: lainnya
        count: 715
      - label: banjir
        count: 370
      - label: gempa
        count: 140
      - label: kebakaran
        count: 70
      - label: longsor
        count: 50
      - label: tsunami
        count: <20
      - label: kekeringan
        count: <20

  imbalance_note: >
    Dataset sangat tidak seimbang (imbalanced) sehingga
    mempengaruhi performa pada kelas minor seperti tsunami dan kekeringan.

  ============================================================
  🧠 EXPLAINABLE AI (XAI)
  ============================================================
  xai_methods:
    - SHAP
    - LIME

  shap_insights:
    table:
      - keyword: banjir
        effect: Meningkatkan prediksi kelas banjir
      - keyword: gempa
        effect: Meningkatkan prediksi kelas gempa
      - keyword: erupsi
        effect: Meningkatkan prediksi kelas erupsi

  lime_example:
    words:
      - banjir: 0.33
      - hujan deras: 0.24
      - meluap: 0.19
      - kawasan: -0.02

  ============================================================
  🏆 KESIMPULAN UTAMA
  ============================================================
  final_summary:
    - Model terbaik: TF-IDF + Linear SVM
    - Cocok untuk dataset kecil & imbalanced
    - Deep Learning & IndoBERT butuh data lebih besar
    - LoRA tidak cocok untuk dataset ini tanpa balancing

  recommendations:
    - Gunakan SMOTE / Data Augmentation
    - Perbesar dataset minor
    - Integrasi real-time news feed
    - Terapkan pada sistem peringatan dini

  ============================================================
  ✅ STATUS PROYEK
  ============================================================
  status: "Completed (Experimental - Academic Project)"
  version: 1.0
  license: Academic Use Only

