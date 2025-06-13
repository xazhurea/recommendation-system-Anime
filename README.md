# Laporan Proyek Machine Learning - Fathia Rahma

## Project Overview

Kemajuan teknologi digital telah mempermudah akses terhadap berbagai bentuk hiburan, seperti film, musik, serial TV, dan anime, melalui platform streaming yang menyediakan konten beragam. Anime, sebagai salah satu industri hiburan global, menunjukkan pertumbuhan signifikan sejak dekade 2010-an. Pada 2017, industri anime Jepang mencatat rekor penjualan sebesar ¥2,15 triliun (sekitar $19,8 miliar), yang sebagian besar didorong oleh permintaan dari penonton internasional. Pada 2019, nilai industri ini mencapai $24 miliar per tahun, dengan 48% pendapatan berasal dari pasar luar negeri, menjadikan anime sebagai salah satu sektor industri terbesar di Jepang [[1](https://edition.cnn.com/style/article/japan-anime-global-identity-hnk-intl)]. Data ini menunjukkan popularitas anime sebagai salah satu konten paling diminati di platform digital saat ini.

Meskipun popularitas anime sering dipengaruhi oleh tren, promosi, atau dinamika komunitas, faktor-faktor tersebut tidak selalu mencerminkan preferensi pribadi penonton. Baik penggemar baru maupun lama sering kali kesulitan menemukan anime yang sesuai dengan minat mereka, terutama ketika dihadapkan pada rekomendasi umum atau daftar tontonan yang sedang viral. Situs seperti MyAnimeList menyediakan informasi dan ulasan, namun pendekatan ini masih memerlukan eksplorasi manual yang memakan waktu. Oleh karena itu, diperlukan sistem rekomendasi yang dapat memberikan saran tontonan secara personal dan relevan berdasarkan karakteristik serta preferensi pengguna, bukan semata-mata mengandalkan popularitas suatu judul.


<!-- Pada bagian ini, Kamu perlu menuliskan latar belakang yang relevan dengan proyek yang diangkat.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Jelaskan mengapa proyek ini penting untuk diselesaikan.
- Menyertakan hasil riset terkait atau referensi. Referensi yang diberikan harus berasal dari sumber yang kredibel dan author yang jelas.
  
  Format Referensi: [Judul Referensi](https://scholar.google.com/)  -->

## Business Understanding

<!-- Pada bagian ini, Anda perlu menjelaskan proses klarifikasi masalah. 

Bagian laporan ini mencakup:-->

Sistem rekomendasi memainkan peran penting dalam membantu pengguna menemukan konten yang relevan di tengah banyaknya pilihan yang tersedia. Dalam konteks anime, pengguna sering kali kesulitan menemukan anime baru yang sesuai dengan preferensi mereka. Dengan lebih dari 12.000 judul anime dan jutaan rating pengguna, dibutuhkan sistem yang dapat memberikan rekomendasi yang akurat, personal, dan efisien.

### Problem Statements
Berdasarkan *Project Overview* diatas, berikut beberapa rincian masalah yang dapat dibahas pada proyek ini.

- Genre anime apa saja yang paling diminati oleh pemirsa?
- Bagaimana merekomendasikan anime kepada pengguna berdasarkan preferensi pengguna?
- Bagaimana merekomendasikan anime berdasarkan genre dengan anime yang disukai pengguna?
  
### Goals

Berdasarkan *Problem statements* diatas, berikut beberapa goals yang diharapkan dari proyek ini:
- Mengetahui genre anime yang paling diminati oleh pemirsa.
- Membuat model untuk merekomendasikan anime kepada pengguna berdasarkan preferensi pengguna.
- Membuat model merekomendasikan anime berdasarkan genre dengan anime yang disukai pengguna

### Solution statements

Berdasarkan *Goals* diatas, berikut solusi yang dapat dilakukan:
- Dengan melakukan Explorasi Data Analysis dan Visualiasi data untuk mengetahui top 10 genre yang paling diminati oleh pemirsa
- Menggunakan algoritma Collaborative Filtering untuk memberikan rekomendasi anime yang sesuai dengan preferensi pemirsa.
- Menggunakan algoritma Content-Based Filtering untuk memberikan rekomendasi anime yang sesuai dengan genre.
- Menggunakan MAE dan RMSE untuk mengevaluasi kinerja model.


<!-- ### Constraints

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Menambahkan bagian “Solution Approach” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Mengajukan 2 atau lebih solution approach (algoritma atau pendekatan sistem rekomendasi). -->

## Data Understanding

Dataset yang digunakan untuk membangun sistem rekomendasi anime ini bersumber dari [Anime Recommendation Database](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database) yang tersedia di Kaggle dan dipublikasikan oleh [CooperUnion](https://www.kaggle.com/CooperUnion) dengan rating usability 10.00. Dataset ini merupakan hasil kompilasi dari berbagai data yang tersedia di [MyAnimeList](https://myanimelist.net/) dan terdiri dari dua file utama: `anime.csv` dan `rating.csv`.

---

### 📁 Struktur Dataset

#### **1. anime.csv**
Dataset ini berisi informasi deskriptif mengenai judul anime dan memiliki **12294 baris dan 7 kolom**.

| Kolom     | Tipe Data                 | Keterangan                                  |
| --------- | ------------------------- | ------------------------------------------- |
| anime\_id | Numerik             | ID unik untuk tiap anime                    |
| name      | Kategorikal       | Judul anime                                 |
| genre     | Kategorikal  | Daftar genre (dipisahkan koma)              |
| type      | Kategorikal      | Tipe anime (TV, Movie, OVA, dll)            |
| episodes  | Numerik             | Jumlah episode                              |
| rating    | Numerik          | Skor rata-rata pengguna                     |
| members   | Numerik           | Jumlah user yang memasukkan anime ke daftar |

Tabel 1. Struktur data anime.csv

#### **2. rating.csv**

Dataset ini berisi interaksi pengguna terhadap anime, dengan total **73515 baris dan 3 kolom**.

| Kolom     | Tipe Data     | Keterangan                                         |
| --------- | ------------- | -------------------------------------------------- |
| user\_id  | Numerik (int) | ID pengguna                                        |
| anime\_id | Numerik (int) | ID anime yang diberi rating                        |
| rating    | Numerik (int) | Nilai rating dari 1–10, `-1` jika belum ada rating |

Tabel 2. Struktur data rating.csv

---

### 🧼 Cek Missing Value

#### **anime.csv**

| Variabel  | Jumlah Missing |
| --------- | -------------- |
| anime\_id | 0              |
| name      | 0              |
| genre     | 62            |
| type      | 25              |
| episodes  | 0              |
| rating    | 230           |
| members   | 0              |

Tabel 3. Nilai hilang pada dataset anime.csv

#### **rating.csv**

| Variabel  | Jumlah Missing |
| --------- | -------------- |
| user\_id  | 0              |
| anime\_id | 0              |
| rating    | 0              |

Tabel 4. Nilai hilang pada dataset rating.csv

**Kesimpulan**: Pada anime.csv, missing value ditemukan pada `genre`, `type` dan `rating`, sehingga nantinya akan dilakukan penghapusan baris yang mengandung missing value untuk menjaga kualitas analisis. Pada rating.csv tidak ditemukan missing value

---

### 📈 Deskripsi Statistik

#### **anime.csv (Setelah pembersihan)**

| Kolom   |   Mean   | Median | Min  | Max       |
| ------- | -------- | ------ | ---- | --------- |
| rating  | 6.473902 | 6.57   | 1.67 | 10.00     |
| members |  18.348  | 1.552  | 12   | 1.013.917 |

Tabel 5. Deskripsi Statistik pada dataset anime.csv

> Menunjukkan distribusi rating cukup normal dengan kecenderungan mendekati 7, serta menunjukkan bahwa sebagian besar anime memiliki jumlah anggota komunitas yang relatif kecil dibandingkan beberapa judul yang sangat populer.

#### **rating.csv**

| Kolom  | Mean | Median | Min  | Max  |
| ------ | ---- | ------ | ---- | ---- |
| rating | 6.14 | 7.00   | -1.0 | 10.0 |

Tabel 6. Deskripsi Statistik pada dataset rating.csv

> Rating dari pengguna menunjukkan kecenderungan positif, dengan mayoritas rating berada di antara 6 dan 9.

---
### 📊 Tren Data
![download](https://github.com/user-attachments/assets/0d316847-385e-49df-85c9-3ec4df1427c8)

Gambar 1. Histogram anime berdasarkan _type_

![download](https://github.com/user-attachments/assets/4431cc6e-c70a-4e90-9b75-6eac4895c52b)

Gambar 2. Diagram batang popularitas anime berdasarkan _genre_

![download](https://github.com/user-attachments/assets/d66e98ec-8e80-41f6-9c99-24b77266aa33)

Gambar 3. Diagram batang popularitas 10 judul anime berdasarkan jumlah penonton


- TV series mendominasi produksi anime, tetapi OVA dan film juga tetap signifikan.
- Genre dan sub-genre yang sangat bervariasi menunjukkan fleksibilitas medium anime dalam menjangkau berbagai demografik.
- Popularitas anime tidak selalu berbanding lurus dengan jumlah genre atau tipe, melainkan dipengaruhi oleh kualitas cerita, daya tarik karakter, dan eksposur global.


Berikut beberapa hal yang didapatkan setelah dilakukan Eplorasi dan visualisasi data

* **Kualitas Data**: Dataset memiliki volume besar, dan beberapa missing value.
* **Preferensi Genre**: Kolom `genre` dan `rating_user` dapat digunakan untuk mengidentifikasi genre favorit per pengguna.
* **Collaborative Filtering**: Jumlah user unik yang besar dan variasi rating memungkinkan pendekatan Collaborative Filtering karena ada cukup banyak user dengan perilaku yang dapat dibandingkan.


<!-- Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis. -->

## Data Preparation

### Penggabungan Dataset
Menggabungkan dataset anime dan review dengan menggunakan fungsi merge dari padas dataframe. Penggabungan dilakukan melalui:

> **Right Join** antara `rating.csv` dan `anime.csv` berdasarkan kolom `anime_id`, untuk memastikan semua data interaksi pengguna tetap terjaga.

Setelah penggabungan, kolom rating_x dan rating_y diganti namanya menjadi AverageRating (dari anime.csv) dan rating_user (dari rating.csv) agar lebih mudah dibedakan. Dataset hasil gabungan terdiri dari 9 kolom, yaitu:

| Kolom Gabungan | Keterangan                      |
| -------------- | ------------------------------- |
| anime\_id      | ID anime                        |
| name           | Judul anime                     |
| genre          | Genre anime                     |
| type           | Tipe anime                      |
| episodes       | Jumlah episode                  |
| AverageRating  | Rating rata-rata dari anime.csv |
| members        | Jumlah member MyAnimeList       |
| user\_id       | ID pengguna                     |
| rating\_user   | Rating yang diberikan oleh user |

Tabel 7. Dataset anime_rating.csv

### Mengatasi *missing value*

Terdapat missing value pada beberapa kolom seperti name, genre, type, episodes, AverageRating, dan members. Namun, setelah dianalisis, baris-baris yang memiliki nilai kosong pada genre dan AverageRating juga memiliki nilai kosong di kolom lain.

Oleh karena itu, penghapusan missing value dilakukan khusus berdasarkan kolom genre dan AverageRating, yang secara efektif membersihkan seluruh baris yang tidak lengkap.

Setelah penghapusan, hasilnya adalah dataset tanpa missing value sama sekali.

### Mengatasi data duplikat

Dataset hasil penggabungan memiliki 1 baris duplikat. Hal ini diatasi dengan menggunakan fungsi drop_duplicates() dari pandas. Setelah penghapusan, seluruh baris dalam dataset menjadi unik. Hal ini perlu dilakukan karena data duplikat dapat menyebabkan bias dalam hasil analisis karena data tersebut akan dihitung lebih dari sekali. Selain itu, data duplikat juga dapat menurunkan akurasi model machine learning dan memperlambat proses komputasi. 

### Mengubah value pada kolom rating_user
Dalam dataset rating.csv, nilai -1 pada kolom rating digunakan untuk menandai bahwa user belum memberikan rating pada suatu anime. Nilai ini diubah menjadi 0 karena nilai 0 mencerminkan "belum memberi rating", sehingga dapat dibedakan dari rating nyata (1–10) saat melakukan analisis atau training model.

#### Data untuk CBF
Karena model Content Based Recomendation menggunakan TF-IDF untuk mentransformasikan  teks menjadi representasi angka maka kita membuat data salinan data untuk model ini dengan adalah menyusun data yang relevan. Data yang digunakan terdiri dari kolom:
- `anime_id`
- `name` 
- `genre` 
- `AverageRating`

#### Ekstraksi Fitur Genre dengan TF-IDF
TF-IDF Vectorizer digunakan pada model Content Based Recomendation yang akan mentransformasikan teks menjadi representasi angka yang memiliki makna tertentu dalam bentuk matriks. 
Hal ini perlu dilakukan untuk melakukan perhitungan dan analisis terhadap teks maka teks tersebut di transformasikan kedalam bentuk angka.Genre dari masing-masing anime diubah menjadi vektor numerik menggunakan teknik TF-IDF, yang memungkinkan untuk mengukur seberapa penting suatu genre dalam koleksi anime.
- TF-IDF diterapkan dengan tokenizer berbasis pemisah koma ', ', agar setiap genre dikenali sebagai token individual.
- Hasil vektorisasi menghasilkan 43 fitur unik genre, seperti 'action', 'drama', 'romance', 'sci-fi', 'supernatural', dan sebagainya.
- Dimensi hasil TF-IDF matrix adalah (11162, 43).

Output menunjukkan bagaimana setiap anime memiliki skor representasi (bobot TF-IDF) terhadap genre-genre tertentu, yang kemudian menjadi dasar perhitungan kemiripan.

#### Filter Rating
Filter rating digunakan pada dataset untuk model Collaborative Filtering Recommendation, data difilter untuk hanya menyertakan rating ≥ 7, agar model fokus pada preferensi positif.

#### Encoding
Encoding dilakukan terhadap ID pengguna dan ID anime untuk mengubahnya menjadi representasi numerik berurutan. Proses ini diperlukan agar setiap entitas dapat dikenali sebagai indeks oleh embedding layer dalam model TensorFlow.

#### Normalisasi
Sementara itu, nilai rating dinormalisasi ke dalam rentang 0–1 untuk menyesuaikan dengan fungsi aktivasi sigmoid pada layer output. Dengan demikian, nilai prediksi yang dihasilkan oleh model berada dalam skala yang sama dengan target, sehingga proses pelatihan dapat berlangsung secara optimal

#### Pembagian Dataset
Dalam membangun model pembelajaran mesin, dataset perlu dibagi menjadi dua bagian utama:

- **Data Latih:** Digunakan untuk melatih model. Model akan mempelajari pola dan hubungan antara fitur dan target dalam data latih ini.
- **Data validasi:** Digunakan untuk menguji kinerja model yang telah dilatih. Model akan memprediksi nilai pada data uji, dan hasilnya akan dibandingkan dengan nilai sebenarnya untuk mengevaluasi seberapa baik model tersebut bekerja pada data yang belum pernah dilihat sebelumnya.

Pada proyek ini dataset dibagi 80:20. Pembagian data dengan perbandingan 80:20 adalah salah satu cara yang umum digunakan, artinya 80% data akan digunakan untuk melatih model dan 20% sisanya untuk menguji model.

Alasan utama pembagian dataset adalah untuk mengukur kemampuan generalisasi model, yaitu seberapa baik model dapat memprediksi data baru yang belum pernah dilihat sebelumnya. Dengan memisahkan sebagian data sebagai data validasi, dapat mengevaluasi apakah model mengalami overfitting (terlalu cocok dengan data latih) atau tidak, dan memastikan bahwa performanya stabil saat digunakan.


<!-- Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut. -->


## Modeling

### Content Based Recomendation
Model akan memberikan rekomendasi dengan cara mengukur tingkat kemiripan antar-anime berdasarkan kesamaan genre. Caranya adalah dengan menggunakan TF-IDF Vectorizer, di mana data teks genre ditransformasikan menjadi representasi numerik bermakna dalam bentuk matriks. Selanjutnya, matriks tersebut dihitung derajat kesamaannya menggunakan Cosine Similarity antar judul anime.

Untuk mengimplementasikan proses rekomendasi ini, dibuat sebuah fungsi bernama Rekomendasi_anime yang menerima input berupa judul anime dan jumlah rekomendasi yang diinginkan (top-N). Fungsi ini akan mencari anime yang paling mirip berdasarkan skor kemiripan dan mengembalikan daftar judul anime yang direkomendasikan, beserta informasi genre dan rata-rata rating-nya.

#### Cosine Similarity
Untuk mengukur kemiripan antar anime, digunakan cosine similarity terhadap TF-IDF matrix. Matriks kemiripan cosine_sim berukuran (11162, 11162) yang menyatakan nilai kemiripan antara semua kombinasi pasangan anime.

Setiap nilai dalam matriks tersebut berada dalam rentang 0–1, di mana 1 menunjukkan dua anime memiliki genre yang sama persis.

#### Fungsi Rekomendasi
Fungsi `Rekomendasi_anime(anime_name, top_n=10)` dibuat untuk menghasilkan daftar rekomendasi berdasarkan kesamaan genre. Mekanismenya. Pertama-tama dimasukkan input judul anime yang diinginkan, kemudian sistem akan mencari anime-anime yang memiliki derajat kemiripan dari genre dan memberikan rekomendasi berdasarkan top N
Kemudian didapat Top N recommendation dari anime
![image](https://github.com/user-attachments/assets/2bd36d8a-e59f-431a-8f36-33823d14217a)

Gambar 4. Top N recommendation model Content Based recomendation

#### Kelebihan
- Mudah Diimplementasikan: Menggunakan pustaka seperti scikit-learn menjadikan metode ini sederhana dan cepat diterapkan.
- Tidak Memerlukan Data Pengguna: Cocok digunakan meskipun tidak ada riwayat pengguna lain.
- 
#### Kekurangan
- Overspecialization: Sistem cenderung memberikan rekomendasi yang sangat mirip karena hanya berdasar genre, mengurangi keragaman.
- Cold Start untuk Item Baru: Jika informasi genre tidak lengkap, sistem sulit bekerja.


### Collaborative Filtering Recommendation
Metode paling umum untuk sistem rekomendasi sering kali dilengkapi dengan Collaborating Filtering (CF) yang mengandalkan kumpulan data pengguna dan item sebelumnya. Model ini adalah model faktor laten, yang mengekstraksi fitur dari matriks pengguna dan item [Denise Chen](https://towardsdatascience.com/recommender-system-singular-value-decomposition-svd-truncated-svd-97096338f361). 

Setelah proses prapemrosesan dan encoding data selesai, pendekatan Collaborative Filtering (CF) digunakan untuk membangun sistem rekomendasi berbasis user-item interaction. Model yang digunakan merupakan varian dari Neural Collaborative Filtering (NCF), yaitu metode non-linear berbasis deep learning yang mengembangkan pendekatan klasik matrix factorization agar dapat menangkap pola interaksi yang lebih kompleks.

Model dikembangkan menggunakan TensorFlow Keras custom class RecommenderNet. Arsitektur model terdiri dari:

* Embedding layer untuk user dan anime: masing-masing merepresentasikan pengguna dan anime ke dalam vektor berdimensi 50.
* Bias embedding: untuk menyesuaikan kecenderungan rating pribadi user dan popularitas anime.
* Dot product antara vektor user dan anime digunakan untuk menghasilkan skor prediksi interaksi, yang kemudian ditambah dengan bias user dan anime.
* Activation function: output dari model dibungkus dalam fungsi sigmoid karena target rating telah dinormalisasi ke skala [0, 1].

Model dikompilasi dengan:

* Loss function: BinaryCrossentropy
* Optimizer: Adam dengan learning rate 0.001
* Evaluation metric: RootMeanSquaredError (RMSE)

Model dilatih selama 20 epoch dengan batch size 128, menggunakan data latih sebesar 80% dari total interaksi user-anime yang telah difilter (hanya rating ≥ 7 yang digunakan untuk menjaga kualitas sinyal preferensi). Validasi dilakukan menggunakan 20% data sisanya.

Berikut top-N anime yang direkomendasikan

![image](https://github.com/user-attachments/assets/e780493e-9c6c-4d15-af0a-37e088085e25)

Gambar 5. Top N recommendation model Collaborative Filtering Recommendation

#### Kelebihan
- Personalisasi Tinggi: Rekomendasi disesuaikan dengan pola preferensi individual.
- Menangkap Pola Laten: Mampu menemukan relasi tersembunyi antara pengguna dan item.
#### Kekurangan
- Cold Start: Tidak dapat merekomendasikan anime baru tanpa interaksi pengguna.
- Kurang Transparan: Sulit menjelaskan alasan mengapa suatu anime direkomendasikan.
<!-- Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih. -->

## Evaluation
<!-- Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja. -->

Dalam proyek Collaborative Filtering ini, metrik evaluasi yang digunakan untuk mengukur kinerja model adalah:


#### **1. Precision\@K**
Proporsi item relevan (positif) di antara *K* item teratas yang direkomendasikan oleh sistem. Dalam proyek ini precision\@K digunakan untuk mengevaluasi akurasi dari hasil rekomendasi dengan 2 pendekatan yaitu berdasarkan genre dan relevansi dari user (rating tinggi oleh user yang sama). Semakin tinggi nilai precision, semakin tepat rekomendasi yang diberikan.

$$
\text{Precision@K} = \frac{\text{Jumlah item relevan dalam top K}}{K}
$$

#### **2. Recall\@K**
Proporsi item relevan yang berhasil ditangkap oleh sistem dalam *K* item teratas yang direkomendasikan. Metrik ini menunjukkan sejauh mana sistem berhasil merekomendasikan seluruh item yang relevan bagi user. Nilai yang tinggi menunjukkan bahwa sistem mampu mencakup banyak preferensi user.

$$
\text{Recall@K} = \frac{\text{Jumlah item relevan dalam top K}}{\text{Jumlah total item relevan milik user}}
$$


#### **3. F1-score\@K**

Rata-rata harmonik dari Precision\@K dan Recall\@K, yang merepresentasikan trade-off antara akurasi dan kelengkapan rekomendasi. Metrik kombinasi ini menyeimbangkan antara Precision dan Recall. Metrik ini berguna dalam menilai performa sistem secara keseluruhan tanpa mengutamakan salah satu aspek saja (baik akurasi maupun kelengkapan).

$$
\text{F1@K} = \frac{2 \cdot \text{Precision@K} \cdot \text{Recall@K}}{\text{Precision@K} + \text{Recall@K}}
$$




Sementara proyek Collaborative Filtering ini, metrik evaluasi yang digunakan untuk mengukur kinerja model adalah:

#### **1. Root Mean Squared Error (RMSE)**

RMSE mengukur akar rata-rata dari kuadrat selisih antara rating asli dan rating prediksi. Formula RMSE adalah:

$$
\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^n (y_i - \hat{y}_i)^2}
$$

  di mana $y_i$ adalah rating asli, $\hat{y}_i$ adalah rating prediksi, dan $n$ adalah jumlah data. RMSE memberikan bobot lebih besar pada kesalahan yang besar, sehingga lebih sensitif terhadap prediksi yang jauh dari nilai asli.
- Semakin kecil nilai MAE, maka akurasi model semakin baik, karena kesalahan rata-rata antara hasil prediksi dan nilai sebenarnya tergolong rendah.
- Sebaliknya, semakin besar nilai MAE, maka akurasi model semakin buruk, karena menunjukkan bahwa prediksi model sering meleset jauh dari nilai sebenarnya.

**Cara Kerja:**
1. **Hitung Selisih Absolut:** Untuk setiap data, kita hitung selisih antara nilai prediksi model dengan nilai aktualnya. Selisih ini kemudian kita ambil nilai absolutnya (artinya kita abaikan tanda positif atau negatif).
2. **Hitung Rata-rata:** Setelah mendapatkan semua selisih absolut, kita hitung rata-rata dari semua selisih tersebut. Hasilnya adalah nilai MAE.


#### **2. Mean Absolute Error (MAE)**

MAE menghitung rata-rata dari nilai absolut selisih antara rating asli dan prediksi. Formula MAE adalah:

$$
\text{MAE} = \frac{1}{n} \sum_{i=1}^n |y_i - \hat{y}_i|
$$

  MAE memberikan gambaran rata-rata kesalahan dalam satuan yang sama dengan rating, sehingga lebih mudah diinterpretasikan.
- Semakin kecil nilai RMSE, maka kinerja model semakin baik, karena menunjukkan bahwa prediksi model umumnya mendekati nilai sebenarnya.
- Sebaliknya, semakin besar nilai RMSE, maka tingkat kesalahan prediksi semakin tinggi, menandakan bahwa model sering membuat prediksi yang jauh dari nilai aktual.

**Cara Kerja RMSE:**

Hitung Selisih Kuadrat: Untuk setiap data, kita hitung selisih antara nilai prediksi model dengan nilai aktualnya. Selisih ini kemudian kita kuadratkan.
Hitung Rata-rata: Setelah mendapatkan semua selisih kuadrat, kita hitung rata-rata dari semua selisih kuadrat tersebut.
Akar Kuadrat: Terakhir, kita ambil akar kuadrat dari hasil rata-rata selisih kuadrat.


### Hasil Evaluasi Proyek

Setelah dilakukan pada evaluasi model Content-Based Recommendation menghasilkan:

* Average Genre Precision@K: 1.0000
* Average Precision@K: 0.0479
* Average Recall@K: 0.0341
* Average F1@K: 0.0244

Pada metrik pertama digunakan untuk mengukur apakah sistem rekomendasi berhasil menyarankan anime yang memiliki genre yang sama dengan anime query. Dan ketiga metrik lainnya digunakan untuk mengevaluasi sejauh mana sistem rekomendasi mampu menyarankan anime yang relevan menurut preferensi pengguna. Relevansi diukur berdasarkan apakah anime yang direkomendasikan juga diberi rating tinggi oleh user yang sama. Nilai Precision@K menunjukkan proporsi anime relevan dalam K rekomendasi teratas, Recall@K mengukur proporsi anime relevan yang berhasil ditemukan, dan F1@K adalah harmonisasi antara precision dan recall.

Sistem rekomendasi menunjukkan kesesuaian genre yang sangat baik (Precision genre = 1.0), yang berarti sistem berhasil menyarankan anime-anime dengan genre yang mirip. Namun, tingkat relevansi berdasarkan rating pengguna masih rendah (Precision@10 < 0.05), mengindikasikan bahwa meskipun genre-nya cocok, belum tentu rekomendasinya dianggap relevan atau menarik oleh pengguna. Ini membuka peluang untuk perbaikan lebih lanjut, misalnya menggabungkan CBF dengan data interaksi pengguna (hybrid model).

Sementara evaluasi model Collaborative Filtering pada data validasi, diperoleh hasil:

* RMSE: 0.2747
* MAE: 0.2192

Nilai RMSE dan MAE yang relatif kecil ini menunjukkan model mampu memprediksi rating dengan tingkat akurasi yang baik. Model dapat memahami preferensi pengguna dan memberikan rekomendasi anime yang sesuai dengan minat mereka.


## Kesimpulan
- Genre anime apa saja yang paling diminati oleh pemirsa?
- Bagaimana merekomendasikan anime kepada pengguna berdasarkan preferensi pengguna?
- Bagaimana merekomendasikan anime berdasarkan genre dengan anime yang disukai pengguna?
  
1. Berdasarkan data yang diperoleh dapat diketahui genre-genre anime yang paling diminati oleh pemirsa yaitu Hentai, Comedy, Music, Kids, Slice of Lice, Dementia.
2. Penerapan metode collaborative filtering berbasis pengguna memungkinkan sistem rekomendasi memberikan rekemondasi anime yang sesuai dengan referensi pemirsa.
3. Melalui pendekatan content-based recommendation, sistem dapat merekomendasikan anime berdasarkan kemiripan genre.

## References
[1] . Jozuka, E. (2019). Japanese anime: From ‘Disney of the East’ to a global industry worth billions. CNN. Diakses dari https://edition.cnn.com/style/article/japan-anime-global-identity-hnk-intl

[2]. Sckit-Learn, diakses 5 Juni 2025, https://scikit-learn.org/dev/modules/generated/sklearn.preprocessing.MultiLabelBinarizer.html

[3]. Denise Chen, diakses 5 Juni 2025, https://towardsdatascience.com/recommender-system-singular-value-decomposition-svd-truncated-svd-97096338f361
