# Laporan Proyek Machine Learning - Sistem Rekomendasi Aplikasi

## Project Overview

Google Play adalah toko online yang sangat populer untuk menemukan aplikasi, game, film, acara TV, buku, dan konten lainnya. Google Play menyediakan 2 juta aplikasi & game untuk miliaran orang di seluruh dunia. Google Play adalah toko online yang dikunjungi pengguna untuk menemukan aplikasi, game, film, acara TV, buku, dan konten lainnya.  Setiap harinya Google Play dibanjiri oleh banyak aplikasi baru yang dibuat oleh para pengembang aplikasi. Hal ini tentunya berdampak positif bagi pengguna karena dihadapkan lebih banyak pilihan aplikasi yang bisa di-install. Namun hal ini tentunya juga akan membuat pengguna bingung memilih aplikasi yang paling sesuai dengan kebutuhannya [[1](https://irjet.com/archives/V8/i4/IRJET-V8I4745.pdf)]. 

Sistem rekomendasi merupakan sistem yang memberikan rekomendasi pada suatu item yang dapat digunakan untuk membantu pengguna dalam mengambil keputusan. [[2](https://www.researchgate.net/publication/220604600_Recommender_Systems_An_Overview)] [[3](https://www.researchgate.net/publication/258651634_A_Study_of_Recommender_System_Techniques)] [[4](https://www.researchgate.net/publication/281705736_Decision-making_in_recommender_systems_The_role_of_user's_goals_and_bounded_resources)]. Dalam hal pengambilan keputusan guna memilih aplikasi yang paling sesuai untuk di-install pengguna Google Play, maka tentunya pengembangan sistem rekomendasi merupakan hal yang akan sangat membantu pengguna. Manfaat dan dampak nyata sistem rekomendasi bagi pengguna Google Play adalah mampu membantu pengguna mendapatkan aplikasi dengan kriteria (Genres, Type, dst) yang mirip dengan aplikasi yang sebelumnya pengguna telah unduh.

Dalam hal pengembangan model sistem rekomendasi, ada banyak faktor yang bisa menjadi bahan pertimbangan [[5](https://www.researchgate.net/publication/331063850_Recommender_Systems_Challenges_and_Solutions_Survey)], Pada sistem rekomendasi aplikasi faktor-faktor yang bisa menjadi bahan pertimbangan antara lain seperti Category,	Rating,	Reviews, Size, Installs,	Type,	Price,	Content, Rating,	Genres,	Last Updated,	Current Ver,	Android Ver, dan faktor-faktor lainnya. Pada proyek ini hanya beberapa faktor saja yang akan dipelajari untuk pembuatan Model Cosine Similarity dan K-Nearest Neighbor. Kedua algoritma ini akan mempelajari kesamaan antar data dalam fitur yang ada. Untuk faktor-faktor lainnya akan dipelajari pada pengembangan model lebih lanjut nantinya.

## Business Understanding

Pengembangan model Sistem Rekomendasi Aplikasi tentunya memiliki potensi dampak atau manfaat berupa menjadi salah satu alat bantu dalam pengambilan keputusan oleh pengguna Google Play.
Contoh potensi manfaat dari Sistem Rekomendasi Aplikasi ini adalah membantu pengguna Google Play membuat keputusan instalasi suatu aplikasi dengan lebih bijaksana.

### Problem Statements
- Berdasarkan eksplorasi *dataset*, bagaimana karakteristik dataset? Ada berapa banyak jumlah data? Fitur apa yang bisa dipilih untuk pengembangan model?
- Pada bagian Data Assesing, apakah terdapat terdapat data duplikat dan data missing? Jika ada tindakan apa yang paling tepat untuk diterapkan?
- Pada bagian Data Cleaning, apakah perlu dilakukan tindakan dropping ataupun imputation untuk memastikan data layak digunakan untuk pengembangan model?
- Bagaimana mengolah *dataset* agar dapat dibuat model sistem rekomendasi?
- Bagimana membuat model sistem rekomendasiCosine Similarity dan K-Nearest Neighbor?
- Bagaimanna cara mengukur nilai perfoma model sistem rekomendasi yang telah dibangun?

### Goals
- Mengeksplorasi informasi *dataset* dan melihat fitur yang paling memungkinkan dipilih untuk pengembangan model
- Melakukan proses Data Assesing untuk melihat kemungkinan adanya data duplikat dan data missing
- Melakukan proses Data Cleaning dan melakukan tindakan yang paling tepat untuk membersihkan data untuk kemudian siap digunakan untuk pengembangan model
- Melakukan proses Data Preparation seperti Vectorizing dan Data Spliting sebelum pembuatan model
- Membuat model sistem rekomendasi Cosine Similarity dan K-Nearest Neighbor berdasarkan fitur yang telah dipilih dari dataset
- Mengukur perfoma model sistem rekomendasi dengan menggunakan metrik evaluasi


### Solution Approach
- Untuk eksplorasi fitur dilakukan Analisis Univariat. Analisis Univariat dilakukan untuk mengeksplorasi distribusi suatu fitur yang dipilih dalam suatu dataset. Teknik yang digunakan adalah menggunakan visualiasi data menggunakan barplot dari fitur yang dipilih.
- Agar didapatkan model prediksi yang baik maka dilakukan proses *Data Wragling* yang meliputi *Data Gathering*, *Data Assessing*, dan *Data Cleaning*. Proses *Data Gathering* dilakukan dengan melakukan *load* data, untuk kemudian disimpan dalam *dataframe*. Proses *Data Assessing* dilakukan dengan mengecek Outlier (data yang menyimpang dari rata-rata sekumpulan data yang ada), Duplicate data (data yang serupa dengan data lainnya), dan missing value (data atau informasi yang "hilang" atau tidak tersedia). Sedangakanm Proses *Data Cleaning* adalah bentuk tindakan atas proses sebelumnya yaitu *Data Assessing*. Tindakan yang dapat dilakukan pada *Data Cleaning* untuk mengatasi data duplikat dan missing values adalah menghapus (dropping) baris data yang saat dicek terdapat  data duplikat dan missing values.
- Untuk mengetahui perfoma model dilakukan pengecekan performa dengan metrik evaluasi seperti Precission, Calinski Harabasz Score, dan Davies Bouldin Score

## Data Understanding
Data yang digunakan dalam pembuatan model merupakan data sekunder. Data diambil dari Kaggle dengan nama *dataset* yaitu *Google Play Store Apps*. 

URL: [https://www.kaggle.com/datasets/lava18/google-play-store-apps]

Berikut merupakan detail dari *dataset* yang digunakan untuk pembuatan model:
- Dataset berupa 3 buah file CSV yaitu googleplaystore.csv, googleplaystore_user_reviews.csv, dan license.txt
- Dataset yang digunakan dalam proyek ini yaitu googleplaystore.csv
- Dataset terdiri dari 10841 entri dengan 13 fitur.
- Dataset terdiri dari 12 data kategori dan 1 data numerik.
- Dataset memiliki *missing value* sejumlah 1474 pada Rating, 1 pada Type, 1 pada Content Rating, 8 pada Current Ver, dan 3 pada Android Ver.
  
### Variabel-variabel pada *dataset* adalah sebagai berikut:
- App                  : nama aplikasi
- Category             : kategori aplikasi
- Rating               : penilaian pengguna dari aplikasi (dalam satuan bintang 1-5)
- Reviews              : jumlah pengguna yang memberikan ulasan pada aplikasi tersebut (dalam satuan buah)
- Size                 : ukuran dari aplikasi (dalam satuan byte)
- Installs             : jumlah pengguna yang meng-install aplikasi
- Type                 : tipe aplikasi (dalam kategori Paid/berbayar atau Free/gratis)
- Price                : harga dari aplikasi (dalam satuan dollar USD)
- Content Rating       : kategori usia penggunaan untuk aplikasi (Everyone, Mature 17+, dst)
- Genres               : kategori dari genre aplikasi (Medical, Lifestyle, dst)
- Last Updated         : tanggal terakhir aplikasi di perbaharui oleh pengembang aplikasi
- Current Ver          : versi terkini dari aplikasi
- Android Ver          : versi android minimum yang dipersyaratkan untuk meng-install aplikasi

Untuk memahami data lebih lanjut, dilakukan Analisis Univariat serta Visualisasi Data

Analisis Univariat merupakan bentuk analisis data yang hanya merepresentasikan informasi yang terdapat pada satu variabel.  Jenis visualisasi ini umumnya digunakan untuk memberikan gambaran terkait distribusi sebuah variabel dalam suatu *dataset*. Sebagai alat bantu analisis, dilakukan teknik Visualisasi Data. Memvisualisasikan data memberikan wawasan mendalam tentang perilaku berbagai fitur-fitur yang tersedia dalam *dataset*. Teknik visualisasi yang digunakan pada pembuatan model proyek ini adalah dengan menggunakan barplot yang digunakan untuk memplot distribusi data.

Berikut adalah hasil Exploratory Data Analysis (EDA) menggunkan Analisis Univariat dengan teknik Visualisasi Data  menggunakan barplot.

![download (8)](https://github.com/ahmadsuaif/Proyek-Akhir-Sistem-Rekomendasi/assets/66425290/cd34f1c8-15c9-4000-bb3d-531c8285a975)

Gambar 1a. Analisis Univariat (Data Kategori)

![download (9)](https://github.com/ahmadsuaif/Proyek-Akhir-Sistem-Rekomendasi/assets/66425290/b19f0786-9a03-4a98-8768-46839a934907)

Gambar 1b. Analisis Univariat (Data Numerik)

Berdasarkan Gambar 1a, dapat dilihat bahwa distribusi data 'Category' memiliki perbandingan jumlah yang tidak sama, dengan tiga 'Catergory' yang paling banyak berturut-turut yaitu: FAMILY sebanyak 1972 sampel dengan persentase 18.2%, GAME sebanyak 1144 sampel dengan persentase 10.6%, dan TOOLS sebanyak 843 sampel dengan persentase 7.8%. Untuk eksplorasi lebih lanjut, bisa divisualisasikan fitur kategorik lainnya. Sedangkan untuk fitur numerik, berdasarkan Gambar 1b, dapat dilihat mayoritas rating berada pada score 4, namun tampak bahwa visualisasi ini menampilkan rentang skor yang luas yaitu 0 sampai dengan sekitar 20. Oleh karena itu, pada bagian selanjutnya perlu dilakukan tindakan lebih terhadap fitur 'Rating'. Tindakan yang diambil untuk kondisi data seperti ini dijelaskan pada bagian berikutnya, Data Preparation.
  
## Data Preparation
Pada proses *Data Preparation* dilakukan kegiatan seperti *Data Gathering*, *Data Assessing*, dan *Data Cleaning*.
Pada proses *Data Gathering*, data diimpor sedemikian rupa agar bisa dibaca dengan baik menggunakan *dataframe* Pandas. Kegiatan ini sudah dilakukan di awal.
Untuk proses *Data Assessing*, berikut adalah beberapa pengecekan yang dilakukan:
- Outlier (data yang menyimpang dari rata-rata sekumpulan data yang ada)
- Duplicate data (data yang serupa dengan data lainnya)
- Missing value (data atau informasi yang "hilang" atau tidak tersedia)
 
Pada proses *Data Cleaning*, secara garis besar, terdapat tiga metode yang dapat digunakan antara lain seperti berikut:
- Dropping (metode yang dilakukan dengan cara menghapus sejumlah baris data)
- Imputation (metode yang dilakukan dengan cara mengganti nilai yang "hilang" atau tidak tersedia dengan nilai tertentu yang bisa berupa median atau mean dari data)
- Interpolation (metode menghasilkan titik-titik data baru dalam suatu jangkauan dari suatu data)

Dengan bantuan visualiasi matriks, tampak terlihat adanya data yang tidak lengkap seperti terlihat pada Gambar 2.

![download (10)](https://github.com/ahmadsuaif/Proyek-Akhir-Sistem-Rekomendasi/assets/66425290/e82a237b-e708-4663-8717-2ef130609b4c)


Gambar 2. Visualiasi Matriks Data

Pada kasus proyek ini ditemukan *outlier*, data duplikat, dan *missing value*. Adapaun metode yang dipilih untuk digunakan dalam rangka mengatasi hal *outlier*, data duplikat, dan *missing value* adalah dengan menerapkan metode *dropping* menggunakan drop(). Metode drop() ini digunakan untuk menghapus baris *outlier*, data duplikat, dan *missing value* dari data. Setelah dilakukan metode ini, data sekarang sudah bersih. Hal ini dapat dilihat ketika dicek menggunakan info(). Tampak Non-Null Count memberikan nilai yang sama untuk semua fitur pada data. Tidak ada lagi outlier, data duplikat, dan data missing. Selanjutnya dataset dapat diolah untuk dapat diproses dalam membuat sistem rekomendasi.

## Modeling

Seperti yang dijelaskan di awal, model yang dipilih adalah model Cosine Similarity dan K-Nearest Neighbor karena mampu membantu melihat kemiripan antar data. 

1. Cosine similarity

Cosine similarity mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama. Ia menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai cosine similarity. Cosine Similarity dituliskan dalam rumusan berikut

$$ Cosine Similarity (A, B) = (A · B) / (||A|| * ||B||) $$ 

dimana: 
- (A·B)menyatakan produk titik dari vektor A dan B.
- ||A|| mewakili norma Euclidean (magnitudo) dari vektor A.
- ||B|| mewakili norma Euclidean (magnitudo) dari vektor B.

Untuk melakukan pengujian model, digunakan potongan kode berikut.

```
app_recommendations('EF Spelling Bee')
```

Tabel 1a, 1b, dan 1c berikut adalah hasil pelatihan model menggunakan Cosine Similarity untuk mendapatkan 5 buah App yang mirip

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

Berdasarkan pengujian model seperti tampak pada Tabel 1a, 1b, dan 1c, dapat dilihat contoh konkret bagaimana model Cosine Similarity memberikan rekomendasi aplikasi berdasarkan fitur-fitur dipilih pada model. Adapun fitur yang dipilih pada model yang dibuat adalah 'App' terhadap 'Genres', 'App' terhadap 'Type', dan 'App' terhadap 'Content Rating'. Dari contoh pengujian dapat dilihat contoh konkret bagaimana model Cosine Similarity memberikan rekomendasi aplikasi yang sejenis dengan 'EF Spelling Bee' dengan fitur 'Genres', 'Type', dan 'Content Rating' yang mirip dengan aplikasi 'EF Spelling Bee' yaitu dengan Genres: Education, Type: Free dan Content Rating: Everyone. Hasil rekomendasi menampilkan 5 buah aplikasi dengan Genres: Education, Type: Free dan Content Rating: Everyone yang serupa dengan 'EF Spelling Bee'. Tentunya sistem rekomendasi ini sangat membantu pengguna mencari aplikasi yang sejenis.

Secara umum, Cosine Similarity mengukuran kesamaan antara dua vektor. Namun begitu terdapat kelebihan dan kekurangan dari model Cosine Similarity. Salah satu keuntungan Cosine Similarity adalah kompleksitasnya yang rendah. Sedangkan, salah satu kelemahan utama Cosine Similarity adalah besarnya vektor tidak diperhitungkan, hanya arahnya saja. Dalam hal ini, berarti perbedaan nilai tidak sepenuhnya diperhitungkan.

2. K-Nearest Neighbor

K-Nearest Neighbor (KNN) merupakan algoritma yang paling sederhana dalam mengkelompokkan. Metode ini mudah dipahami dibandingkan metode lain karena mengkelompokkan berdasarkan jarak terdekat dengan objek lainnya (tetangga). K dalam KNN merupakan variabel jumlah tetangga terdekat yang akan diambil untuk proses klasifikasi. Jumlah K=1 akan membuat hasil klasifikasi terasa kalu karena hanya memperhitungkan satu tetangga terdekat atau satu record karakteristik data terdekat. Pada proyek ini dibuat model KNN dengan menggunakan Euclidean Distance. Diberikan titik data P dan kumpulan data D yang berisi beberapa titik data, jarak Euclidean antara P dan setiap titik data di D dihitung menggunakan rumus berikut:

$$ Euclidean Distance (P, Q) = sqrt(∑(Pi - Qi)^2) $$

Di mana:
- Pi mewakili fitur ke-i dari titik data P.
- Qi mewakili fitur ke-i dari titik data Q (titik data dari kumpulan data D).
- ∑ merupakan simbol penjumlahan pada semua fitur titik data.

Setelah jarak dihitung, algoritma KNN memilih tetangga terdekat K (titik data dengan jarak terkecil) untuk membuat prediksi untuk titik data baru P.

Tabel 2 berikut merupakan hasil pengujian model K-Nearest Neighbor dengan metrik Euclidean Distance

Tabel 2. Hasil Pengujian Model K-Nearest Neighbor

|     |App Name|Similiarity Score|
|---|---|---|
|0|Hush - Beauty for Everyone	|100.0%|
|1|Hairstyles step by step|99.99%|
|2|Tie - Always be happy|99.97%|
|3|Girls Hairstyles	|99.96%|
|4|Mirror - Zoom & Exposure -|99.95%|

Berdasarkan Tabel 2, tampak contoh konkret bagaimana model K-Nearest Neighbor memberikan rekomendasi aplikasi berdasarkan fitur-fitur yang dipelajari dalam model, yaitu 'App' terhadap 'Category',	'Rating',	'Reviews',	'Size',	'Installs', dan	'Price'. Hasil rekomendasi untuk aplikasi yang mirip dengan 'Natural recipes for your beauty' berdasarkan berdasarkan fitur-fitur yang dipelajari memberikan hasil rekomendasi aplikasi serupa yaitu 'Hush - Beauty for Everyone', 'Hairstyles step by step', 'Tie - Always be happy', 'Girls Hairstyles', dan 'Mirror - Zoom & Exposure' seperti tampak pada Tabel 2 dengan tingkat kemiripan dalam persentase berturut-turut senilai 100.0%, 99.99%, 99.97%, 99.96%, dan 99.95%. Tentunya model ini akan sangat membantu pengguna menemukan aplikasi yang mirip dengan Natural recipes for your beauty.

KNN memiliki beberapa kelebihan, diantaranya adalah pelatihan sangat cepat, sederhana dan mudah dipelajari, tahan terhadap data pelatihan yang memiliki derau, dan efektif jika data pelatihan besar. Sedangkan, kekurangan dari KNN adalah: 1) nilai k menjadi bias dalam model; 2) komputasi yang kompleks; 3) keterbatasan memori; dan 4) mudah tertipu dengan atribut yang tidak relevan.

## Evaluation
Untuk mengukur seberapa baik model, digunakan metrik evaluasi. Adapun metrik yang sebagai alat ukur perfoma model yang dibuat antara lain **Precission, Calinski Harabasz Score**, dan **Davies Bouldin Score**. 

- Presisi adalah metrik yang digunakan untuk mengevaluasi kinerja model pengelompokan. Metrik ini menghitung rasio prediksi positif sejati terhadap jumlah total prediksi positif (positif sejati dan positif palsu).
- Calinski-Harabasz adalah metrik yang digunakan untuk mengevaluasi kualitas algoritma pengelompokan. Metrik ini mengukur rasio dispersi antar-cluster dengan dispersi dalam-cluster. Nilai yang lebih tinggi dari skor ini menunjukkan cluster yang terdefinisi dengan lebih baik.
- Davies-Bouldin adalah metrik lain yang digunakan untuk mengevaluasi kualitas algoritma pengelompokan. Metrik ini menghitung kesamaan rata-rata antara setiap cluster dan cluster yang paling mirip sambil mempenalti cluster yang terlalu dekat satu sama lain.

Berikut merupakan rumus dari masing-masing metrik yang digunakan:

$$ Precision = TP / (TP + FP) $$

$$ Calinski-Harabasz Score = (BSS / WSS) * (n - k) / (k - 1) $$

$$ Davies-Bouldin Score = (1 / k) * Σ(max((Ri + Rj) / d(Ci, Cj))) $$

dimana
- TP (True Positives) adalah jumlah kejadian positif yang diprediksi dengan benar.
- FP (False Positif) adalah jumlah kejadian positif yang diprediksi salah.
- BSS (Between Sum of Squares) adalah jumlah kuadrat jarak antara centroid cluster dan rata-rata keseluruhan.
- WSS (Dalam Jumlah Kuadrat) adalah jumlah jarak kuadrat antara titik data dan pusat cluster masing-masing.
- n adalah jumlah total titik data.
- k adalah jumlah cluster.
- Ri adalah jarak rata-rata antara setiap titik data di cluster i dan centroid cluster i.
- Rj adalah jarak rata-rata antara setiap titik data di cluster j dan pusat massa cluster j.
- d(Ci, Cj) adalah jarak antara sentroid cluster i dan j.

a. Presisi

Adapun interpretasi hasil presisi berdasarkan Tabel Tabel 1a, 1b, dan 1c dapat dilihat bahwasanya besar presisi jika dihitung dengan menggunakan rumusan presisi adalah 5/5 atau 100% untuk model rekomendasi Top-5. Hal ini menunjukkan bahwa model mampu memberikan rekomendasi dengan tingkat presisi yang sangat baik (dalam hal ini 100%). Hal ini sesuai dengan hasil uji dimana model mampu memberikan rekomendasi dengan Genres, Type, dan Content Rating yang yang mirip dengan aplikasi 'EF Spelling Bee' yaitu dengan Genres: Education, Type: Free dan Content Rating: Everyone. Hasil rekomendasi menampilkan 5 buah aplikasi dengan Genres: Education, Type: Free dan Content Rating: Everyone yang serupa dengan 'EF Spelling Bee'.

b. Calinski-Harabasz Score

Berikut adalah potongan kode untuk mengukur besar Calinski-Harabasz Score dari model yang telah dibuat 
```
calinski_harabasz_score(googleplaystore, app_name)
```
Berikut adalah skor setelah potongan kode tersebut dijalankan 
```
7.4998974132315315
```

Adapun interpretasi hasil Calinski-Harabasz Score pada model ini adalah bahwa model memberikan skor yang relatif rendah dengan nilai 7.4998974132315315. Hal ini menunjukkan bahwa kluster pada model masih belum terpisahkan dengan baik karena nilai skornya masih cukup rendah. Hal ini memungkinkan adanya rekomendasi pada beberapa aplikasi yang tidak sesuai dengan aplikasi yang disukai pengguna. Pada pengujian model  untuk aplikasi yang mirip dengan 'Natural recipes for your beauty' memberikan hasil rekomendasi aplikasi serupa yaitu 'Hush - Beauty for Everyone', 'Hairstyles step by step', 'Tie - Always be happy', 'Girls Hairstyles', dan 'Mirror - Zoom & Exposure'. Mengingat skor Calinski-Harabasz yang relatif cukup rendah, maka artinya kluster 'App' masih belum terpisahkan dengan sempurna.

c. Davies-Bouldin Score

Berikut adalah potongan kode untuk mengukur besar Davies-Bouldin Score dari model yang telah dibuat 
```
davies_bouldin_score(googleplaystore, app_name)
```
Berikut adalah skor setelah potongan kode tersebut dijalankan 
```
1.585735926526135
```
Adapun interpretasi hasil Davies-Bouldin Score pada model ini adalah bahwa model memberikan skor dengan nilai 1.585735926526135. Hasil evaluasi Davies-Bouldin menunjukkan bahwa model ini memiliki skor yang relatif cukup kecil. Hal ini menandakan bahwa model sudah memiliki separasi kluster yang cukup baik. Pada pengujian model  untuk aplikasi yang mirip dengan 'Natural recipes for your beauty' memberikan hasil rekomendasi aplikasi serupa yaitu 'Hush - Beauty for Everyone', 'Hairstyles step by step', 'Tie - Always be happy', 'Girls Hairstyles', dan 'Mirror - Zoom & Exposure'. Mengingat skor Davies-Bouldin Score yang relatif cukup rendah, dari 5 aplikasi serupa yng ditampilkan oleh model artinya model telah cukup berhasil memisahkan 'App' pada kluster yang sesuai sehingga mampu memberikan rekomendasi aplikasi yang mirip dengan yang digunakan pengguna.


## Referensi:
[1] Akhlak, Nancy, Suchit, Anil. (2021). Play Store App Analysis. International Research Journal of Engineering and Technology. 8. 3888-3893.

[2] Burke, Robin & Felfernig, Alexander & Göker, Mehmet. (2011). Recommender Systems: An Overview. AI Magazine. 32. 13-18. 10.1609/aimag.v32i3.2361. 

[3] Pagare, Reena & Shinde, Anita. (2012). A Study of Recommender System Techniques. International Journal of Computer Applications. 47. 1-4. 10.5120/7269-0078. 

[4] Cremonesi, Paolo & Donatacci, A. & Garzotto, Franca & Turrin, R.. (2012). Decision-making in recommender systems: The role of user's goals and bounded resources. CEUR Workshop Proceedings. 893. 1-7.

[5] Mohamed, Marwa & Khafagy, Mohamed & Ibrahim, Mohamed. (2019). Recommender Systems Challenges and Solutions Survey. 10.1109/ITCE.2019.8646645. 
