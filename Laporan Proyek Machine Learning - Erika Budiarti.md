# Laporan Proyek Machine Learning 
-- **ERIKA BUDIARTI** --

## Project Overview

**Latar Belakang Proyek Rekomendasi Film**

Film merupakan salah satu bentuk hiburan yang populer di dunia. Setiap tahunnya, ribuan judul film dirilis di berbagai *platform*, baik di bioskop maupun layanan streaming. Hal ini tentu membuat masyarakat memiliki banyak pilihan film yang bisa ditonton.
Namun, banyaknya pilihan film juga bisa menjadi tantangan tersendiri. Masyarakat seringkali kesulitan untuk menemukan film yang sesuai dengan selera masing-masing. Oleh karena itu, diperlukan sistem rekomendasi film yang dapat membantu masyarakat menemukan film yang diinginkan.

Proyek rekomendasi film ini menawarkan solusi untuk permasalahan tersebut. Sistem rekomendasi film yang akan dibangun akan menggunakan metode pembelajaran mesin untuk mempelajari data film dan pengguna. Sistem ini mampu memberikan rekomendasi film yang sesuai dengan minat pengguna, meskipun jumlah data film yang ada sangatlah besar dan kompleks.

**Research Terkait**

Selama dekade terakhir, telah terjadi peningkatan data yang luar biasa karena media sosial, *e-commerce*, dan digitalisasi perusahaan secara keseluruhan. Data tersebut dimanfaatkan untuk membuat pilihan yang tepat, memprediksi *trend* pasar, dan pola dalam preferensi konsumen. Sistem rekomendasi telah menjadi hal yang umum setelah penetrasi layanan internet di kalangan masyarakat. Idenya adalah untuk menggunakan teknik pemfilteran dan pengelompokan untuk menyarankan item yang menarik bagi pengguna. Untuk komoditas media seperti film, diharapkan menemukan profil pengguna dengan selera yang sama. Awalnya, preferensi pengguna diperoleh dengan membiarkan pengguna menilai film pilihannya. Setelah digunakan, sistem rekomendasi akan dapat memahami pengguna dengan lebih baik dan menyarankan film yang dinilai lebih tinggi. Hasil eksperimen pada dataset *MovieLens* memberikan model yang andal yang akurat dan menghasilkan rekomendasi film yang lebih personal dibandingkan dengan model lain. [1]


## Business Understanding

### Problem Statements
1. Diperlukan suatu sistem yang dapat memprediksi peringkat atau preferensi pengguna terhadap film yang belum pernah ditonton. Dalam kata lain, bagaimana dapat mengembangkan model atau algoritma yang dapat merekomendasikan film kepada pengguna berdasarkan pemberian *rating* terhadap film-film sebelumnya, serta informasi tambahan seperti *genre*.
2. Diperlukan suatu sistem yang dapat memaksimalkan tingkat akurasi dalam membuat rekomendasi film kepada pengguna. Ini berarti bagaimana dapat mengembangkan algoritma atau model yang dapat memahami preferensi pengguna dengan baik dan memberikan rekomendasi yang sesuai dengan preferensi pengguna, sehingga meningkatkan pengalaman pengguna dalam menemukan film yang disukai. 

### Goals
1. Mengembangkan sistem rekomendasi film yang dapat memprediksi preferensi pengguna terhadap film yang belum pernah ditonton serta menyediakan rekomendasi yang personal dan relevan kepada pengguna dan meningkatkan tingkat kepuasan pengguna.
2. Meningkatkan akurasi dan kualitas rekomendasi film yang diberikan kepada pengguna. Dalam hal ini, meningkatkan pemahaman tentang preferensi pengguna dengan memanfaatkan teknik-teknik seperti pemfilteran kolaboratif (*collaborative filtering*) dan pemfilteran berdasarkan konten (*content based filtering*).

