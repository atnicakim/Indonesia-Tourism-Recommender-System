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
Dataset yang digunakan berasal dari Kaggle dan memiliki 4 file csv berbeda. Dataset dapat diunduh pada link berikut ini: [Indonesia Tourism Destinantion Data](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination/data). 

Jumlah data informasi destinasi wisata:  437
Jumlah data penilaian oleh pengguna:  437
Jumlah data pengguna:  300
Jumlah data paket wisata:  100

package_tourism.csv: 100 baris × 7 kolom
tourism_rating.csv: 10.000 baris × 3 kolom
tourism_with_id.csv: 437 baris × 13 kolom
user.csv: 300 baris × 3 kolom

Jumlah missing value kolom Time_Minutes di dataset tourism_with_id.csv adalah 232

Variabel-variabel pada Indonesia Tourism Destination dataset adalah sebagai berikut:

- **user.csv**: berisi informasi ID pengguna dan data demografi. Meliputi fitur:
   - user_id — ID unik untuk setiap pengguna.
   - location — Lokasi pengguna.
   - age — Usia pengguna.

- **package_tourism.csv**: berisi daftar paket wisata dengan deskripsi destinasi. Meliputi fitur:
   - package — ID unik untuk setiap paket wisata.
   - city — Nama kota tempat destinasi wisata berada.
   - Place_Tourism1 – Nama destinasi pertama yang termasuk dalam paket
   - Place_Tourism2 – Nama destinasi kedua yang termasuk dalam paket
   - Place_Tourism3 – Nama destinasi ketiga yang termasuk dalam paket
   - Place_Tourism4 – Nama destinasi keempat yang termasuk dalam paket
   - Place_Tourism5 – Nama destinasi kelima yang termasuk dalam paket

- **tourism_rating.csv**: berisi data rating wisatawan terhadap destinasi tertentu. Meliputi fitur:
   - user_id — ID unik pengguna yang memberikan rating.
   - place_id — ID destinasi wisata yang dinilai.
   - place_ratings — Skor penilaian yang diberikan pengguna (dalam skala 1–5).

- **tourism_with_id.csv**: berisi daftar destinasi wisata beserta ID tempat. Meliputi fitur:
   - place_id — ID unik destinasi wisata.
   - place_name — Nama destinasi wisata.
   - description — Deskripsi destinasi wisata.
   - category — Kategori wisata (misalnya: Budaya, dll).
   - city — Kota tempat destinasi wisata berada.
   - price — Harga tiket atau biaya masuk (angka).
   - rating — Rating rata-rata destinasi wisata (angka).
   - time_minutes — Estimasi waktu kunjungan dalam menit.
   - coordinate — representasi koordinat destinasi wisata
   - lat — Latitude (garis lintang) untuk koordinat destinasi wisata.
   - long — Longitude (garis bujur) untuk koordinat destinasi wisata.
   - Unnamed: 11 — Kolom tidak bernama, sepenuhnya kosong, tidak ada informasi dan nilai apapun di seluruh baris, kemungkinan noise.
   - Unnamed: 12 — Kolom tidak bernama, kemungkinan merupakan duplikasi dari kolom place_id.



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

1. **Pembersihan kolom Unnamed**  
   Menghapus kolom Unnamed:11 dan Unnamed:12 dari dataset wisata karena tidak terpakai
2. **Merge Data**  
   Menggabungkan data tourism_rating dan tourism_with_id berdasarkan `place_id` untuk memperkaya informasi tempat wisata
3. **Pembuatan Fitur city_category**  
   Dibuat fitur city_category untuk menemukan representasi fitur penting dari setiap kategori wisata
4. **Mengidentifikasi Missing Value**  
   Memastikan tidak ada data yang kosong yang dapat mengganggu proses training atau rekomendasi
5. **Menghapus Duplikasi Data**  
   Data yang duplikat dihapus untuk menghindari redudansi data pada tempat wisata yang sama
