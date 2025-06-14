# Case-Based Reasoning (CBR) pada PN Rantau Prapat (Narkotika & Psikotropika tahun 2024)

Sistem Case-Based Reasoning (CBR) ini membantu analisis putusan pengadilan kategori Narkotika dan Psikotropika dari PN Rantau Prapat Tahun 2024.

## Daftar Isi
1.  [Gambaran Umum](#gambaran-umum)
2.  [Instalasi](#instalasi)
3.  [Cara Menjalankan Pipeline](#cara-menjalankan-pipeline)
    * [Tahap 1: Case Base (Scraping & Cleaning)](#tahap-1-case-base-scraping--cleaning)
    * [Tahap 2: Case Representation](#tahap-2-case-representation)
    * [Tahap 3: Case Retrieval](#tahap-3-case-retrieval)
    * [Tahap 4: Solution Reuse](#tahap-4-solution-reuse)

---

### 1. Gambaran Umum

Proyek ini mengimplementasikan siklus Sistem Case-Based Reasoning (CBR) untuk putusan pengadilan: pengumpulan data, representasi kasus, pencarian kasus serupa, dan rekomendasi solusi.
* **Data:** Putusan PN Rantau Prapat, Narkotika & Psikotropika, Tahun 2024 ($\geq 30$ dokumen).
* **Struktur Folder di GitHub:**
    * `data/` (berisi seluruh data mentah dan olahan)
    * `notebooks/` (berisi 4 notebook: `1. Case_Base_(Scraping_&_Cleaning).ipynb`, `2. Case_Representation.ipynb`, `3. Case_Retrieval.ipynb`, `4. Solution_Reuse.ipynb`)
    * `log_scraping.txt`
    * `models/` (untuk model yang dilatih)
    * `requirements.txt`
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
3.  **Instal Dependensi:** Buat `requirements.txt` dengan daftar library seperti `pandas`, `numpy`, `scikit-learn`, `nltk`, `jupyter`, dll.
    ```bash
    pip install -r requirements.txt
    ```
4.  **Download NLTK Data:**
    ```python
    import nltk
    nltk.download('stopwords')
    nltk.download('punkt')
    ```

### 3. Cara Menjalankan Pipeline

Buka Jupyter Notebook dari direktori utama proyek Anda (`penalaran`):
```bash
jupyter notebook
