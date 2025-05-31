# Laporan Proyek Machine Learning - Mikacinta Gustina Amalan Toyibah

## Project Overview

Pariwisata merupakan salah satu sektor strategis dalam pembangunan ekonomi Indonesia. Berdasarkan data Badan Pusat Statistik (BPS), jumlah perjalanan wisatawan nusantara pada tahun 2023 mencapai 741,82 juta perjalanan, meningkat 11,45% dibandingkan tahun sebelumnya. Sementara itu, jumlah kunjungan wisatawan mancanegara (wisman) juga mengalami peningkatan signifikan. Hingga Oktober 2023, total kunjungan mencapai hampir 9,5 juta, melampaui target tahunan sebesar 8,5 juta kunjungan. Informasi ini disampaikan oleh Kementerian Pariwisata dan Ekonomi Kreatif (Kemenparekraf) dalam siaran pers resmi. Namun demikian, data menunjukkan bahwa kunjungan wisatawan—baik domestik maupun mancanegara—masih terkonsentrasi di destinasi wisata populer seperti Bali, Yogyakarta, dan Bandung. Dalam laporan "Statistik Wisatawan Nusantara 2023", provinsi-provinsi dengan infrastruktur dan promosi wisata yang kuat mendominasi jumlah perjalanan. Hal ini mengindikasikan adanya ketimpangan distribusi wisatawan, yang dapat menimbulkan fenomena overtourism di satu sisi, dan kurangnya eksposur terhadap destinasi potensial di sisi lainnya.

Di sisi lain, dengan semakin meluasnya akses internet, sebagian besar wisatawan kini merencanakan perjalanannya secara mandiri. Berdasarkan laporan Google Travel Trends 2023, sebanyak 68% wisatawan Indonesia mencari inspirasi wisata melalui internet. Namun, 52% di antaranya merasa kewalahan karena terlalu banyak pilihan informasi yang tersedia secara daring (information overload). Akibatnya, calon wisatawan justru mengalami kesulitan dalam menentukan tujuan yang sesuai dengan preferensi dan kebutuhan mereka. Kondisi tersebut menegaskan pentingnya pemanfaatan teknologi cerdas untuk membantu wisatawan dalam proses pengambilan keputusan. Teknologi seperti recommender system berbasis kecerdasan buatan (Artificial Intelligence) dapat menjadi solusi untuk memberikan rekomendasi destinasi wisata yang personal dan relevan bagi setiap individu. Dengan mempertimbangkan preferensi pengguna, jenis wisata yang disukai, anggaran, jarak, dan waktu perjalanan, sistem ini akan mempermudah wisatawan menemukan destinasi yang tepat dan sesuai kebutuhan.

Selain membantu wisatawan, sistem rekomendasi ini juga dapat berperan dalam mendukung strategi pemerataan pariwisata nasional. Dengan memperkenalkan destinasi yang kurang populer namun potensial, model ini turut berkontribusi dalam pengembangan daerah serta mendorong terciptanya ekosistem pariwisata yang lebih inklusif. Pengembangan model ini sejalan dengan visi transformasi digital sektor pariwisata Indonesia, seperti yang dicanangkan oleh Kemenparekraf melalui program “Digital Tourism”, yang mendorong pemanfaatan teknologi untuk meningkatkan daya saing industri pariwisata di era digital.