6. **TF-IDF Vectorizer**   digunakan untuk melakukan vectorisasi terhadap teks deskripsi tempat wisata. TF-IDF sangat efektif untuk ekstraksi fitur dari teks lain dalam conten-based.
7. **Encoding Representasi Teks (TF-IDF Vectorization)**  
   Melakukan encoding pada UserId dan PlaceId untuk model Collaborative Filtering
8. **Pengacakan Data (Shuffling)**  
   Melakukan pengacakan data sebelum membagi data latih dan data uji untuk Collaborative Filtering
9. **Normalization**  
   Melakukan normalisasi rating menggunakan **MinMaxScaler** untuk model embedding agar model lebih mudah dilatih.
10. **Train-Test-Split**  
   Memlakukan pembagian data menjadi data latih dan data uji dengan proporsi 80:20.


## Modeling

1. Pemodelan dengan Content-Based Filtering menggunakan TF-IDF Vectorizer dan Cosihne Similarity

Content-Based Filtering adalah metode rekomendasi yang bekerja dengan membandingkan fitur atau atribut dari item dengan preferensi pengguna, lalu merekomendasikan item serupa berdasarkan konten tersebut. Sistem membuat representasi fitur dari setiap destinasi wisata, kemudian ketika pengguna memiliki riwayat preferensi atau pilihan destinasi tertentu, sistem akan mencari destinasi lain yang mirip dengan destinasi tersebut.

Content-Based Filtering dilakukan dengan menggunakan TF-IDF dari kolom city_category untuk menghitung cosine similarity antar tempat wisata. Selanjutnya Rekomendasi diberikan berdasarkan destinasi yang paling mirip dengan input pengguna.
 
   - **TF-IDF Vectorinizer**
     
     $$ TF-IDF = Term Frequency – Inverse Document Frequency $$

     - Representasi Fitur: Mengubah konten  menjadi bentuk vektor agar bisa dihitung kemiripannya
     - Mengukur Kemiripan: Memungkinkan perhitungan cosine similarity antar item untuk mencari item yang mirip
     - Fokus pada kata penting: TF-IDF memberi bobot lebih tinggi pada kata khas item, bukan kata umum
     - Top-N Recommendation: Mengambil 10 destinasi dengan skor kesamaan tertinggi (kecuali destinasi yang sedang dicari).

   - **Cosine Similarity**
     Cosine Similarity mengukur kemiripan antara dua vektor berdasarkan sudut (bukan panjangnya).

Nilai berada di antara `-1` hingga `1`:

`1` → sangat mirip (arah vektor sama)

`0` → tidak mirip (tegak lurus)

`-1` → berlawanan (jarang terjadi di NLP)


**Rumus Cosine Similarity**

$$
\text{cosine\_similarity}(A, B) = \frac{A \cdot B}{\|A\| \times \|B\|}
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

Collaborative Filtering dilakukan menggunakan jaringan neural kustom (RecommenderNet) dengan Keras Embedding Layers dan dot product untuk mempelajari preferensi pengguna berdasarkan rating. Model dievaluasi dengan menggunakan metrik RMSE antara rating prediksi dan rating aktual. Untuk merekomendasikan tempat wisata yang belum pernah dikunjungi oleh pengguna, dibuat variabel place_not_visited. Rekomendasi ini dilakukan hanya pada destinasi yang belum pernah dikunjungi pengguna. Pada tahap ini, model menghitung skor kecocokan antara pengguna dan tempat wisata dengan **teknik embedding**. Selanjutnya, lakukan operasi **perkalian dot product** antara embedding user dan place. Selain itu, kita juga dapat menambahkan *bias* untuk setiap user dan place. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi **aktivasi sigmoid**. Model ini menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation. 

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



- **Accuracy**: Persentase prediksi yang benar dari total prediksi.
- **Precision**: Kemampuan model untuk tidak salah menandai contoh negatif sebagai positif.

Untuk mendapatkan rekomendasi tempat wisata, diambil sampel user secara acak dan definisikan variabel `place_not_visited` yang merupakan daftar wisata yang belum pernah dikunjungi oleh pengguna. Rating digunakan untuk membuat rekomendasi wisata yang mungkin cocok untuk pengguna.


Visualisasi Metriks