### Solution statements
Berikut adalah beberapa pendekatan yang dapat digunakan untuk membangun rekomendasi film:
    
1. *Content-Based Filtering (CBF)*:
Pendekatan ini akan memanfaatkan informasi tentang film, seperti *genre* dan deskripsi alur cerita, untuk memahami preferensi pengguna. Algoritma ini akan mencocokkan preferensi pengguna dengan atribut-atribut film dan memberikan rekomendasi film yang memiliki atribut yang sesuai dengan preferensi pengguna.
    
2. *Collaborative Filtering (CF)*:
Pendekatan ini yang memanfaatkan data historis peringkat pengguna untuk memprediksi preferensi mereka. CF dapat diimplementasikan dengan menggunakan dua varian, yaitu *User-Based CF* dan *Item-Based CF*. *User-Based CF* akan mencari pengguna serupa dan      merekomendasikan film yang disukai oleh pengguna serupa. *Item-Based CF* akan mencari film serupa dan merekomendasikan film yang mirip dengan yang sudah disukai oleh pengguna.
    

## Data Understanding
Klik *link* berikut untuk *download* dataset:
[MovieLens](https://www.kaggle.com/datasets/snehal1409/movielens).

*Dataset* tersebut mempunyai data 9125 film dan 100004 penilaian (*rating*) dari 671 pengguna yang dikumpulkan dari 9 Januari 1995 sampai dengan 16 Oktober 2016.

Variabel-variabel pada MovieLens dataset adalah sebagai berikut:
- movieId : kode unik pengenal film
- title : judul film
- year : tahun film dirilis
- genres : pengelompokan film berdasarkan konten/alur cerita
- userId : kode unik pengguna/penonton
- rating : penilaian pengguna atas film (range 0.5 sampai 5.0)


*Tabel 1* : **Dataset Movie Lens**
|movieID|                  genres                         |                         title  | year |  userId | rating |
|-------|-------------------------------------------------|--------------------------------|------|---------|--------|
|   1   |[Adventure, Animation, Children, Comedy, Fantasy]|                       Toy Story| 1995 |     7   |   3.0  |
|   1   |[Adventure, Animation, Children, Comedy, Fantasy]|                       Toy Story| 1995 |     9   |   4.0  |
|   1   |[Adventure, Animation, Children, Comedy, Fantasy]|                       Toy Story| 1995 |    13   |   5.0  |
|   1   |[Adventure, Animation, Children, Comedy, Fantasy]|                       Toy Story| 1995 |    15   |   2.0  |
|   1   |[Adventure, Animation, Children, Comedy, Fantasy]|                       Toy Story| 1995 |    19   |   3.0  |
| ..... |               ....................              |             ....               | .... |  .....  |   ...  |
| 99997 |                                          [Drama]| The Last Brickmaker in  America| 2001 |   287   |   5.0  |
| 99998 |                                          [Drama]|                 Stranger Things| 2016 |    73   |   4.5  |
| 99999 |                              [Romance, Thriller]|                          Rustom| 2016 |   611   |   5.0  |
|100000 |                      [Adventure, Drama, Romance]|                    Mohenjo Daro| 2016 |   611   |   3.0  |
|100001 |                                    [Documentary]| The Beatles: Eight Days a Week | 2016 |   547   |   5.0  |

           
### **Visualisasi Dataset**            
  *Grafik 1* : **Visualisasi pemberian rating film oleh pengguna**
  ![rating](https://raw.githubusercontent.com/ERIKABUDIARTI/Movie_Lens/main/rating.png)
    Pada grafik 1, bisa dilihat bahwa pengguna paling banyak memberikan *rating* 4.0 disusul *rating* 3.0 dan *rating* 5.0    
           
  *Grafik 2* : **Visualisasi sebaran genre film**
  ![genre](https://raw.githubusercontent.com/ERIKABUDIARTI/Movie_Lens/main/genre.png)  
    Grafik 2 memperlihatkan bahwa *genre* terbanyak dalam daftar film adalah *Drama* dan *Comedy*, sedangkan posisi terendah adalah *Film-Noir*.


## Data Preparation
**Tahapan dalam Persiapan Data**
1. **Impor library dan dataset**:   
    * Tahapan ini penting karena perlu memuat *library Python* dan *dataset* ke dalam *environment* (seperti *Jupyter Notebook* atau IDE lainnya) sebelum memulai analisis data.
    * Proses: impor *library Python* seperti *pandas*, *numpy*, dan lainnya yang dibutuhkan untuk mengolah data, kemudian impor *dataset* dari sumbernya (misalnya, *file CSV*, *file XLS*, atau *database*) ke *environment*.

2. **Pemeriksaan data**:   
    * Pemeriksaan data membantu untuk memahami dataset, mengidentifikasi masalah awal, dan memastikan kualitas data.
    * Proses: melihat struktur data, menampilkan beberapa sampel data, memeriksa tipe data kolom dan mengidentifikasi nilai yang hilang.

3. **Eksplorasi data**:
    * Eksplorasi data melibatkan analisis lebih mendalam terhadap dataset, termasuk visualisasi data, pemahaman distribusi data, identifikasi pola, dan analisis korelasi antar variabel.
    * Proses: Membuat visualisasi seperti *histogram*, *scatter plot*, atau *box plot* untuk memahami variabel-variabel yang ada maupun hubungan antar variabel

4. **Pembersihan data**:   
    * Data seringkali memiliki nilai yang hilang, data duplikat, *outlier*, atau kesalahan lain yang dapat mempengaruhi hasil analisis. Tahapan ini diperlukan untuk membersihkan data dari masalah-masalah tersebut.
    * Proses: Pembersihan data dapat melibatkan pengisian nilai yang hilang, menghapus baris atau kolom yang tidak relevan, menghapus data duplikat, menangani *outlier*, dan melakukan transformasi data jika diperlukan.

5. **Pembagian data**:   
    * Data perlu dibagi menjadi set pelatihan (*training set*) dan set pengujian (*testing set*) untuk melatih dan menguji model machine learning.
    * Proses: data dibagi secara acak menjadi dua bagian, misalnya 70% untuk pelatihan dan 30% untuk pengujian atau 80% untuk pelatihan dan 20% untuk pengujian. Pembagian data ini penting untuk menghindari *overfitting* (model yang terlalu cocok dengan data pelatihan) dan memastikan evaluasi yang obyektif.

## Modeling
*Gambar 1* : 
**Ilustrasi penggunaan model CONTENT-BASED FILTERING dan COLLABORATIVE FILTERING** 

![model](https://editor.analyticsvidhya.com/uploads/88506recommendation%20system.png)

1. **Content-Based Filtering (CBF)**:
CBF memanfaatkan informasi tentang atribut atau konten dari *item-item* yang akan direkomendasikan kepada pengguna. Misalnya, dalam sistem rekomendasi film, CBF akan menganalisis fitur-fitur film seperti *genre* atau alur cerita untuk membuat rekomendasi.

    *Kelebihan CBF*:
    * Personalisasi 
    CBF dapat memberikan rekomendasi yang lebih personal karena berdasarkan pada preferensi pengguna yang spesifik terhadap atribut-atribut *item*.
    * Pemahaman yang Baik 
    CBF memahami kenapa item direkomendasikan karena ia memperhitungkan atribut-atribut yang spesifik, sehingga hasil rekomendasi lebih dapat dijelaskan.
    * Tidak Bergantung pada Data Pengguna 
    CBF tidak memerlukan informasi riwayat pengguna atau data dari pengguna lain.
    
    *Kekurangan CBF*:
    * Terbatas dalam diversitas 
    CBF cenderung tidak mampu merekomendasikan *item* yang berbeda dari preferensi yang sudah ada. Pengguna mungkin cenderung mendapatkan rekomendasi yang sangat mirip dengan yang disukai sebelumnya.
    * Keterbatasan dalam atribut: 
    CBF hanya efektif jika atribut-atribut *item* dapat diukur atau diekstrak dengan baik. Jika atribut-atribut ini tidak mencakup preferensi pengguna, sistem tidak akan efektif.
    * *Cold Start Problem* 
    CBF mengalami kesulitan saat menghadapi *item* baru yang belum memiliki informasi atribut yang cukup.
    
    Proyek ini menggunakan algoritma KNN untuk membuat rekomendasi *Content-Based Filtering*, dengan parameter:
    * metric='cosine' 
    * algorithm='brute'
    * n_neighbors=30 
    * n_jobs=-1
  
    Algoritma KNN adalah algoritma berbasis pembandingan atau berbasis jarak yang digunakan dalam sistem rekomendasi. Algoritma ini bekerja dengan cara mengukur kesamaan antara item atau pengguna berdasarkan metrik jarak, seperti jarak Euclidean atau dalam kasus cosine similarity, yang umumnya digunakan untuk data teks atau vektor fitur. Prosesnya melibatkan langkah-langkah berikut:
Mengitung jarak (cosine similarity atau metrik jarak lainnya) antara *item* atau pengguna yang sedang dinilai dan semua *item* atau pengguna lain dalam basis data. Selanjutnya memilih *K item* atau pengguna terdekat.
Berdasarkan peringkat atau preferensi *item* yang paling mirip dengan *item* atau pengguna yang sedang dinilai, algoritma akan menghasilkan rekomendasi.

    *Kelebihan: 
    * Algoritma KNN tergolong sederhana
    * mudah diimplementasikan
    * tidak memerlukan proses pelatihan yang panjang
    
    *Kekurangan*: 
    * KNN bisa memiliki kinerja yang buruk untuk dataset yang sangat besar karena harus menghitung jarak ke semua *item* atau pengguna dalam basis data.
    * Pemilihan nilai K yang tepat dan pemilihan metrik jarak yang cocok bisa menjadi tantangan.  
    
    Adapun untuk rekomendasi film diberikan berdasarkan *user input*. Berikut adalah contoh rekomendasi yang diberikan apabila pengguna memasukkan *keyword* "Avengers"
    
    |        |                  title               |               genres                    |
    |--------|--------------------------------------| --------------------------------------- |
    |    1   |	                        Matrix, The	|   Adventure, Children, Comedy, Musical  |
    |    2   |	                          Spartacus |	Adventure, Children, Comedy, Musical  |
    |    3   |	       Land of Silence and Darkness |	Adventure, Children, Comedy, Musical  |
    |    4   |	                   Right Stuff, The	|   Adventure, Children, Comedy, Musical  |
    |    5	 |                  Requiem for a Dream	|   Adventure, Children, Comedy, Musical  |
    |    6	 |Austin Powers: The Spy Who Shagged Me	|   Adventure, Children, Comedy, Musical  |
    |    7	 |                                North |	Adventure, Children, Comedy, Musical  |
    |    8	 |                        Things Change |	Adventure, Children, Comedy, Musical  |
    |    9	 |                   Joy Luck Club, The |	Adventure, Children, Comedy, Musical  |
    |   10   |                       13 Going on 30	|   Adventure, Children, Comedy, Musical  |

2. **Collaborative Filtering (CF)**:
CF mengandalkan data kolaboratif dari pengguna, yaitu informasi riwayat interaksi pengguna dengan item. Dua jenis utama dari CF adalah *User-Based CF* dan *Item-Based CF*.

    *Kelebihan CF*:
    * Efektif untuk item baru 
    CF cenderung lebih efektif dalam menangani *item* baru karena ia mengandalkan perilaku pengguna, bukan atribut *item*.
    * Dapat menangani diversitas 
    CF dapat merekomendasikan item yang berbeda dari preferensi pengguna karena ia mengidentifikasi pola interaksi yang mungkin tidak terlihat dari atribut *item*.
    * Tidak Bergantung pada fitur atribut 
    Tidak bergantung pada atribut *item*, sehingga cocok untuk berbagai jenis produk atau layanan.
    
    *Kekurangan CF*:
    * Data yang diperlukan 
    CF memerlukan data pengguna yang cukup untuk menghasilkan rekomendasi yang baik. Dalam kasus yang jarang terjadi, ini bisa menjadi masalah.
    * *Sparsity* 
    Masalah sparsitas terjadi ketika banyak *item* dan pengguna, sehingga matriks kolaboratif menjadi sangat jarang dan sulit untuk memberikan rekomendasi yang akurat.
    * *Bubble Filter* 
    Ada kemungkinan bahwa CF hanya merekomendasikan *item* yang populer atau sering digunakan, yang dapat menyebabkan pengguna terjebak dalam "gelembung filter".
    
    Proyek ini menggunakan algoritma Neural Network untuk membuat model rekomendasi *Collaborative Filtering* dengan parameter: 
    * loss = Binary Crossentropy
    * optimizer = Adam
    * metric = Root Mean Squared Error
    
    Adapun untuk rekomendasi film diberikan adalah sebagai berikut: 
    
    |        |                  title               |                       genres                      |
    |--------|--------------------------------------| ------------------------------------------------- |
    |    1   |	                        District 9	|                       Mystery, Sci-Fi, Thriller   |
    |    2   |	                      Departed, The |	                        Crime, Drama, Thriller  |
    |    3   |	                     Cool Hand Luke |	                                       Drama    |
    |    4   |Grand Day Out with Wallace and Gromit	|   Adventure, Animation, Children, Comedy, Sci-Fi  |
    |    5	 |                         Interstellar |                                   Sci-Fi, IMAX    |
    |    6	 |                          Stand by Me	|                                 Adventure, Drama  |
    |    7	 |                          Dark Knight |	                    Action, Crime, Drama, IMAX  |
    |    8	 |                   Young Frankenstein |	                                Comedy, Fantasy |
    |    9	 |                  Killing Fields, The |	                                    Drama, War  |
    |   10   |                   X-Men: First Class |       Action, Adventure, Sci-Fi, Thriller, War    |


## Evaluation
Proyek ini menggunakan metrik evaluasi **ROOT MEAN SQUARED ERROR (RMSE)** dan metrik loss **BINARY CROSS ENTROPY**

1. **ROOT MEAN SQUARED ERROR**
    *Root Mean Square Error (RMSE)* adalah metrik evaluasi yang digunakan untuk mengukur rata-rata dari selisih antara prediksi model dan nilai sebenarnya, dihitung sebagai berikut:

        RMSE = √(Σ(yi - ŷi)² / n)
    *yi* adalah nilai sebenarnya dalam data
    *ŷi* adalah nilai yang diprediksi oleh model
    *Σ* adalah simbol untuk menjumlahkan (penjumlahan dari i = 1 hingga n)
    *n* adalah jumlah sampel data
    
    Cara RMSE bekerja adalah sebagai berikut:
    Model menghasilkan prediksi (ŷi) untuk setiap sampel dalam data. Selanjutnya menghitung selisih antara nilai sebenarnya (yi) dan prediksi model (ŷi) untuk setiap sampel. Setiap selisih di-kuadrat-kan (dipangkatkan dua). Hasil kuadrat selisih tersebut kemudian dijumlahkan untuk semua sampel data, kemudian dibagi oleh jumlah sampel data (n). Akar kuadrat dari hasil tersebut diambil untuk menghasilkan RMSE.
    
    Dengan kata lain, RMSE adalah akar kuadrat dari rata-rata dari kuadrat kesalahan antara prediksi model dan nilai sebenarnya. 
    
    Metrik ini memiliki beberapa karakteristik penting:
    * Semua selisih antara prediksi dan nilai sebenarnya dihitung dan diperlakukan sama, tetapi dikuadratkan untuk menghindari perhitungan negatif yang dapat membatalkan satu sama lain.
    * RMSE memberikan penalti lebih besar untuk kesalahan besar, sehingga kesalahan yang signifikan memiliki dampak yang lebih besar pada skor RMSE.
    * RMSE menghasilkan skor dalam unit yang sama dengan data sebenarnya, sehingga lebih mudah untuk menginterpretasinya.
    
    Umumnya, semakin rendah nilai RMSE, semakin baik kinerja model. Sebagai pembanding, model dengan RMSE lebih rendah dianggap lebih baik dalam memprediksi data dibandingkan dengan model dengan RMSE yang lebih tinggi.
    
    *Grafik 3* : **Validation RMSE vs Train RMSE**
    ![RMSE](https://raw.githubusercontent.com/ERIKABUDIARTI/Movie_Lens/main/Rmse.png)

2. **BINARY CROSS ENTROPY**
    *Binary Cross-Entropy* atau *Logistic Loss* adalah metrik *loss function* yang digunakan dalam tugas klasifikasi biner. Ini mengukur sejauh mana model memprediksi kelas yang benar dan seberapa yakin model tersebut dengan prediksi tersebut. 

    Binary Cross-Entropy bekerja dengan menggunakan logaritma natural (log) untuk menghitung kesalahan prediksi kelas biner. Berikut adalah formula dan cara kerja Binary Cross-Entropy:

        Binary Cross-Entropy Loss = -Σ(y * log(p) + (1 - y) * log(1 - p))
    *y* adalah label sebenarnya (0 atau 1).
    *p* adalah probabilitas yang diprediksi oleh model
    *Σ* adalah simbol untuk menjumlahkan (penjumlahan untuk semua sampel dalam dataset).

    Cara *Binary Cross-Entropy Loss* bekerja adalah sebagai berikut:
    Untuk setiap sampel, dibuat perbandingan antara probabilitas yang diprediksi (*p*) dengan label sebenarnya (*y*). Jika *y* adalah 1, hitung logaritma natural dari p. Jika *y* adalah 0, hitung logaritma natural dari (1 - p). Logaritma natural diterapkan agar kesalahan (*error*) kelihatan lebih besar untuk prediksi yang mempunyai perbedaan sifnifikan dari label sebenarnya. Setiap nilai logaritma yang dihitung dijumlahkan dan dibalikkan tanda negatif untuk menghasilkan nilai *Binary Cross-Entropy Loss*.

    *Binary Cross-Entropy* mengukur sejauh mana model mendekati label yang benar dan menilai tingkat ketidakpastian dalam prediksi. Semakin kecil nilai *Binary Cross-Entropy Loss*, semakin baik model yang dibuat. Loss yang rendah menunjukkan bahwa model menghasilkan probabilitas yang mendekati 1 untuk sampel kelas positif dan mendekati 0 untuk sampel kelas negatif.

    Tujuan utama mengoptimalkan *Binary Cross-Entropy Loss* adalah untuk mencapai nilai yang lebih rendah, yang mencerminkan kinerja yang lebih baik.

    *Grafik 4* : **Validation Loss vs Train Loss**
    ![Loss](https://raw.githubusercontent.com/ERIKABUDIARTI/Movie_Lens/main/Loss.png)


---

**Referensi**:  
[1] V. Subramaniyaswamy, "A personalised movie recommendation system based on collaborative filtering", International Journal of High Performance Computing and Networking, Vol.10 No.1-2, 2017.    
[A personalised movie recommendation system based on collaborative filtering](https://www.inderscienceonline.com/doi/abs/10.1504/IJHPCN.2017.083199) 



**---Ini adalah bagian akhir laporan---**
