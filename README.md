# Case-Based Reasoning (CBR) pada PN Rantau Prapat (Narkotika & Psikotropika tahun 2024)

Sistem *Case-Based Reasoning* (CBR) ini membantu analisis putusan pengadilan kategori Narkotika dan Psikotropika dari PN Rantau Prapat Tahun 2024.

---

## Daftar Isi

1.  [Gambaran Umum](#1-gambaran-umum)
2.  [Instalasi](#2-instalasi)
3.  [Detail Notebooks](#3-detail-notebooks)
    * [1. Case Base (Scraping & Cleaning)](#1-case-base-scraping--cleaning)
    * [2. Case Representation](#2-case-representation)
    * [3. Case Retrieval](#3-case-retrieval)
    * [4. Solution Reuse](#4-solution-reuse)

---

## 1. Gambaran Umum

Proyek ini mengimplementasikan siklus Sistem *Case-Based Reasoning* (CBR) untuk putusan pengadilan: pengumpulan data, representasi kasus, pencarian kasus serupa, dan rekomendasi solusi.

* **Data**: Putusan PN Rantau Prapat, Narkotika & Psikotropika, Tahun 2024 (≥ 30 dokumen).
* **Struktur Repositori**:
    | Folder/File | Deskripsi |
    | :--- | :--- |
    | **`data/`** | Berisi seluruh data mentah dan hasil olahan. |
    | **`notebooks/`**| Berisi 4 notebook untuk setiap tahap siklus CBR. |
    | **`models/`** | Menyimpan model yang telah dilatih. |
    | **`log_scraping.txt`** | Catatan proses scraping data. |
    | **`README.md`** | Dokumentasi proyek. |

---

## 2. Instalasi

1.  **Clone Repositori:**
    ```bash
    git clone [https://github.com/haaahabib/case-based-reasoning.git](https://github.com/haaahabib/case-based-reasoning.git)
    cd case-based-reasoning
    ```
2.  **Buat Virtual Environment (Opsional):**
    ```bash
    python -m venv venv
    # Windows
    .\venv\Scripts\activate
    # macOS/Linux
    source venv/bin/activate
    ```
3.  **Install Library yang Diperlukan:**
    Pastikan *library* berikut terinstal:
    ```bash
    pip install pandas numpy requests beautifulsoup4 PyPDF2 scikit-learn joblib matplotlib seaborn jupyter nltk
    ```
4.  **Download NLTK Data:**
    Jalankan skrip Python berikut sekali:
    ```python
    import nltk
    nltk.download('stopwords')
    nltk.download('punkt')
    ```

---

## 3. Detail Notebooks

Jalankan Jupyter Notebook dari direktori utama proyek, lalu buka dan jalankan setiap *notebook* di folder `notebooks/` secara berurutan.

```bash
jupyter notebook
```

#### 1. Case Base (Scraping & Cleaning)
* **File:** `notebooks/1. Case_Base_(Scraping_&_Cleaning).ipynb`
* **Tujuan:** Mengumpulkan putusan pengadilan dan membersihkan teks agar siap diproses.
* **Output Utama:** File PDF di `data/putusan_files/`, teks putusan di `data/txt_files/`, dan CSV `data/data_putusan.csv`, `data/datasets.csv`.

#### 2. Case Representation
* **File:** `notebooks/2. Case_Representation.ipynb`
* **Tujuan:** Mengekstrak metadata penting (seperti nomor perkara, tanggal, pasal, pihak) dan fitur teks (ringkasan fakta, argumen hukum utama) dari putusan yang telah dibersihkan.
* **Output Utama:** `data/cases_representation.csv` dengan **51 kasus** yang berhasil diproses.

#### 3. Case Retrieval
* **File:** `notebooks/3. Case_Retrieval.ipynb`
* **Tujuan:** Melatih model untuk mencari kasus-kasus lama yang paling mirip dengan kasus baru (query) dan melakukan evaluasi performa.
* **Hasil Evaluasi Model Retrieval:**
    | Metrik | Nilai |
    | :--- | :---: |
    | **Akurasi** | **90.91%** |
    | **Precision (macro avg)** | 72% |
    | **Recall (macro avg)** | 75% |
    | **F1-Score (macro avg)** | 73% |

    **Classification Report:**
    | Kelas | Precision | Recall | F1-Score | Support |
    | :--- | :---: | :---: | :---: | :---: |
    | **1 angka 1** | 0.88 | 1.00 | 0.93 | 7 |
    | **1 ayat 1** | 0.00 | 0.00 | 0.00 | 1 |
    | **7 jo pasal 8**| 1.00 | 1.00 | 1.00 | 1 |
    | **nan** | 1.00 | 1.00 | 1.00 | 2 |

* **Contoh Simulasi Retrieval:**
    * **Query**: Pencarian kasus sabu dengan pasal 112.
    * **Prediksi Model**: `1 angka 1`
    * **Top Kasus Mirip**:
        * **Rank 1**: Case ID: 9, Similarity: 0.1365

#### 4. Solution Reuse
* **File:** `notebooks/4. Solution_Reuse.ipynb`
* **Tujuan:** Merekomendasikan solusi (pasal dan amar putusan) dari kasus serupa yang ditemukan pada tahap *retrieval*.
* **Contoh Rekomendasi Solusi**:
    * **Query Kasus Baru**: Kepemilikan sabu 5 gram.
    * **Kasus Paling Mirip Ditemukan**: Case ID: 45
    * **Rekomendasi Solusi**:
        * **Pasal**: `1 Angka 1`
        * **Ringkasan Amar Putusan**: (diambil dari amar putusan Case ID 45)