**Sumber**:
- Badan Pusat Statistik. (2024). Statistik wisatawan nusantara 2023. [Statistik Wisatawan Nusantra 2023](https://www.bps.go.id/id/publication/2024/05/23/9bbe16f7f850126353cea5d2/statistik-wisatawan-nusantara-2023.html)
- Kementerian Pariwisata dan Ekonomi Kreatif. (2023). Jumlah kunjungan wisman hingga Oktober 2023 capai 9,5 juta, lampaui target tahunan 8,5 juta kunjungan [Siaran Pers Kemenparekraf 2023](https://kemenparekraf.go.id/berita/siaran-pers-jumpa-pers-akhir-tahun-kemenparekraf-paparkan-capaian-kinerja-di-sepanjang-2023)
- Google. (2023). Google travel trends Indonesia 2023: Bagaimana orang Indonesia merencanakan perjalanan mereka. [Google Travel Report 2023](https://www.thinkwithgoogle.com/_qs/documents/18369/google_travel_report_2023.pdf)


## Business Understanding

### Problem Statements

Menjelaskan pernyataan masalah:
- Bagaimana cara membantu wisatawan dalam menemukan destinasi wisata yang sesuai dengan preferensi pribadi mereka secara efisien?
- Bagaimana cara memberikan rekomendasi 10 destinasi wisata terbaik di kota-kota Indonesia, yang sesuai dengan preferensi destinasi pengguna?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Mengembangkan sistem rekomendasi destinasi wisata yang dapat memberikan hasil personalisasi berdasarkan konten deskripsi destinasi dan preferensi pengguna dengan teknik Content-based Filtering dan Collaborative Filtering.
- Memberikan top-10 rekomendasi sesuai dengan preferensi destinasi serupa.

### Solution statements
- Menggunakan pendekatan Content-Based Filtering dengan TF-IDF dan Cosine Similarity, hal ini untuk memanfaatkan deskripsi tempat wisata untuk mengukur kemiripan antar destinasi
- Menggunakan pendekatan Collaborative Filtering dengan menggunakan data interaksi pengguna (rating) untuk mencari pola kesamaan antar pengguna. 

## Data Understanding
Dataset yang digunakan berasal dari Kaggle dan memiliki 4 file csv berbeda. Dataset dapat diunduh pada link berikut ini: [Indonesia Tourism Destinantion Data](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination/data)

Variabel-variabel pada Indonesia Tourism Destination dataset adalah sebagai berikut:
- **user.csv**: berisi informasi ID pengguna dan data demografi.
- **paket_tourism.csv**: berisi daftar paket wisata dengan deskripsi destinasi.
- **rating_tourism.csv**: berisi data rating wisatawan terhadap destinasi tertentu.
- **place_list.csv**: berisi daftar destinasi wisata beserta ID tempat.

Variabel penting yang digunakan dalam proyek ini antara lain:
- Place_Id: ID tempat wisata
- Place_Name: nama tempat wisata
- Description: deskripsi destinasi (digunakan dalam content-based)
- City: kota tujuan
- User_Id: ID pengguna
- Rating: nilai rating yang diberikan pengguna
- Category: jenis wisata

**Teknik Visualisasi data dan Exploratory Data Analysis dengan Univariate Analysis**:
- Visualisasi 10 tempat wisata dengan rating terbanyak
  ![10 wisata rating terbanyak](https://github.com/user-attachments/assets/8e2a4aad-61d1-4ea5-8006-9bd6959907cb)

- Pemetaan sebaran pada kategori wisata di Yogyakarta
  ![perbandingan kategori wisata di yogyakarta](https://github.com/user-attachments/assets/88bc9abe-7c3a-4f61-8a4c-b8101174537e)

- Visualisasi Distribusi Usia Pengguna

  ![distribusi usia pengguna](https://github.com/user-attachments/assets/7bc62f43-7337-4ca4-b612-b5a75728d583)

- Visualisasi Distribusi Harga Masuk Wisata

  ![distribusi harga masuk wisata](https://github.com/user-attachments/assets/a540d527-26fa-4b67-a559-09cf977dec7e)

- Pemetaan Jumlah Asal Kota Pengguna
  ![jumlah asal kota pengguna](https://github.com/user-attachments/assets/1ae9f9f9-decb-429a-8126-e67f8d77285a)



## Data Preparation

Tahapan data preparation dilakukan sebagai berikut:

1. **Merge Data**  
   Menggabungkan data tourism_rating dan tourism_with_id berdasarkan `place_id` untuk memperkaya informasi tempat wisata
   
2. **Cleaning Text**  
   - Mengubah teks deskripsi menjadi lowercase.
   - Menghapus stopwords.
   - Lemmatization (mengurangi kata ke bentuk dasar).
     
3. **TF-IDF Vectorizer** digunakan untuk melakukan vectorisasi terhadap teks deskripsi tempat wisata. TF-IDF sangat efektif untuk ekstraksi fitur dari teks lain dalam conten-based.
4. **Normalization dan Filtering**  
   Melakukan normalisasi rating menggunakan **MinMaxScaler** untuk model embedding agar model lebih mudah dilatih. Hal inio juga dilakukan untuk menghilangkan user atau destinasi dengan terlalu sedikit interaksi (noise reduction).
5. Mengidentifikasi Missing Value
   Memastikan tidak ada data yang kosong yang dapat mengganggu proses training atau rekomendasi
6. Menghapus Duplikasi Data
   Data yang duplikat dihapus untuk menghindari redudansi data pada tempat wisata yang sama
8. Encoding Representasi Teks (TF-IDF Vectorization)
   Melakukan encoding pada variabel target kategori agar memiliki skala yang sama
9. Train-Test-Split
   Memlakukan pembagian data menjadi data latih dan data uji dengan proporsi 80:20.


## Modeling

1. Pemodelan dengan Content-Based Filtering menggunakan TF-IDF Vectorizer dan Cosihne Similarity

Dengan menggunakan Content-Based Filtering dilakukan dengan menggunakan TF-IDF dari kolom Description untuk menghitung cosine similarity antar tempat wisata. Selanjutnya Rekomendasi diberikan berdasarkan destinasi yang paling mirip dengan input pengguna.
 
   - **TF-IDF Vectorinizer**
     
     $$ TF-IDF = Term Frequency – Inverse Document Frequency $$

     - Representasi Fitur: Mengubah konten  menjadi bentuk vektor agar bisa dihitung kemiripannya
     - Mengukur Kemiripan: Memungkinkan perhitungan cosine similarity antar item untuk mencari item yang mirip
     - Fokus pada kata penting**: TF-IDF memberi bobot lebih tinggi pada kata khas item, bukan kata umum
     - Top-N Recommendation: Mengambil 10 destinasi dengan skor kesamaan tertinggi (kecuali destinasi yang sedang dicari).

   - **Cosine Similarity**
     Cosine Similarity mengukur kemiripan antara dua vektor berdasarkan sudut (bukan panjangnya).

Nilai berada di antara `-1` hingga `1`:

`1` → sangat mirip (arah vektor sama)

`0` → tidak mirip (tegak lurus)

`-1` → berlawanan (jarang terjadi di NLP)


**Rumus Cosine Similarity**

$$
\text{cosine_similarity}(A, B) = \frac{A \cdot B}{\|A\| \times \|B\|}
$$

Keterangan:
- $ A \cdot B $: dot product antara vektor A dan B  
- $ \|A\| $: panjang (norma) dari vektor A  
- $ \|B\| $: panjang (norma) dari vektor B

Dengan menggunakan argpartition, kita mengambil sejumlah nilai `k` tertinggi dari similarity data (dalam kasus ini: `dataframe cosine_sim_df`). Kemudian, mengambil data dari bobot (tingkat kesamaan) tertinggi ke terendah. Lalu menghapus `place_name` yang yang dicari agar tidak muncul dalam daftar rekomendasi.

Hasil: Sistem merekomendasikan 5 tempat wisata, dan 4 sesuai selera user berdasarkan input →

```
Input: 'Candi Prambanan', category = Budaya
Dataset:
0 - Candi Ratu Buko                        → Budaya ✅
1 - Taman Budaya Yogyakarta                → Budaya ✅
2 - Monumen Yogya Kembali                  → Budaya ✅
3 - Museum Benteng Vredeburg Yogyakarta    → Budaya ✅
4 - Bukit Panguk Kediwung                  → Budaya ✅
```

$$
Precision@5=\dfrac{5}{5}= 1.00
$$

Hasil Top-5-Content-Based Filtering
![image](https://github.com/user-attachments/assets/906037d5-b697-496d-b13d-735f388292c8)


Content-Based Filtering memiliki kelebihan mudah dalam pengimplementasiannya dan tidak memerlukan interaksi dari pengguna sebelumnya. Sedangkan kekurangannya adalah model ini tidak dapat menangkap preferensi pengguna secara personal


2. Pemodelan dengan Collaborative Filtering menggunakan pendekatan **embedding matrix** dan **dot product**.

Collaborative Filtering dilakukan menggunakan pendekatan matrix factorization (SVD dari scikit-surprise) untuk mempelajari preferensi pengguna berdasarkan rating. Model SVD mampu menangkap hubungan laten antara user dan destinasi. Model dievaluasi dengan menggunakan metrik RMSE antara rating prediksi dan rating aktual. Untuk merekomendasikan tempat wisata yang belum pernah dikunjungi oleh pengguna, dibuat variabel place_not_visited. Rekomendasi ini dilakukan hanya pada destinasi yang belum pernah dikunjungi pengguna. Pada tahap ini, model menghitung skor kecocokan antara pengguna dan tempat wisata dengan **teknik embedding**. Selanjutnya, lakukan operasi **perkalian dot product** antara embedding user dan place. Selain itu, kita juga dapat menambahkan *bias* untuk setiap user dan place. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi **aktivasi sigmoid**. Model ini menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation. 

Hasil Collaborative Filtering

![model_metrics](https://github.com/user-attachments/assets/d1317297-bbf7-4562-b972-cd91aa664206)

Perhatikanlah, proses training model cukup smooth dan model konvergen pada epochs sekitar 50. Dari proses ini, diperoleh nilai error akhir sebesar sekitar 0.31 dan error pada data validasi sebesar 0.35. Nilai tersebut cukup bagus untuk sistem rekomendasi.

Jumlah Rating Tertinggi Pengguna
![image](https://github.com/user-attachments/assets/d94c2fd2-86c7-41e9-b2c5-1f01d1d753ca)

Top 10 Rekomendasi Wisata
![image](https://github.com/user-attachments/assets/d5ef8461-d99e-4a5a-b1fd-fe6b4b2ebd97)


Kelebihan dari Collaborative Filtering adalah dapat memahami preferensi pengguna dan rekomendasinya personal. Kekurangan dari model ini membutuhkan interaksi pengguna yang cukup banyak



## Evaluation

**Metrik Evaluasi yang Digunakan**

Precision

Precision mengukur seberapa banyak rekomendasi yang benar dari total yang diberikan.

$$
\text{Precision@k} = \frac{\text{Jumlah item relevan dalam top-}k}{k}
$$


Fokus: Akurasi dari hasil yang ditampilkan ke user.

RMSE

![image](https://github.com/user-attachments/assets/78e43791-b974-4498-9eba-e9605784f196)


Hasil: Sistem merekomendasikan 5 tempat wisata, dan 4 sesuai selera user berdasarkan input →

```
Input: 'Candi Prambanan', category = Budaya
Dataset:
0 - Candi Ratu Buko                        → Budaya ✅
1 - Taman Budaya Yogyakarta                → Budaya ✅
2 - Monumen Yogya Kembali                  → Budaya ✅
3 - Museum Benteng Vredeburg Yogyakarta    → Budaya ✅
4 - Bukit Panguk Kediwung                  → Budaya ✅
```

$$
Precision@5=\dfrac{5}{5}= 1.00
$$

Hasil Content-Based Filtering
![image](https://github.com/user-attachments/assets/906037d5-b697-496d-b13d-735f388292c8)


- **Accuracy**: Persentase prediksi yang benar dari total prediksi.
- **Precision**: Kemampuan model untuk tidak salah menandai contoh negatif sebagai positif.

Untuk mendapatkan rekomendasi tempat wisata, diambil sampel user secara acak dan definisikan variabel `place_not_visited` yang merupakan daftar wisata yang belum pernah dikunjungi oleh pengguna. Rating digunakan untuk membuat rekomendasi wisata yang mungkin cocok untuk pengguna.


Visualisasi Metriks

![model_metrics](https://github.com/user-attachments/assets/d1317297-bbf7-4562-b972-cd91aa664206)

Hasil Collaborative Filtering
Jumlah Rating Tertinggi Pengguna
![image](https://github.com/user-attachments/assets/d94c2fd2-86c7-41e9-b2c5-1f01d1d753ca)

Top 10 Rekomendasi Wisata
![image](https://github.com/user-attachments/assets/d5ef8461-d99e-4a5a-b1fd-fe6b4b2ebd97)


Perhatikanlah, proses training model cukup smooth dan model konvergen pada epochs sekitar 50. Dari proses ini, diperoleh nilai error akhir sebesar sekitar 0.31 dan error pada data validasi sebesar 0.35. Nilai tersebut cukup bagus untuk sistem rekomendasi.
Proyek ini berhasil mengembangkan sistem rekomendasi destinasi wisata berbasis content-based filtering dan collaborative filtering. Berdasarkan evaluasi, sistem ini mampu memberikan rekomendasi yang relevan dengan preferensi pengguna (Precision@5 = 1.0) dan memiliki error yang relatif rendah (RMSE = 0.35). Hal ini menunjukkan bahwa sistem rekomendasi yang dikembangkan dapat membantu wisatawan menemukan destinasi yang sesuai dengan preferensi mereka, mengurangi information overload, dan mendukung pemerataan pariwisata di Indonesia.

Implementasi sistem ini diharapkan dapat membantu pemerintah dan industri pariwisata untuk mempromosikan destinasi-destinasi yang kurang populer namun potensial, sehingga pembangunan pariwisata di Indonesia menjadi lebih inklusif.
