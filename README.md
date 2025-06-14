# Case-Based Reasoning (CBR) pada PN Rantau Prapat (Narkotika & Psikotropika tahun 2024)

Sistem Case-Based Reasoning (CBR) ini membantu analisis putusan pengadilan kategori Narkotika dan Psikotropika dari PN Rantau Prapat Tahun 2024.

## Daftar Isi
1.  [Gambaran Umum](#1-gambaran-umum)
2.  [Instalasi](#2-instalasi)
3.  [Detail Notebooks](#3-detail-notebooks)
    * [1. Case Base (Scraping & Cleaning)](#1-case-base-scraping--cleaning)
    * [2. Case Representation](#2-case-representation)
    * [3. Case Retrieval](#3-case-retrieval)
    * [4. Solution Reuse](#4-solution-reuse)

---

### 1. Gambaran Umum

Proyek ini mengimplementasikan siklus Sistem Case-Based Reasoning (CBR) untuk putusan pengadilan: pengumpulan data, representasi kasus, pencarian kasus serupa, dan rekomendasi solusi.
* **Data:** Putusan PN Rantau Prapat, Narkotika & Psikotropika, Tahun 2024 ($\geq 30$ dokumen).
* **Struktur Folder di GitHub:**
    * `data/` (berisi seluruh data mentah dan olahan)
    * `notebooks/` (berisi 4 notebook: `1. Case_Base_(Scraping_&_Cleaning).ipynb`, `2. Case_Representation.ipynb`, `3. Case_Retrieval.ipynb`, `4. Solution_Reuse.ipynb`)
    * `log_scraping.txt`
    * `models/` (untuk model yang dilatih)
    * `README.md`

### 2. Instalasi

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
3.  **Download NLTK Data:**
    ```python
    import nltk
    nltk.download('stopwords')
    nltk.download('punkt')
    ```
    *Catatan: Pastikan Anda memiliki library Python yang diperlukan seperti `pandas`, `numpy`, `requests`, `beautifulsoup4`, `PyPDF2`, `scikit-learn`, `joblib`, `matplotlib`, `seaborn`, dan `jupyter` yang terinstal di lingkungan Python Anda sebelum menjalankan notebook.*

---

### 3. Detail Notebooks

Anda dapat menjalankan notebook-notebook ini menggunakan Jupyter. Dari direktori utama proyek Anda (dimana folder `data` dan `notebooks` berada), jalankan:
```bash
jupyter notebook
```
Kemudian, buka dan jalankan setiap notebook di folder `notebooks/` secara berurutan.

#### 1. Case Base (Scraping & Cleaning)
* **File:** `notebooks/1. Case_Base_(Scraping_&_Cleaning).ipynb`
* **Penjelasan:** Notebook ini menangani pengumpulan putusan pengadilan dan membersihkan teks yang diekstrak agar siap diproses.
* **Output Utama:** File PDF asli di `data/putusan_files/`, teks putusan di `data/txt_files/`, dan CSV `data/data_putusan.csv`, `data/datasets.csv`. Log di `log_scraping.txt`.

#### 2. Case Representation
* **File:** `notebooks/2. Case_Representation.ipynb`
* **Penjelasan:** Fokus pada ekstraksi metadata penting (seperti nomor perkara, tanggal, pasal, pihak) dan fitur teks (ringkasan fakta, argumen hukum utama) dari putusan yang telah dibersihkan. Data disimpan dalam format terstruktur.
* **Contoh Output Singkat:**
    ```
    --- Proses Selesai ---
    Data representasi kasus berhasil disimpan ke: .../cases_representation.csv
    Jumlah kasus yang berhasil diproses: 51
    ```

#### 3. Case Retrieval
* **File:** `notebooks/3. Case_Retrieval.ipynb`
* **Penjelasan:** Notebook ini melatih model untuk mencari kasus-kasus lama yang paling mirip dengan kasus baru (query) dan melakukan evaluasi performa model menggunakan metrik standar.
* **Hasil Evaluasi Model Retrieval:**
    ```
    Accuracy: 0.9091
    Precision: 0.8295
    Recall: 0.9091
    F1-score: 0.8667

    Classification Report:
                  precision    recall  f1-score   support

       1 angka 1       0.88      1.00      0.93         7
        1 ayat 1       0.00      0.00      0.00         1
    7 jo pasal 8       1.00      1.00      1.00         1
             nan       1.00      1.00      1.00         2

        accuracy                           0.91        11
       macro avg       0.72      0.75      0.73        11
    weighted avg       0.83      0.91      0.87        11
    ```
* **Contoh Simulasi Retrieval (Singkat):**
    ```
    --- Simulasi Case Retrieval ---
    Query 1: Pencarian umum kasus sabu dengan pasal 112
      Teks Query (Raw): Seorang terdakwa kasus narkotika ditangkap dengan sabu 10 gram di Medan...
      Label yang diprediksi oleh model: 1 angka 1

      Top 1 Kasus Paling Mirip:
        Rank 1: Case ID: 9, File: 944_Pid.Sus_2024_PN Rap.txt, Similarity: 0.1365
    ```

#### 4. Solution Reuse
* **File:** `notebooks/4. Solution_Reuse.ipynb`
* **Penjelasan:** Tahap ini fokus pada bagaimana solusi dari kasus-kasus lama yang paling relevan (mirip) dapat diambil dan direkomendasikan untuk kasus baru. Ini mencakup pengambilan pasal dan ringkasan amar putusan.
* **Contoh Rekomendasi Solusi (Singkat):**
    ```
    --- Melakukan Solution Reuse untuk Query Baru ---
    --- Query 1: Kasus baru: kepemilikan sabu 5 gram. ---

    Menemukan 1 kasus paling mirip:
      Rank 1: Case ID: 45, File: 855_Pid.Sus_2024_PN Rap.txt
        Pasal: 1 Angka 1

    --- Rekomendasi Solusi Berdasarkan Kasus Serupa ---
    Pasal yang Direkomendasikan: 1 Angka 1
    Ringkasan Amar Putusan dari Kasus Paling Mirip: nan
    
