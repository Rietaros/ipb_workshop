# Workshop AI / Machine Learning IPB — Notebook Revisi

## Apa saja yang berubah?

- **Lab 1B: Course-demand forecast** — ada definisi jelas feature X / target y, contoh `lag_1` / `lag_2`, langkah data preparation → training → time-based holdout → MAE → forecast semester 9.
- **Lab 1C: Demand–Supply** — tujuan analitik, decision process, dan `allocate_sections()` versi pemula–menengah: satu section per putaran, cek kompetensi, sisa SKS, batas section, audit.
- **Lab 2A–B: DO risk** — definisi target DO dalam 2 semester ke depan, feature dictionary, ROC-AUC/PR-AUC, permutation feature importance, **SHAP beeswarm global dan waterfall individual**, serta queue penawaran dukungan.
- **Lab 2C: Collaborative filtering** — berbasis matriks **berhasil lulus** (nilai akhir `>= 2.0` hanya sebagai aturan data sintetis), cosine item–item, contoh mahasiswa yang lulus X juga lulus Y, offline Precision@3 dibanding popularity, dan aturan prasyarat **semua wajib lulus** (`AND`) melalui `course_prerequisites.csv`. Filter yang sudah lulus, kesiapan dosen, course offered, level, dan kapasitas juga diterapkan.

## Isi ZIP

```text
IPB_Workshop_Notebook_Baru/
├── IPB_2Labs_ML_Enhanced_Guided.ipynb
├── IPB_2Labs_ML_Enhanced_Solution_Executed.ipynb  # hasil yang sudah dieksekusi
├── requirements.txt
├── README.md
├── data/
│   ├── academic_history.csv
│   ├── course_prerequisites.csv
│   ├── course_demand.csv
│   ├── courses.csv
│   ├── lecturer_availability_term9.csv
│   ├── lecturer_course_eligibility.csv
│   ├── next_term_candidates.csv
│   ├── student_term_snapshots.csv
│   ├── student_course_interactions.csv
│   └── students.csv
└── outputs/  # terisi saat notebook dijalankan
```

## Cara menjalankan

1. **Ekstrak ZIP**, jangan buka notebook dalam ZIP langsung.
2. Di terminal folder paket: `pip install -r requirements.txt` (atau install dengan `%pip` di notebook).
3. Jalankan Jupyter Lab/Notebook dari folder paket lalu buka `IPB_2Labs_ML_Enhanced_Guided.ipynb`.
4. **Run All Cells** dari atas ke bawah. Hasil perencanaan, penugasan dosen, queue simulasi dan rekomendasi contoh disimpan di folder `outputs/`.
5. Untuk Google Colab, upload satu folder `data/` bersama notebook ke lokasi kerja Colab dan jalankan dari sana. Alternatif: unggah ZIP lalu ekstrak dengan `!unzip ...`; folder kerja harus memiliki `data/` yang sejajar dengan notebook.

## Expected output saat dites (contoh, tidak dijamin lintas versi library)

- Random Forest forecast MAE ~**5.96** mahasiswa/mata kuliah vs seasonal naive **11.22**.
- Estimasi pendaftaran semester 9 **2,006** mahasiswa–mata kuliah; 140 sections berdosen; demand yang belum terlayani **62** pada alokasi simulasi.
- DO risk ROC-AUC ~**0.814** dan PR-AUC ~**0.336** (holdout data sintetis).
- Item-based CF Precision@3 ~**22.6%** vs baseline popularitas ~**22.0%** pada *subset evaluasi yang memenuhi aturan eligibility*. Ini bukan indikator kesuksesan mahasiswa di dunia nyata.

## Catatan penting

- **Semua data fiktif**. Nama mata kuliah/program adalah contoh, bukan penetapan resmi IPB.
- Dalam `course_prerequisites.csv`, delapan mata kuliah memiliki **dua prasyarat** untuk demo `AND` (contoh C410 memerlukan **C404 dan C406**); data tambahan dibuat khusus untuk latihan, bukan ketentuan riil kampus.
- `grade_points >= 2.0` untuk **lulus** adalah definisi demo, bukan klaim mengenai aturan resmi IPB.
- Kesamaan riwayat lulus tidak membuktikan sebab-akibat atau menjamin suatu mahasiswa akan lulus mata kuliah yang direkomendasikan.
- SHAP menjelaskan output model, bukan penyebab mahasiswa DO. Risiko tinggi tidak boleh otomatis menghambat akses ke KRS/layanan.
- Algoritma alokasi dosen menggunakan **greedy heuristic**, bukan solver penjadwalan optimal. Belum termasuk bentrok jadwal/ruangan, SKS maksimal aktual, dan kursi KRS live.

## Sumber dokumentasi Python

- https://scikit-learn.org/stable/modules/ensemble.html#forests-of-randomized-trees
- https://scikit-learn.org/stable/modules/generated/sklearn.inspection.permutation_importance.html
- https://scikit-learn.org/stable/modules/metrics.html#cosine-similarity
- https://shap.readthedocs.io/en/latest/generated/shap.LinearExplainer.html
