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
Dataset ini berisi informasi deskriptif mengenai judul anime dan memiliki **12.017 baris dan 7 kolom**.

| Kolom     | Tipe Data                 | Keterangan                                  |
| --------- | ------------------------- | ------------------------------------------- |
| anime\_id | Numerik (int)             | ID unik untuk tiap anime                    |
| name      | Kategorikal (string)      | Judul anime                                 |
| genre     | Kategorikal (string/list) | Daftar genre (dipisahkan koma)              |
| type      | Kategorikal (string)      | Tipe anime (TV, Movie, OVA, dll)            |
| episodes  | Numerik (int)             | Jumlah episode                              |
| rating    | Numerik (float)           | Skor rata-rata pengguna                     |
| members   | Numerik (int)             | Jumlah user yang memasukkan anime ke daftar |

Tabel 1. Struktur data anime.csv

#### **2. rating.csv**

Dataset ini berisi interaksi pengguna terhadap anime, dengan total **7.813.737 baris dan 3 kolom**.

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

**Kesimpulan**: Pada anime.csv, missing value ditemukan pada `genre`, `type` dan `rating`, sehingga nantinya dilakukan penghapusan baris yang mengandung missing value untuk menjaga kualitas analisis. Pada rating.csv tidak ditemukan missing value

---

### 📈 Deskripsi Statistik

#### **anime.csv (Setelah pembersihan)**

| Kolom   | Mean   | Median | Min  | Max       |
| ------- | ------ | ------ | ---- | --------- |
| rating  | 6.48   | 6.57   | 1.67 | 10.00     |
| members | 18.348 | 1.552  | 12   | 1.013.917 |

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

<!-- Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut. -->


## Modeling

### Content Based recomendation
Dengan menggunakan TF-IDF Vectorizer data teks ditransformasikan menjadi representasi angka yang memiliki makna terntentu kedalam bentuk matriks. Selanjutnya matriks tersebut akan dihitung derajat kesamaanya dengan menggunakan Cosine Similarity antar judul dari anime. Langkah-langkahnya adalah sebagai berikut.

#### Persiapan Data
Langkah awal dalam pengembangan sistem rekomendasi berbasis konten (content-based filtering) adalah menyusun data yang relevan. Data yang digunakan terdiri dari kolom:
- `anime_id`
- `name` (judul anime)
- `genre` (daftar genre dipisah koma)
- `AverageRating`

#### Ekstraksi Fitur Genre dengan TF-IDF
TF-IDF Vectorizer akan mentransformasikan teks menjadi representasi angka yang memiliki makna tertentu dalam bentuk matriks. 
Hal ini perlu dilakukan untuk melakukan perhitungan dan analisis terhadap teks maka teks tersebut di transformasikan kedalam bentuk angka.Genre dari masing-masing anime diubah menjadi vektor numerik menggunakan teknik TF-IDF, yang memungkinkan untuk mengukur seberapa penting suatu genre dalam koleksi anime.
- TF-IDF diterapkan dengan tokenizer berbasis pemisah koma ', ', agar setiap genre dikenali sebagai token individual.
- Hasil vektorisasi menghasilkan 43 fitur unik genre, seperti 'action', 'drama', 'romance', 'sci-fi', 'supernatural', dan sebagainya.
- Dimensi hasil TF-IDF matrix adalah (11162, 43).

Contoh output menunjukkan bagaimana setiap anime memiliki skor representasi (bobot TF-IDF) terhadap genre-genre tertentu, yang kemudian menjadi dasar perhitungan kemiripan.

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
Metode paling umum untuk sistem rekomendasi sering kali dilengkapi dengan Collaborating Filtering (CF) yang mengandalkan kumpulan data pengguna dan item sebelumnya. adalah model faktor laten, yang mengekstraksi fitur dari matriks pengguna dan item [Denise Chen](https://towardsdatascience.com/recommender-system-singular-value-decomposition-svd-truncated-svd-97096338f361).

Berikut tahapan-tahapannya:

#### Persiapan Data
- Data difilter untuk hanya menyertakan rating ≥ 7, agar model fokus pada preferensi positif.
- Untuk menyesuaikan data dengan format yang dibutuhkan oleh model TensorFlow, dilakukan encoding ID pengguna dan anime ke dalam representasi numerik berurutan
- Nilai rating diskalakan ke rentang 0–1 karena model menggunakan fungsi aktivasi sigmoid pada output, yang menghasilkan prediksi di antara 0 dan 1.

### Pembagian Dataset

Dalam membangun model pembelajaran mesin, dataset perlu dibagi menjadi dua bagian utama:

- **Data Latih:** Digunakan untuk melatih model. Model akan mempelajari pola dan hubungan antara fitur dan target dalam data latih ini.
- **Data validasi:** Digunakan untuk menguji kinerja model yang telah dilatih. Model akan memprediksi nilai pada data uji, dan hasilnya akan dibandingkan dengan nilai sebenarnya untuk mengevaluasi seberapa baik model tersebut bekerja pada data yang belum pernah dilihat sebelumnya.

Pada proyek ini dataset dibagi 80:20. Pembagian data dengan perbandingan 80:20 adalah salah satu cara yang umum digunakan, artinya 80% data akan digunakan untuk melatih model dan 20% sisanya untuk menguji model.

Alasan utama pembagian dataset adalah untuk mengukur kemampuan generalisasi model, yaitu seberapa baik model dapat memprediksi data baru yang belum pernah dilihat sebelumnya. Dengan memisahkan sebagian data sebagai data validasi, dapat mengevaluasi apakah model mengalami overfitting (terlalu cocok dengan data latih) atau tidak, dan memastikan bahwa performanya stabil saat digunakan.


#### Fungsi Model
Menggunakan model berbasis Neural Collaborative Filtering (NCF), yang merupakan pengembangan dari matrix factorization tradisional namun dengan representasi yang lebih fleksibel dan non-linear. Model ini dirancang untuk mempelajari embedding dari pengguna dan item (anime) menggunakan arsitektur neural network

Model RecommenderNet, yaitu custom TensorFlow Keras model yang terdiri dari dua lapisan embedding (untuk user dan anime). Model ini mampu menangkap interaksi antara pengguna dan anime melalui dot product dari embedding masing-masing entitas.

Model ini menganalisis penilaian pengguna sebelumnya untuk mengenali pola preferensi serta karakteristik anime yang disukai. Berdasarkan informasi tersebut, model dapat merekomendasikan anime yang serupa dengan yang pernah disukai pengguna, atau yang diminati oleh pengguna lain dengan selera yang sejenis.

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

**Root Mean Squared Error (RMSE):**
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


**Mean Absolute Error (MAE):**
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

Setelah dilakukan evaluasi pada data validasi, diperoleh hasil:

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

[2]. Sckit-Learn, diakses 25 November 2024, https://scikit-learn.org/dev/modules/generated/sklearn.preprocessing.MultiLabelBinarizer.html

[3]. Denise Chen, diakses 25 November 2024, https://towardsdatascience.com/recommender-system-singular-value-decomposition-svd-truncated-svd-97096338f361
