# Laporan Last Project Machine Learning - Sistem Rekomendasi Aplikasi

## Project Overview

Google Play adalah platform daring yang sangat terkenal untuk menemukan aplikasi, permainan, film, acara TV, buku, dan konten lainnya. Google Play menawarkan lebih dari 2 juta aplikasi dan permainan untuk miliaran pengguna di seluruh dunia. Google Play merupakan destinasi utama bagi pengguna yang ingin menemukan aplikasi, permainan, film, acara TV, buku, dan konten lainnya. Setiap hari, Google Play diramaikan dengan kelahiran banyak aplikasi baru yang dikembangkan oleh para pengembang. Fenomena ini tentu memberikan dampak positif bagi pengguna dengan memberikan lebih banyak pilihan aplikasi yang dapat diunduh. Tetapi, hal ini juga bisa membuat pengguna merasa kebingungan dalam memilih aplikasi yang paling cocok dengan kebutuhan mereka. [[1](https://irjet.com/archives/V8/i4/IRJET-V8I4745.pdf)]. 

Sistem saran adalah sistem yang memberikan saran pada suatu item yang dapat digunakan untuk membantu pengguna dalam mengambil keputusan. [[2](https://www.researchgate.net/publication/220604600_Recommender_Systems_An_Overview)] [[3](https://www.researchgate.net/publication/258651634_A_Study_of_Recommender_System_Techniques)] [[4](https://www.researchgate.net/publication/281705736_Decision-making_in_recommender_systems_The_role_of_user's_goals_and_bounded_resources)]. Dalam konteks pengambilan keputusan untuk memilih aplikasi yang paling cocok untuk diunduh oleh pengguna Google Play, tentunya pengembangan sistem rekomendasi akan sangat berguna. Keuntungan dan dampak yang nyata dari sistem saran bagi pengguna Google Play adalah kemampuannya untuk membantu pengguna menemukan aplikasi dengan kriteria (genre, jenis, dll.) yang serupa dengan aplikasi yang telah diunduh sebelumnya oleh pengguna.

Dalam konteks pengembangan model sistem rekomendasi, terdapat beragam faktor yang dapat dipertimbangkan. [[5](https://www.researchgate.net/publication/331063850_Recommender_Systems_Challenges_and_Solutions_Survey)], Pada sistem saran aplikasi, beberapa aspek yang bisa menjadi pertimbangan termasuk Kategori, Rating, Ulasan, Ukuran, Instalasi, Jenis, Harga, Konten, Rating, Genre, Tanggal Terakhir Diperbarui, Versi Terkini, Versi Android, dan aspek lainnya. Dalam proyek ini, hanya beberapa aspek yang akan diperhatikan dalam pembuatan Model Kemiripan Cosine dan K-Nearest Neighbor. Kedua algoritma ini akan mengeksplorasi kesamaan antar data dalam fitur yang tersedia. Aspek lainnya akan diteliti dalam pengembangan model yang lebih lanjut di masa mendatang.


## Business Understanding

Pengembangan model Sistem Saran Aplikasi tentu memiliki potensi dampak atau manfaat, seperti menjadi salah satu alat bantu dalam proses pengambilan keputusan bagi pengguna Google Play. Contoh potensi manfaat dari Sistem Saran Aplikasi ini adalah membantu pengguna Google Play untuk membuat keputusan instalasi aplikasi dengan lebih cerdas.


### Problem Statements
- Berdasarkan penjelajahan dataset, apa karakteristiknya? Berapa jumlah entri data? Fitur apa yang bisa dipilih untuk pengembangan model?

- Dalam evaluasi data, apakah ada duplikat atau data yang hilang? Jika ada, langkah apa yang paling tepat untuk diambil?

- Dalam pembersihan data, apakah perlu melakukan penghapusan atau imputasi untuk memastikan kelayakan data untuk pengembangan model?

- Bagaimana cara memproses dataset untuk membuat model sistem rekomendasi?

- Bagaimana membuat model sistem rekomendasi berbasis Kemiripan Cosine dan Tetangga Terdekat-K?

- Bagaimana cara mengukur kinerja model sistem rekomendasi yang telah dibuat?

### Goals
- Menyelidiki informasi dataset dan mengevaluasi fitur yang paling cocok untuk dipilih dalam pengembangan model.

- Melakukan proses Penilaian Data untuk mendeteksi potensi keberadaan data duplikat dan data yang hilang.

- Melakukan proses Pembersihan Data dan menerapkan langkah-langkah yang paling sesuai untuk membersihkan data agar siap digunakan dalam pengembangan model.

- Melakukan persiapan Data, seperti Vektorisasi dan Pembagian Data, sebelum membangun model.

- Membuat model sistem rekomendasi berdasarkan Kesamaan Kosinus dan Tetangga Terdekat K, menggunakan fitur yang telah dipilih dari dataset.

- Menilai kinerja model sistem rekomendasi dengan menggunakan metrik evaluasi.


### Solution Approach
- Dalam rangka mengeksplorasi fitur, dilakukan Analisis Univariat. Analisis ini bertujuan untuk menyelidiki distribusi suatu fitur tertentu dalam dataset. Teknik yang digunakan mencakup visualisasi data melalui barplot dari fitur yang telah dipilih.

- Untuk memperoleh model prediksi yang optimal, langkah-langkah Data Wrangling diterapkan, mencakup Data Gathering, Data Assessing, dan Data Cleaning. Proses Data Gathering melibatkan pengambilan data dengan memuatnya dan menyimpannya dalam dataframe. Data Assessing melibatkan pemeriksaan terhadap pencilan (outlier), data duplikat, dan nilai yang hilang (missing value). Sedangkan, Data Cleaning adalah tindakan yang diambil setelah proses Data Assessing. Tindakan yang dapat diambil dalam Data Cleaning untuk menangani duplikat dan nilai yang hilang melibatkan penghapusan (dropping) baris data yang mengandung duplikat dan nilai yang hilang.

- Evaluasi performa model melibatkan penggunaan metrik evaluasi seperti Presisi (Precision), Skor Calinski Harabasz, dan Skor Davies Bouldin.


## Data Understanding
Informasi yang digunakan dalam pengembangan model bersumber dari data sekunder. Data ini diperoleh dari Kaggle dan dikenal dengan nama dataset 'Google Play Store Apps'.

URL: [https://www.kaggle.com/datasets/lava18/google-play-store-apps]

Informasi terperinci mengenai dataset yang digunakan dalam pembuatan model adalah sebagai berikut:

- Dataset terdiri dari 3 berkas CSV, yaitu googleplaystore.csv, googleplaystore_user_reviews.csv, dan license.txt.
- Dalam proyek ini, kita menggunakan dataset bernama googleplaystore.csv.
- Dataset terdiri dari 10841 entri dengan 13 fitur.
- Dari total fitur tersebut, 12 di antaranya merupakan data kategori, sementara 1 fitur bersifat numerik.
- Terdapat missing value pada dataset, dengan jumlah 1474 pada fitur Rating, 1 pada fitur Type, 1 pada fitur Content Rating, 8 pada fitur Current Ver, dan 3 pada fitur Android Ver.
  
### Berikut adalah variabel-variabel dalam dataset:

- Aplikasi : nama aplikasi
- Kategori : kategori aplikasi
- Penilaian : penilaian pengguna untuk aplikasi (dalam satuan bintang 1-5)
- Ulasan : jumlah pengguna yang memberikan ulasan pada aplikasi tersebut (dalam satuan buah)
- Ukuran : ukuran dari aplikasi (dalam satuan byte)
- Instalasi : jumlah pengguna yang meng-install aplikasi
- Jenis : jenis aplikasi (dalam kategori Berbayar atau Gratis)
- Harga : harga dari aplikasi (dalam satuan dollar USD)
- Kategori Usia : kategori usia pengguna untuk aplikasi (Semua, Dewasa 17+)
- Genre : kategori dari genre aplikasi (Kedokteran, Gaya Hidup, dst)
- Terakhir Diperbarui : tanggal terakhir aplikasi diperbarui oleh pengembang aplikasi
- Versi Terkini : versi terkini dari aplikasi
- Versi Android : versi android minimum yang diperlukan untuk meng-install aplikasi

Untuk mendapatkan pemahaman yang lebih mendalam mengenai data, dilakukan Analisis Univariat dan Visualisasi Data.

Analisis Univariat adalah metode analisis data yang fokus pada representasi informasi dari satu variabel. Jenis analisis ini umumnya digunakan untuk menggambarkan distribusi suatu variabel dalam dataset. Sebagai alat bantu analisis, diterapkan teknik Visualisasi Data. Visualisasi data membuka wawasan yang mendalam terhadap perilaku berbagai fitur yang terdapat dalam dataset. Dalam pengembangan model proyek ini, teknik visualisasi yang digunakan adalah melalui barplot, yang digunakan untuk memvisualisasikan distribusi data.

Berikut adalah hasil dari Analisis Univariat dan Visualisasi Data (EDA) menggunakan teknik barplot.

![download (8)](https://github.com/whiteevl/Laporan-Sistem-Rekomendasi/blob/main/download.png)

Gambar 1a. Analisis Univariat (Data Kategori)

![download (9)](https://github.com/whiteevl/Laporan-Sistem-Rekomendasi/blob/main/download%20(1).png)

Gambar 1b. Analisis Univariat (Data Numerik)

Berdasarkan Gambar 1a, terlihat bahwa distribusi data pada 'Kategori' memiliki ketidakseimbangan, dengan tiga 'Kategori' terbanyak berturut-turut: FAMILY dengan 1972 sampel (persentase 18.2%), GAME dengan 1144 sampel (persentase 10.6%), dan TOOLS dengan 843 sampel (persentase 7.8%). Untuk mendapatkan pemahaman yang lebih mendalam, eksplorasi dapat dilanjutkan dengan memvisualisasikan fitur kategorikal lainnya. Sementara itu, pada fitur numerik, berdasarkan Gambar 1b, mayoritas nilai rating terletak pada skor 4. Meskipun demikian, visualisasi ini menunjukkan rentang skor yang luas, yaitu dari 0 hingga sekitar 20. Oleh karena itu, di bagian selanjutnya, perlu dilakukan tindakan lebih lanjut terhadap fitur 'Rating'. Langkah-langkah yang diambil untuk kondisi data seperti ini akan dijelaskan pada bagian berikutnya, yaitu Data Preparation.

  
## Data Preparation
Pada tahap Persiapan Data, dilakukan aktivitas seperti Pengumpulan Data, Penilaian Data, dan Pembersihan Data. Dalam proses Pengumpulan Data, data diimpor dengan konfigurasi yang memungkinkan pembacaan yang optimal menggunakan dataframe Pandas. Kegiatan ini telah dilakukan sejak awal.
Pada proses Penilaian Data, beberapa pemeriksaan berikut telah dilakukan:

- Pencilan (outlier), yaitu data yang jauh berbeda dari rata-rata data dalam kelompoknya.
- Data duplikat, yang merupakan data identik dengan data lainnya.
- Missing value, atau data yang tidak lengkap atau tidak tersedia.
 
Pada tahap Pembersihan Data, secara umum, terdapat tiga metode yang dapat diterapkan, yaitu sebagai berikut:

- Penghapusan (Dropping) (metode yang dilakukan dengan cara mengeliminasi sejumlah baris data)

- Imputasi (Imputation) (metode yang dilakukan dengan mengganti nilai yang "hilang" atau tidak tersedia dengan nilai tertentu, seperti median atau rata-rata dari data)

- Interpolasi (metode yang menghasilkan titik-titik data baru dalam suatu rentang data)

Dengan menggunakan visualisasi matriks, terlihat adanya data yang tidak lengkap, sebagaimana dapat dilihat pada Gambar 2.

![download (10)](https://github.com/whiteevl/Laporan-Sistem-Rekomendasi/blob/main/download%20(2).png)


Gambar 2. Visualiasi Matriks Data

Pada proyek ini, ditemui keberadaan outlier, data duplikat, dan missing value. Untuk mengatasi hal ini, dipilih metode drop() untuk membersihkan data dengan menghapus baris yang mengandung outlier, data duplikat, dan missing value. Setelah penerapan metode ini, dapat disimpulkan bahwa data kini telah bersih. Hal ini dapat diverifikasi dengan memeriksa menggunakan fungsi info(). Terlihat bahwa Non-Null Count memberikan nilai yang seragam untuk semua fitur dalam data, menunjukkan bahwa tidak ada lagi outlier, data duplikat, dan data yang hilang. Selanjutnya, dataset siap untuk diolah dalam pembuatan sistem rekomendasi.

## Modeling

Seperti yang dijelaskan pada awal, model yang dipilih adalah model Kesamaan Kosinus (Cosine Similarity) dan K-Nearest Neighbor karena mampu membantu dalam mengevaluasi tingkat kemiripan antar data.

1. Cosine similarity

Cosine similarity mengukur sejauh mana dua vektor mirip dan menentukan apakah keduanya memiliki arah yang serupa. Metode ini menghitung sudut cosinus antara dua vektor, di mana semakin kecil sudut cosinus, semakin tinggi nilai Kesamaan Kosinus. Rumus Kesamaan Kosinus dapat dirumuskan sebagai berikut:

$$ Cosine Similarity (A, B) = (A · B) / (||A|| * ||B||) $$ 

dimana: 
- (A·B)menyatakan produk titik dari vektor A dan B.
- ||A|| mewakili norma Euclidean (magnitudo) dari vektor A.
- ||B|| mewakili norma Euclidean (magnitudo) dari vektor B.

Untuk melakukan pengujian model, digunakan potongan kode berikut.

```
app_recommendations('EF Spelling Bee')
```

Tabel 1a, 1b, dan 1c berikut adalah hasil pengolahan model menggunakan Kesamaan Kosinus untuk mendapatkan 5 aplikasi yang serupa.

Tabel 1a. Hasil Pengujian Model Content Based Filtering (dengan Filter Genre)

|     |App|Genres|
|---|---|---|
|0|Timetable|Education|
|1|British Columbia License|Education|
|2|Starfall Free & Member|Education|
|3|AP Calculus BC Practice Test	|Education|
|4|Wifi BT Scanner|Education|

Tabel 1b. Hasil Pengujian Model Content Based Filtering (dengan Filter Type)

|     |App|Type|
|---|---|---|
|0|Timetable|Free|
|1|British Columbia License|Free|
|2|Starfall Free & Member|Free|
|3|AP Calculus BC Practice Test	|Free|
|4|Wifi BT Scanner|Free|

Tabel 1c. Hasil Pengujian Model Content Based Filtering (dengan Content Rating)

|     |App|Content Rating|
|---|---|---|
|0|Timetable|Everyone|
|1|British Columbia License|Everyone|
|2|Starfall Free & Member|Everyone|
|3|AP Calculus BC Practice Test	|Everyone|
|4|Wifi BT Scanner|Everyone|

Berdasarkan hasil uji model seperti terlihat pada Tabel 1a, 1b, dan 1c, dapat diperhatikan contoh konkret bagaimana model Kesamaan Kosinus memberikan rekomendasi aplikasi berdasarkan fitur-fitur yang dipilih pada model. Fitur yang menjadi fokus pada model yang telah dibuat adalah 'App' terhadap 'Genres', 'App' terhadap 'Type', dan 'App' terhadap 'Content Rating'. Melalui contoh pengujian, terlihat bagaimana model Kesamaan Kosinus memberikan rekomendasi aplikasi yang serupa dengan 'EF Spelling Bee', dengan fitur 'Genres', 'Type', dan 'Content Rating' yang mirip dengan aplikasi tersebut, yaitu dengan Genres: Education, Type: Free, dan Content Rating: Everyone. Hasil rekomendasi menampilkan 5 aplikasi dengan karakteristik Genres: Education, Type: Free, dan Content Rating: Everyone yang serupa dengan 'EF Spelling Bee'. Tentu saja, sistem rekomendasi ini membantu pengguna dalam mencari aplikasi dengan karakteristik serupa.

Secara keseluruhan, Cosine Similarity mengukur tingkat kesamaan antara dua vektor. Namun, terdapat kelebihan dan kekurangan pada model Kesamaan Kosinus. Salah satu keunggulan Kesamaan Kosinus adalah kompleksitasnya yang rendah. Sementara itu, salah satu kelemahan utamanya adalah bahwa magnitudo vektor tidak diperhitungkan, hanya arahnya yang menjadi fokus. Dengan kata lain, perbedaan besar atau kecilnya nilai tidak sepenuhnya mempengaruhi hasil perhitungan.

2. K-Nearest Neighbor

K-Nearest Neighbor (KNN) adalah salah satu algoritma paling sederhana dalam pengelompokan. Metode ini mudah dipahami karena pengelompokan dilakukan berdasarkan jarak terdekat dengan objek-objek lainnya (tetangga). Nilai K dalam KNN adalah variabel yang menentukan jumlah tetangga terdekat yang akan digunakan dalam proses klasifikasi. Sebagai contoh, jika K=1, hasil klasifikasi akan sangat dipengaruhi oleh satu tetangga terdekat atau satu rekaman karakteristik data terdekat. Dalam proyek ini, model KNN dibuat dengan menggunakan Metode Jarak Euclidean. Jarak Euclidean antara titik data P dan setiap titik data dalam kumpulan data D dihitung menggunakan rumus berikut:

$$ Euclidean Distance (P, Q) = sqrt(∑(Pi - Qi)^2) $$

Di mana:
- Pi mewakili fitur ke-i dari titik data P.
- Qi mewakili fitur ke-i dari titik data Q (titik data dari kumpulan data D).
- ∑ merupakan simbol penjumlahan pada semua fitur titik data.

Setelah perhitungan jarak selesai, algoritma KNN memilih K tetangga terdekat (titik data dengan jarak terkecil) untuk melakukan prediksi pada titik data baru P.

Tabel 2 berikut merupakan hasil pengujian model K-Nearest Neighbor dengan metrik Euclidean Distance

Tabel 2. Hasil Pengujian Model K-Nearest Neighbor

|     |App Name|Similiarity Score|
|---|---|---|
|0|Hush - Beauty for Everyone	|100.0%|
|1|Hairstyles step by step|99.99%|
|2|Tie - Always be happy|99.97%|
|3|Girls Hairstyles	|99.96%|
|4|Mirror - Zoom & Exposure -|99.95%|

Berdasarkan Tabel 2, terlihat contoh konkret bagaimana model K-Nearest Neighbor memberikan rekomendasi aplikasi berdasarkan fitur-fitur yang telah dipelajari, yakni 'App' terhadap 'Category', 'Rating', 'Reviews', 'Size', 'Installs', dan 'Price'. Hasil rekomendasi untuk aplikasi yang serupa dengan 'Natural recipes for your beauty' berdasarkan fitur-fitur tersebut mencakup 'Hush - Beauty for Everyone', 'Hairstyles step by step', 'Tie - Always be happy', 'Girls Hairstyles', dan 'Mirror - Zoom & Exposure', sebagaimana terlihat pada Tabel 2 dengan tingkat kemiripan berturut-turut sebesar 100.0%, 99.99%, 99.97%, 99.96%, dan 99.95%. Dengan demikian, model ini dapat sangat membantu pengguna menemukan aplikasi yang memiliki kesamaan dengan 'Natural recipes for your beauty'.

KNN memiliki beberapa keunggulan, termasuk pelatihan yang sangat cepat, kesederhanaan dan kemudahan pembelajaran, ketahanan terhadap derau dalam data pelatihan, serta efektivitas pada data pelatihan yang besar. Sementara itu, terdapat beberapa kelemahan pada KNN, yaitu: 1) nilai k dapat memengaruhi hasil model; 2) komputasi yang kompleks; 3) keterbatasan memori; dan 4) rentan terhadap atribut yang tidak relevan.

## Evaluation
Untuk menilai seberapa baik model, digunakan metrik evaluasi. Beberapa metrik evaluasi yang digunakan sebagai penilaian kinerja model antara lain Presisi, Skor Calinski-Harabasz, dan Skor Davies-Bouldin.

- Presisi adalah metrik yang digunakan untuk menilai kinerja model pengelompokan. Metrik ini menghitung rasio positif sejati terhadap total prediksi positif (termasuk positif sejati dan positif palsu).

- Skor Calinski-Harabasz adalah metrik yang digunakan untuk menilai kualitas algoritma pengelompokan. Metrik ini mengukur perbandingan dispersi antar-cluster dengan dispersi dalam-cluster. Skor yang lebih tinggi menunjukkan pengelompokan yang lebih baik.

- Skor Davies-Bouldin adalah metrik lain yang digunakan untuk menilai kualitas algoritma pengelompokan. Metrik ini menghitung kesamaan rata-rata antar setiap cluster dan cluster yang paling mirip, sambil memberikan penalti pada cluster yang terlalu dekat satu sama lain.

Berikut adalah formula dari setiap metrik yang digunakan:

$$ Precision = TP / (TP + FP) $$

$$ Calinski-Harabasz Score = (BSS / WSS) * (n - k) / (k - 1) $$

$$ Davies-Bouldin Score = (1 / k) * Σ(max((Ri + Rj) / d(Ci, Cj))) $$


- TP (True Positives) adalah jumlah kejadian positif yang diprediksi dengan benar.
- FP (False Positives) adalah jumlah kejadian positif yang diprediksi salah.
- BSS (Between Sum of Squares) adalah jumlah kuadrat jarak antara centroid cluster dan rata-rata keseluruhan.
- WSS (Within Sum of Squares) adalah jumlah jarak kuadrat antara titik data dan pusat cluster masing-masing.
- n adalah jumlah total titik data.
- k adalah jumlah cluster.
- Ri adalah jarak rata-rata antara setiap titik data di cluster i dan centroid cluster i.
- Rj adalah jarak rata-rata antara setiap titik data di cluster j dan pusat massa cluster j.
- d(Ci, Cj) adalah jarak antara sentroid cluster i dan j.

a. Presisi

Interpretasi hasil presisi berdasarkan Tabel 1a, 1b, dan 1c menunjukkan bahwa presisi yang dihitung menggunakan rumus presisi adalah 5/5 atau 100% untuk model rekomendasi Top-5. Hal ini mengindikasikan bahwa model mampu memberikan rekomendasi dengan tingkat presisi yang sangat tinggi, dalam hal ini mencapai 100%. Kesesuaian ini sesuai dengan hasil uji, di mana model mampu memberikan rekomendasi dengan fitur Genres, Type, dan Content Rating yang mirip dengan aplikasi 'EF Spelling Bee', yakni dengan Genres: Education, Type: Free, dan Content Rating: Everyone. Hasil rekomendasi menampilkan 5 aplikasi dengan Genres: Education, Type: Free, dan Content Rating: Everyone yang serupa dengan 'EF Spelling Bee'.


b. Calinski-Harabasz Score

Berikut adalah potongan kode untuk mengukur besar Calinski-Harabasz Score dari model yang telah dibuat 
```
calinski_harabasz_score(googleplaystore, app_name)
```
Berikut adalah skor setelah potongan kode tersebut ketika di run
```
7.4998974132315315
```

Interpretasi hasil Skor Calinski-Harabasz pada model ini adalah bahwa model memberikan skor yang relatif rendah dengan nilai 7.4998974132315315. Ini menandakan bahwa kluster pada model masih belum terpisahkan dengan baik, karena nilai skornya masih cukup rendah. Hal ini dapat mengakibatkan adanya rekomendasi pada beberapa aplikasi yang tidak sepenuhnya sesuai dengan preferensi pengguna. Pada pengujian model untuk aplikasi yang serupa dengan 'Natural recipes for your beauty', hasil rekomendasi mencakup 'Hush - Beauty for Everyone', 'Hairstyles step by step', 'Tie - Always be happy', 'Girls Hairstyles', dan 'Mirror - Zoom & Exposure'. Mengingat skor Calinski-Harabasz yang relatif rendah, dapat diartikan bahwa kluster 'App' masih belum terpisahkan secara optimal.

c. Davies-Bouldin Score

Berikut adalah potongan kode untuk mengukur besar Davies-Bouldin Score dari model yang telah dibuat 
```
davies_bouldin_score(googleplaystore, app_name)
```
Berikut adalah skor setelah potongan kode tersebut ketika di run
```
1.585735926526135
```
Interpretasi hasil Skor Davies-Bouldin pada model ini adalah bahwa model memberikan skor dengan nilai 1.585735926526135. Evaluasi Davies-Bouldin menunjukkan bahwa model ini memiliki skor yang relatif kecil, menandakan bahwa model sudah memiliki separasi kluster yang cukup baik. Pada pengujian model untuk aplikasi yang serupa dengan 'Natural recipes for your beauty', hasil rekomendasi mencakup 'Hush - Beauty for Everyone', 'Hairstyles step by step', 'Tie - Always be happy', 'Girls Hairstyles', dan 'Mirror - Zoom & Exposure'. Dengan mempertimbangkan skor Davies-Bouldin Score yang relatif rendah, dari kelima aplikasi serupa yang ditampilkan oleh model, dapat diartikan bahwa model telah berhasil memisahkan 'App' pada kluster yang sesuai, sehingga mampu memberikan rekomendasi aplikasi yang mirip dengan yang digunakan pengguna.


## Referensi:
[1] Akhlak, Nancy, Suchit, Anil. (2021). Play Store App Analysis. International Research Journal of Engineering and Technology. 8. 3888-3893.

[2] Burke, Robin & Felfernig, Alexander & Göker, Mehmet. (2011). Recommender Systems: An Overview. AI Magazine. 32. 13-18. 10.1609/aimag.v32i3.2361. 

[3] Pagare, Reena & Shinde, Anita. (2012). A Study of Recommender System Techniques. International Journal of Computer Applications. 47. 1-4. 10.5120/7269-0078. 

[4] Cremonesi, Paolo & Donatacci, A. & Garzotto, Franca & Turrin, R.. (2012). Decision-making in recommender systems: The role of user's goals and bounded resources. CEUR Workshop Proceedings. 893. 1-7.

[5] Mohamed, Marwa & Khafagy, Mohamed & Ibrahim, Mohamed. (2019). Recommender Systems Challenges and Solutions Survey. 10.1109/ITCE.2019.8646645. 