![model_metrics](https://github.com/user-attachments/assets/d1317297-bbf7-4562-b972-cd91aa664206)

Hasil Collaborative Filtering
Jumlah Rating Tertinggi Pengguna
![image](https://github.com/user-attachments/assets/d94c2fd2-86c7-41e9-b2c5-1f01d1d753ca)



Perhatikanlah, proses training model cukup smooth dan model konvergen pada epochs sekitar 50. Dari proses ini, diperoleh nilai error akhir sebesar sekitar 0.31 dan error pada data validasi sebesar 0.35. Nilai tersebut cukup bagus untuk sistem rekomendasi.
Proyek ini berhasil mengembangkan sistem rekomendasi destinasi wisata berbasis content-based filtering dan collaborative filtering. Berdasarkan evaluasi, sistem ini mampu memberikan rekomendasi yang relevan dengan preferensi pengguna (Precision@5 = 1.0) dan memiliki error yang relatif rendah (RMSE = 0.35). Hal ini menunjukkan bahwa sistem rekomendasi yang dikembangkan dapat membantu wisatawan menemukan destinasi yang sesuai dengan preferensi mereka, mengurangi information overload, dan mendukung pemerataan pariwisata di Indonesia.

Model Content-Based Filtering menggunakan TF-IDF dan Cosine Similarity berhasil memanfaatkan deskripsi destinasi wisata untuk mengukur kemiripan antar destinasi. Dengan demikian, wisatawan dapat menemukan destinasi wisata yang sesuai dengan preferensi pribadi mereka dengan lebih efisien, melalui pencarian destinasi yang memiliki deskripsi mirip dengan destinasi favorit mereka. Implementasi model Collaborative Filtering memanfaatkan data rating pengguna terhadap destinasi untuk menemukan pola kesamaan antar pengguna, sehingga dapat merekomendasikan destinasi yang disukai oleh pengguna dengan preferensi serupa. Selain itu, dengan top-N recommendation (top-10), sistem ini efektif memberikan 10 destinasi wisata terbaik yang relevan secara personal bagi pengguna.

Model Content-Based Filtering (menggunakan TF-IDF dan Cosine Similarity) memanfaatkan deskripsi destinasi wisata untuk mencocokkan kesamaan antar destinasi berdasarkan kata-kata kunci yang relevan. Model Collaborative Filtering menggunakan rating pengguna untuk memodelkan preferensi personal berdasarkan pola interaksi dengan destinasi wisata. Kedua model yang dikembangkan berhasil menghasilkan daftar rekomendasi destinasi wisata dalam bentuk top-10, yang membantu pengguna menemukan tempat wisata sesuai dengan preferensi mereka. Model collaborative filtering menggunakan user-based similarity untuk menghasilkan rekomendasi berbasis kesamaan preferensi pengguna, sedangkan content-based filtering fokus pada kemiripan deskripsi destinasi.

Dengan menggunakan model Content-Based Filtering (menggunakan TF-IDF dan Cosine Similarity), model ini mampu membantu wisatawan menemukan destinasi yang mirip dengan destinasi favorit mereka. tampak positif terlihat dalam hasil evaluasi berupa kemiripan yang tinggi antar destinasi wisata yang relevan secara konten, yang mempermudah pengguna untuk memilih destinasi sesuai preferensi mereka.

Dengan menggunakan pendekatan Collaborative Filtering berbasis rating pengguna, model ini berhasil merekomendasikan destinasi wisata berdasarkan kesamaan pola preferensi pengguna lain. Dampaknya terlihat pada hasil evaluasi model yang menunjukkan bahwa destinasi yang disarankan memiliki rating yang relevan dan personal bagi pengguna. Dengan pendekatan ini, pengguna bisa mendapatkan rekomendasi yang lebih bervariasi dan sesuai selera pengguna lain dengan preferensi serupa.

Implementasi sistem ini diharapkan dapat membantu pemerintah dan industri pariwisata untuk mempromosikan destinasi-destinasi yang kurang populer namun potensial, sehingga pembangunan pariwisata di Indonesia menjadi lebih inklusif.
