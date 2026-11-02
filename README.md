# NLP-3

Kumpulan notebook Google Colab untuk materi mata kuliah **IT Platform Infrastructure**.
Repo ini adalah fork dari [myhanafi/NLP-3](https://github.com/myhanafi/NLP-3).

Materinya mencakup lima topik: NLP dasar, sistem rekomendasi, big data dan graph,
deteksi intrusi jaringan (IDS), serta computer vision untuk citra medis.

## Gambaran umum (untuk pemula)

Bagian ini menjelaskan isi repo tanpa istilah teknis. Kalau menemukan istilah yang
belum dikenal, lihat [Glosarium istilah](#glosarium-istilah) di bagian akhir.

### Apa itu notebook dan Google Colab?

Setiap file `.ipynb` di repo ini adalah **notebook**: dokumen yang berisi potongan
kode, teks penjelasan, dan hasil (tabel, grafik, gambar) dalam satu halaman.
Kodenya dibagi menjadi kotak-kotak kecil (**sel**) yang dijalankan satu per satu dari
atas ke bawah.

**Google Colab** adalah layanan Google untuk membuka dan menjalankan notebook langsung
di browser. Tidak perlu memasang apa pun di laptop, karena komputasinya dikerjakan
di server Google, termasuk GPU untuk pekerjaan berat.

### Pola yang sama di semua materi

Walaupun topiknya berbeda-beda, hampir semua notebook mengikuti langkah yang sama:

1. **Ambil data**: misalnya ulasan aplikasi, data rating film, catatan trafik
   jaringan, atau foto rontgen.
2. **Bersihkan data**: membuang bagian yang tidak berguna, seperti tanda baca,
   data kosong, atau gambar yang terlalu gelap.
3. **Ubah data menjadi angka**: komputer tidak bisa langsung memahami kata atau
   gambar, jadi semuanya diubah menjadi deretan angka.
4. **Latih model**: komputer mempelajari pola dari contoh-contoh data yang sudah
   diketahui jawabannya, seperti siswa yang berlatih soal beserta kunci jawabannya.
5. **Uji model**: model diberi data baru yang belum pernah dilihatnya, lalu dihitung
   seberapa sering tebakannya benar.

### Penjelasan tiap topik

- **NLP (Natural Language Processing)**: mengajari komputer "membaca" teks. Contoh di
  repo ini memakai ulasan Gojek dan Tokopedia. Komputer belajar menebak apakah sebuah
  ulasan bernada positif atau negatif, dan belajar bahwa kata seperti "driver" dan
  "ojol" punya makna yang berdekatan.
- **Sistem rekomendasi**: cara kerja fitur seperti "film yang mungkin Anda suka" di
  Netflix. Kalau dua orang menyukai film-film yang sama, film lain yang disukai orang
  pertama kemungkinan juga disukai orang kedua.
- **Big data dan graph**: data penerbangan di AS digambarkan sebagai peta jaringan.
  Bandara menjadi titik dan rute penerbangan menjadi garis penghubung. Dari peta itu
  dicari bandara yang paling sentral dan rute tercepat antarbandara. Karena datanya
  sangat besar, pengolahannya memakai Apache Spark, yang membagi pekerjaan ke banyak
  komputer sekaligus.
- **IDS (Intrusion Detection System)**: seperti satpam untuk jaringan komputer. Model
  mempelajari catatan trafik jaringan yang sudah diberi label "normal" atau "serangan",
  lalu dipakai untuk mendeteksi serangan baru secara otomatis.
- **Rontgen paru-paru**: komputer belajar mengenali foto rontgen dada pasien COVID-19,
  pasien pneumonia akibat virus, dan orang sehat. Agar tidak belajar dari nol, model
  memakai "otak" yang sudah dilatih untuk mengenali jutaan gambar umum, lalu dilatih
  ulang khusus untuk rontgen. Teknik ini disebut transfer learning. Hasilnya juga
  divisualisasikan dalam bentuk peta warna yang menunjukkan bagian paru-paru mana
  yang diperhatikan model saat menebak.

### Apa hubungannya dengan IT Platform Infrastructure?

Semua materi di atas tidak bisa berjalan tanpa infrastruktur yang mendukungnya:

- **Tempat menyimpan data**, misalnya Google Drive.
- **Mesin untuk menghitung**, misalnya server Colab dengan GPU.
- **Sistem untuk mengolah data besar**, misalnya Spark.
- **Database khusus**, misalnya Neo4j untuk data berbentuk jaringan.

Mata kuliah ini melihat AI dan pengolahan data dari sisi platform yang menopangnya:
komponen apa saja yang dibutuhkan dan bagaimana komponen-komponen itu saling
terhubung. Penjelasan yang lebih teknis ada di bagian
[Kaitan dengan IT Platform Infrastructure](#kaitan-dengan-it-platform-infrastructure).

## Daftar materi

### 1. Natural Language Processing (NLP)

| Notebook | Isi | Dataset |
|---|---|---|
| [NLP_PERTEMUAN_3](NLP_PERTEMUAN_3.ipynb) | Dasar text preprocessing: case folding, hapus angka dan tanda baca, tokenisasi, stopword, stemming bahasa Indonesia dengan **Sastrawi**, wordcloud | Contoh teks di notebook |
| [Untitled3](Untitled3.ipynb) | One-hot encoding karakter sederhana | Contoh teks di notebook |
| [word_vector_pertemuan_4](word_vector_pertemuan_4.ipynb) | Representasi teks dengan scikit-learn: `CountVectorizer` (bag of words), `TfidfVectorizer`, `HashingVectorizer` | Contoh teks di notebook |
| [word_vec_gojek](word_vec_gojek.ipynb) | Melatih **Word2Vec** (gensim) dari ulasan Gojek, simpan/muat model, visualisasi vektor kata dengan UMAP + Plotly | `gojek_review.csv` |
| [Gojek_review_Fasttext](Gojek_review_Fasttext.ipynb) | Melatih **FastText** (gensim) dari ulasan Gojek | `gojek_review.csv` |
| [word_vec_tokopedia-v2](word_vec_tokopedia-v2.ipynb) | Word2Vec dari ulasan Tokopedia + visualisasi UMAP | `tokopedia_reviews_dirty.csv` |
| [Untitled2](Untitled2.ipynb) | Word2Vec dari teks buku Project Gutenberg | `novel_lines.txt` dan `ProjectGutenbergBooks.json` (file lokal, sumbernya belum diketahui; teks bukunya berasal dari [Project Gutenberg](https://www.gutenberg.org/)) |
| [Sentimen_analisis_gojek](Sentimen_analisis_gojek.ipynb) | Analisis sentimen ulasan Gojek dengan pipeline scikit-learn + **SVM** (`jcopml`) | `gojek_review_sentiment.csv` |
| [CLASSIFICATION_TEXT_TFIDF](CLASSIFICATION_TEXT_TFIDF.ipynb) | Klasifikasi teks dengan tiga pendekatan: TF-IDF + Logistic Regression, word embedding + **BiLSTM**, dan **DistilBERT** | BBC News (`bbc-text.csv`), Coronavirus tweets (`Corona_NLP_test.csv`) |

### 2. Sistem rekomendasi

| Notebook | Isi | Dataset |
|---|---|---|
| [collaborative_filtering_movielense](collaborative_filtering_movielense.ipynb) | **Collaborative filtering** user-based (user-user) dan item-based (item-item) | [MovieLens](https://grouplens.org/datasets/movielens/) (`ratings.csv`) |

### 3. Big data dan graph analytics

| Notebook | Isi | Dataset |
|---|---|---|
| [graphframev4](graphframev4.ipynb) | **Apache Spark + GraphFrames**: bandara sebagai node, rute penerbangan sebagai edge. Analisis keterlambatan, **PageRank**, shortest path, visualisasi (NetworkX, Bokeh), serta contoh koneksi ke **Neo4j** | `flights.csv`: data keterlambatan penerbangan AS dari Bureau of Transportation Statistics, sama dengan yang dipakai di [blog Databricks](https://databricks.com/blog/2016/03/16/on-time-flight-performance-with-graphframes-for-apache-spark.html); `airports.dat`: daftar bandara dari [OpenFlights](https://openflights.org/data.html) |

### 4. Keamanan jaringan: Intrusion Detection System (IDS)

| Notebook | Isi | Dataset |
|---|---|---|
| [IDS_classic_ML](IDS_classic_ML.ipynb) | Klasifikasi trafik normal/serangan dengan ML klasik: Logistic Regression, KNN, Decision Tree, Random Forest, SVM, XGBoost, LightGBM. Tuning hyperparameter dengan **Optuna** | `Train_data.csv`, `Test_data.csv` (di Google Drive) |
| [KDD_SDAE_LSTM_multiclass_classification](KDD_SDAE_LSTM_multiclass_classification.ipynb) | Klasifikasi multikelas jenis serangan dengan **Stacked Denoising Autoencoder + LSTM** | [KDD Cup 1999](http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html) (diunduh otomatis lewat `wget`; URL di notebook mungkin sudah tidak aktif, lihat [status dataset](#status-kesiapan-dataset)) |

### 5. Computer vision: rontgen paru-paru

Semua notebook di bagian ini mengklasifikasikan citra rontgen dada ke 3 kelas:
**COVID-19, Normal, dan Viral pneumonia**. Citra ditingkatkan kontrasnya dengan
**CLAHE**, lalu dilatih dengan transfer learning. Evaluasinya memakai confusion matrix
dan kurva ROC, dan visualisasinya memakai **Grad-CAM**.

| Notebook | Isi |
|---|---|
| [X_RAY_MOBILENET_attention](X_RAY_MOBILENET_attention.ipynb) | MobileNetV2 + layer Attention |
| [Lung_X_ray_MOBILENET_attention](Lung_X_ray_MOBILENET_attention.ipynb) | Variasi MobileNetV2 + Attention |
| [150_EPOCH_MOBILENET_COVID_19_CLAHE_DL_attention_variation_2_modified_2](150_EPOCH_MOBILENET_COVID_19_CLAHE_DL_attention_variation_2_modified_2.ipynb) | Variasi MobileNetV2 + Attention dengan pelatihan lebih panjang |
| [MULTI_CLASS_RESTNET_TRANSFORMER_COVID_19_CLAHE_DL](MULTI_CLASS_RESTNET_TRANSFORMER_COVID_19_CLAHE_DL.ipynb) | Perbandingan backbone MobileNetV2, ResNet50, InceptionResNetV2, dan kombinasi fitur dengan Attention |

Dataset: folder citra `COVID/`, `NORMAL/`, `VIRUS/` di Google Drive pemilik notebook.
Sumber publiknya tidak disebutkan di notebook.

## Kaitan dengan IT Platform Infrastructure

Selain algoritmanya, notebook-notebook ini memperlihatkan beberapa komponen platform
yang dipakai untuk pekerjaan data dan AI:

- **Cloud notebook dan akselerator**: semua notebook dijalankan di Google Colab, yang
  menyediakan GPU untuk melatih model deep learning (CNN, LSTM, DistilBERT).
- **Cloud storage**: dataset dan model hasil pelatihan disimpan di Google Drive yang
  di-mount ke Colab (`drive.mount('/content/drive')`).
- **Pemrosesan terdistribusi**: Apache Spark (PySpark) dan GraphFrames untuk mengolah
  data berukuran besar.
- **Database graf**: Neo4j untuk menyimpan dan meng-query data berbentuk graf.
- **Keamanan infrastruktur**: IDS berbasis machine learning untuk mendeteksi serangan
  pada trafik jaringan.

## Status kesiapan dataset

Tabel ini menunjukkan notebook mana yang datanya sudah tersedia dan mana yang
datasetnya masih harus dicari. Status ini hanya soal **data**: notebook yang
datanya siap tetap bisa error karena versi library (lihat catatan di
[Cara menjalankan](#cara-menjalankan)).

| Status | Arti | Notebook |
|---|---|---|
| ✅ Siap | Data ada di dalam notebook, tidak perlu file tambahan | NLP_PERTEMUAN_3, Untitled3, word_vector_pertemuan_4 |
| ⚠️ Perlu cek | Data diunduh otomatis, tetapi URL `kdd.ics.uci.edu` mengembalikan 403 saat dicek; mungkin perlu diganti ke [UCI Machine Learning Repository](https://archive.ics.uci.edu/) | KDD_SDAE_LSTM_multiclass_classification |
| 📥 Unduh manual | Sumber diketahui, file harus diunduh dan path disesuaikan | collaborative_filtering_movielense (MovieLens), graphframev4 (`flights.csv` + `airports.dat` dari OpenFlights) |
| ❓ Belum diverifikasi | Nama dataset dikenal (kemungkinan dari Kaggle), tetapi sumbernya tidak disebut di notebook | CLASSIFICATION_TEXT_TFIDF (`bbc-text.csv`, `Corona_NLP_test.csv`) |
| ❌ Cari dataset | Sumber tidak diketahui; file ada di Colab/Drive pribadi pemilik notebook | word_vec_gojek, Gojek_review_Fasttext, Sentimen_analisis_gojek, word_vec_tokopedia-v2, Untitled2, IDS_classic_ML, keempat notebook rontgen paru |

## Cara menjalankan

1. Buka notebook di GitHub, lalu klik badge **Open in Colab** di bagian atas notebook.
2. Untuk notebook deep learning, aktifkan GPU: **Runtime → Change runtime type → GPU**.
3. Siapkan dataset. Banyak notebook membaca data dari path pribadi seperti
   `/content/drive/MyDrive/...`, `/content/...`, atau `/home/DATASET/...`. Unduh
   datasetnya, unggah ke Colab atau Google Drive Anda, lalu sesuaikan path di notebook.
4. Pasang library yang belum tersedia di Colab bila diminta, misalnya
   `pip install Sastrawi jcopml optuna graphframes`.

Catatan: beberapa notebook memakai API versi lama. Contohnya gensim 3.x
(`size=`, `iter=`) yang di gensim 4 menjadi `vector_size=` dan `epochs=`, serta
`neo4j.v1`. Notebook seperti ini mungkin perlu penyesuaian kecil agar berjalan di
versi library terbaru.

## Struktur remote git

| Remote | Repo | Kegunaan |
|---|---|---|
| `origin` | [mingkimingki/NLP-3](https://github.com/mingkimingki/NLP-3) | Fork pribadi, tujuan `git push` |
| `upstream` | [myhanafi/NLP-3](https://github.com/myhanafi/NLP-3) | Repo asli dari dosen |

Untuk mengambil update terbaru dari repo dosen:

```bash
git pull upstream main
git push origin main
```

## Glosarium istilah

### Data dan machine learning

| Istilah | Arti sederhana |
|---|---|
| Dataset | Kumpulan data yang dipakai untuk belajar dan menguji, misalnya ribuan ulasan atau foto rontgen |
| CSV | Format file tabel sederhana (seperti Excel) yang kolomnya dipisahkan dengan koma |
| Label | "Kunci jawaban" untuk setiap data, misalnya "positif"/"negatif" atau "COVID"/"normal" |
| Machine learning | Cara membuat komputer belajar dari contoh data, bukan diberi aturan satu per satu |
| Model | Hasil belajar komputer: "rumus" yang bisa dipakai untuk menebak jawaban dari data baru |
| Training (pelatihan) | Proses model belajar dari data yang sudah ada labelnya |
| Testing (pengujian) | Proses mengukur kemampuan model dengan data yang belum pernah dilihatnya |
| Klasifikasi | Tugas menebak kategori, misalnya positif/negatif atau serangan/normal |
| Akurasi | Persentase tebakan model yang benar |
| Confusion matrix | Tabel yang menunjukkan berapa tebakan benar dan salah untuk setiap kategori |
| Kurva ROC | Grafik untuk menilai seberapa baik model membedakan satu kategori dari kategori lain |
| Hyperparameter | Pengaturan model yang ditentukan sebelum pelatihan, misalnya jumlah tetangga pada KNN |
| Optuna | Library yang mencoba banyak kombinasi hyperparameter secara otomatis untuk mencari yang terbaik |
| Random Forest, XGBoost, KNN, SVM | Nama-nama algoritma machine learning klasik untuk klasifikasi |

### Teks (NLP)

| Istilah | Arti sederhana |
|---|---|
| Preprocessing | Membersihkan dan merapikan data mentah sebelum dipakai |
| Tokenisasi | Memecah kalimat menjadi potongan kata (token) |
| Stopword | Kata yang sangat umum dan kurang bermakna, misalnya "yang", "di", "dan"; biasanya dibuang |
| Stemming | Mengubah kata ke bentuk dasarnya, misalnya "memakan" menjadi "makan" |
| Sastrawi | Library untuk stemming bahasa Indonesia |
| Bag of words | Mengubah teks menjadi angka dengan menghitung berapa kali tiap kata muncul |
| TF-IDF | Seperti bag of words, tetapi kata yang muncul di semua dokumen diberi bobot lebih kecil karena kurang khas |
| Word embedding | Mengubah setiap kata menjadi deretan angka sehingga kata yang maknanya mirip punya angka yang berdekatan |
| Word2Vec, FastText | Metode untuk membuat word embedding |
| Analisis sentimen | Menebak nada sebuah teks: positif, negatif, atau netral |
| BERT / DistilBERT | Model bahasa besar yang sudah dilatih dengan sangat banyak teks; DistilBERT adalah versi ringkasnya |

### Deep learning dan gambar

| Istilah | Arti sederhana |
|---|---|
| Deep learning | Jenis machine learning yang memakai jaringan saraf tiruan berlapis-lapis; cocok untuk teks dan gambar |
| Neural network (jaringan saraf tiruan) | Model yang terinspirasi cara kerja otak: banyak "neuron" kecil yang saling terhubung |
| CNN | Jenis jaringan saraf yang khusus untuk mengenali pola pada gambar |
| MobileNetV2, ResNet50, InceptionResNetV2 | Nama-nama model CNN terkenal yang sudah dilatih sebelumnya |
| Transfer learning | Memakai model yang sudah pintar di satu tugas, lalu melatihnya ulang untuk tugas lain |
| LSTM / BiLSTM | Jenis jaringan saraf untuk data berurutan, seperti kalimat atau rangkaian trafik jaringan |
| Autoencoder | Jaringan saraf yang belajar meringkas data lalu menyusunnya kembali, untuk menangkap ciri pentingnya |
| Attention | Mekanisme yang membuat model fokus pada bagian data yang paling penting |
| Epoch | Satu putaran penuh model mempelajari seluruh data latih |
| CLAHE | Teknik memperjelas kontras gambar agar detail rontgen lebih terlihat |
| Grad-CAM | Peta warna yang menunjukkan bagian gambar mana yang paling diperhatikan model |

### Data besar dan graph

| Istilah | Arti sederhana |
|---|---|
| Big data | Data yang terlalu besar untuk diolah dengan satu komputer biasa |
| Apache Spark | Sistem untuk mengolah data besar dengan membagi pekerjaan ke banyak komputer |
| Graph | Struktur data berupa titik (node) dan garis penghubung (edge), seperti peta rute penerbangan |
| GraphFrames | Library untuk mengolah graph di Spark |
| PageRank | Cara mengukur seberapa penting sebuah titik dalam graph, berdasarkan banyaknya hubungan ke titik itu |
| Shortest path | Jalur terpendek antara dua titik dalam graph |
| Neo4j | Database yang khusus menyimpan data berbentuk graph |
| Collaborative filtering | Metode rekomendasi berdasarkan kesamaan selera antarpengguna atau antarbarang |

### Infrastruktur dan alat kerja

| Istilah | Arti sederhana |
|---|---|
| Notebook (`.ipynb`) | Dokumen berisi kode, teks, dan hasil yang bisa dijalankan per bagian |
| Sel | Satu kotak kode atau teks di dalam notebook |
| Google Colab | Layanan Google untuk menjalankan notebook di browser |
| GPU | Prosesor khusus yang sangat cepat untuk perhitungan deep learning |
| Runtime | "Mesin" di server Colab yang menjalankan notebook Anda |
| Mount Drive | Menghubungkan Google Drive ke Colab agar file di Drive bisa dibaca notebook |
| Path | Alamat lokasi file, misalnya `/content/drive/MyDrive/data.csv` |
| Library | Kumpulan kode siap pakai buatan orang lain, misalnya pandas atau scikit-learn |
| `pip install` | Perintah untuk memasang library Python |
| Git | Alat untuk mencatat riwayat perubahan file |
| GitHub | Situs untuk menyimpan repo git secara online |
| Repo (repository) | Folder proyek yang riwayat perubahannya dicatat oleh git |
| Fork | Salinan repo milik orang lain ke akun GitHub sendiri |
| Commit | Menyimpan "titik simpan" perubahan beserta catatannya |
| Push | Mengirim commit dari komputer ke GitHub |
| Pull | Mengambil perubahan terbaru dari GitHub ke komputer |
| Remote (`origin`, `upstream`) | Alamat repo online yang terhubung dengan repo lokal |
