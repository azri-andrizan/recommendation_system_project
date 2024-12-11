# **Laporan Proyek _Machine Learning_ - Azri Andrizan**

---

# **_Courses System Recommendation_**

# **Domain Proyek**

Industri pendidikan daring telah mengalami pertumbuhan yang pesat dalam dekade terakhir, khususnya setelah pandemi COVID-19 yang memaksa banyak institusi pendidikan dan perusahaan beralih ke platform digital untuk pelatihan dan pembelajaran. Menurut laporan oleh *Research and Markets* [[1]], pasar global untuk pendidikan daring diperkirakan mencapai USD 350 miliar pada tahun 2025. Hal ini menciptakan peluang besar sekaligus tantangan dalam menyajikan pengalaman belajar yang personal dan relevan bagi pengguna.

Salah satu tantangan utama dalam sektor ini adalah membantu pengguna menemukan kursus yang sesuai dengan kebutuhan, preferensi, atau tujuan karier mereka di tengah ribuan pilihan yang tersedia di berbagai platform pembelajaran seperti *Coursera*, *edX*, dan *Udemy*. Berdasarkan survei oleh *EdTech Magazine* [[2]], pengguna sering kali merasa kewalahan dengan banyaknya pilihan yang ditawarkan, sehingga membutuhkan waktu lebih lama untuk memilih kursus yang benar-benar relevan bagi mereka. Fenomena ini disebut sebagai "*choice overload*" dan dapat mengurangi efisiensi dan kepuasan pengguna dalam memilih kursus.

Sistem rekomendasi telah menjadi solusi yang populer untuk mengatasi masalah ini. Dalam penelitian oleh Ricci et al. [[3]], sistem rekomendasi berbasis _content-based filtering_ (CBF) dan _collaborative filtering_ (CF) terbukti efektif dalam membantu pengguna menemukan konten yang relevan berdasarkan preferensi mereka sebelumnya. Di sisi lain, _popularity-based filtering_ (PBF) memungkinkan pengguna mendapatkan rekomendasi kursus yang paling diminati oleh komunitas, meningkatkan kepercayaan terhadap pilihan tersebut.

Namun, setiap pendekatan memiliki keterbatasan. Sebagai contoh, CBF mungkin gagal merekomendasikan kursus baru yang belum memiliki cukup metadata relevan, sedangkan PBF cenderung hanya menonjolkan kursus populer tanpa mempertimbangkan kebutuhan spesifik pengguna. Untuk mengatasi keterbatasan ini, pendekatan hybrid yang menggabungkan kedua metode telah menunjukkan hasil yang menjanjikan. Dalam penelitian oleh Burke [[4]], pendekatan hybrid memberikan rekomendasi yang lebih akurat dan memuaskan dibandingkan pendekatan tunggal.

Studi ini bertujuan untuk membangun sistem rekomendasi hybrid yang memanfaatkan teknik CBF dan PBF, yang dirancang untuk membantu pengguna menemukan kursus yang relevan dengan preferensi mereka sekaligus menawarkan pilihan yang populer di komunitas. Selain itu, evaluasi kinerja sistem menggunakan metrik seperti precision, recall, coverage, dan nDCG dilakukan untuk memastikan kualitas rekomendasi.

# **_Business Understanding_**
## **_Problem Statement_**
Berangkat dari permasalahan yang telah dipaparkan pada bagian Domain Proyek, proyek ini berfokus pada pengembangan sistem rekomendasi _hybrid_ untuk meningkatkan pengalaman pengguna dalam memilih kursus online yang relevan dan bernilai. Adapun masalah spesifik yang akan dijawab adalah: 
1.  Bagaimana memanfaatkan metadata kursus dan data popularitas untuk memberikan rekomendasi kursus yang personal dan relevan bagi pengguna?
2.  Bagaimana mengintegrasikan elemen popularitas kursus untuk meningkatkan kepercayaan pengguna terhadap rekomendasi yang diberikan?
3.  Bagaimana menggabungkan pendekatan _content-based filtering_ dan _popularity-based filtering_ untuk memberikan rekomendasi yang optimal?
4. Bagaimana mengevaluasi kinerja sistem rekomendasi dengan metrik yang relevan untuk memastikan kualitas rekomendasi?

## **_Goals_**
Berdasarkan problem statement yang telah dirumuskan, berikut adalah tujuan (_goals_) yang relevan untuk proyek sistem rekomendasi ini:
1.  **Mengembangkan sistem rekomendasi _hybrid_ yang efektif dan efisien** Membuat sistem rekomendasi yang menggabungkan _content-based filtering_ (CBF) dan _popularity-based filtering_ (PBF) untuk menghasilkan rekomendasi kursus yang relevan dan berkualitas.
2.  **Meningkatkan personalisasi rekomendasi kursus** dengan memanfaatkan metadata kursus (seperti *keyword*, _modules_, dan _instructor_) untuk memberikan rekomendasi yang disesuaikan dengan preferensi.
3.  **Memanfaatkan popularitas kursus sebagai indikator kualitas** dengan mengintegrasikan elemen popularitas (rating dan jumlah ulasan) ke dalam rekomendasi untuk meningkatkan kredibilitas dan daya tarik rekomendasi bagi pengguna.
4. **Mengukur kualitas rekomendasi menggunakan metrik** seperti _precision_, _recall_, _coverage_, dan nDCG untuk memastikan sistem mampu memberikan rekomendasi yang relevan dan bermanfaat.

## **_Solution Statement_**
Untuk menjawab tantangan dalam memberikan rekomendasi kursus yang relevan dan berkualitas, proyek ini akan mengembangkan sistem rekomendasi hybrid yang memadukan dua pendekatan utama:
1.  **Hybrid Recommendation System**
    *   **_Content-Based Filtering (CBF)_**
    Pendekatan ini akan memanfaatkan metadata kursus seperti deskripsi, kata kunci, modul, dan informasi instruktur untuk menemukan kesamaan antara kursus tertentu dengan kursus lainnya. Dengan menggunakan metode _cosine similarity_, sistem akan memberikan rekomendasi berdasarkan konten yang paling mirip dengan preferensi pengguna atau kursus yang mereka minati.

    *   **_Popularity-Based Filtering (PBF)_**
    Untuk melengkapi pendekatan berbasis konten, sistem akan menghitung skor popularitas menggunakan data numerikal seperti rating dan jumlah ulasan. Kursus dengan skor popularitas tertinggi akan disarankan sebagai kursus yang paling diminati dan berkualitas tinggi.

    Kedua pendekatan ini akan digabungkan dengan metode berbobot untuk menghasilkan sistem rekomendasi yang lebih kuat. Skor dari CBF dan PBF akan dikombinasikan untuk mempertimbangkan kesesuaian konten serta popularitas kursus secara bersamaan.

2.  **Evaluasi Sistem**

    Untuk memastikan kinerja sistem, evaluasi akan dilakukan menggunakan metrik seperti _precision_, _recall_, _coverage_, dan nDCG. Metrik ini akan membantu mengukur relevansi, cakupan, dan kualitas rekomendasi yang dihasilkan.

# **_Data Understanding_**
Pada proyek ini, dataset yang digunakan adalah **Coursera Dataset** yang disediakan oleh **Kaggle**, dataset dapat diakses dan diunduh pada tautan [Coursera Dataset](https://www.kaggle.com/datasets/elvinrustam/coursera-dataset). Dataset ini menyajikan informasi rinci mengenai berbagai kursus yang tersedia di Coursera, termasuk informasi seperti nama kursus, rating, jumlah ulasan, deskripsi, tingkat kesulitan, serta kategori kursus. Dataset ini dirancang untuk memberikan wawasan mendalam terkait kursus yang ditawarkan oleh platform e-learning terbesar tersebut, sehingga sangat relevan untuk pengembangan sistem rekomendasi. Dataset disediakan dalam format csv (_comma seperated value_), berisi jumlah sampel dengan 8370 baris data yang mencakup berbagai

Terdapat 13 fitur dalam dataset ini, yang meliputi :
| Fitur         | Deskripsi                                          |Tipe Data|
|:--------------|:--------------------------------------------------|:---------|
|Course Title| Berisi judul atau nama kursus di platform Coursera. |object|
|Rating    |Skor rata-rata yang diberikan oleh pengguna              |float64|
|Level           |Menunjukkan tingkat kesulitan kursus, seperti Beginner, Intermediate, Advanced.  |object|
|Schedule|Informasi mengenai jadwal kursus|object|
|What you will learn|Deskripsi ringkas tentang kemampuan atau pengetahuan yang akan diperoleh peserta setelah menyelesaikan kursus.|object|
|Skill gain| Daftar keterampilan spesifik yang akan dikuasai peserta setelah mengikuti kursus.|object|
|Modules| Merinci jumlah modul atau bagian dalam kursus.|object|
|Instructor| Nama instruktur atau tim pengajar yang menawarkan kursus.|object|
|Offered By| Institusi atau organisasi yang menawarkan kursus, seperti universitas atau perusahaan tertentu.| object|
|Keyword| Kumpulan kata kunci yang berkaitan dengan konten kursus| object|
|Course Url| Tautan ke halaman kursus di platform Coursera| object|
|Duration to complete (Approx.)| Estimasi durasi waktu (dalam jam atau minggu) yang diperlukan untuk menyelesaikan kursus.| float64|
|Number of Review| Jumlah ulasan yang diterima kursus dari pengguna| int64|

Kolom yang akan menjadi fitur untuk masing-masing model sistem rekomendasi ditentukan sebagai berikut.

Content-Based Filtering:
*   *Level*
*   *Modules*
*   *Instructor*
*   *Keyword*

Popularity-Based Filtering:
*   *Rating*
*   *Number of Review*

## **__Exploratory Data Analysis__**

*   **_Missing Value Identification_**

    ![Gambar 1. Distribusi missing value ](https://raw.githubusercontent.com/azri-andrizan/Assets/main/asset2/missing_value.png)
    
    Gambar 1. Distribusi _missing value_ pada kolom *Modules* dan *Instructor*

    Pada variabel *Modules* dan *Instructor* terdapat 33 baris data *missing value* pada kolom **_Modules_** dan 88 baris data *missing value* pada kolom **_Instructor_**. Setelah dilakukan analisa lebih lanjut, pada *missing value* dikolom **_Modules_** terdapat pola yang menarik dimana seluruh data yang hilang ini mempunyai nama **_Instructor_** yang sama yaitu **_Google Cloud Training_**. Sehingga dilakukan pendekatan lanjut dengan menganalisis apakah ada pola tertentu berdasarkan *value*nya pada variabel lain. Hasilnya berdasarkan variabel **_Duration to Complete (Approx.)_** waktu yang digunakan untuk menyelesaikan kursus dengan *Missing value* ini terbilang singkat yaitu berkisar rata-rata diantara 1 - 1.5 unit waktu. Hal ini mengindikasikan bahwa kursus yang yang berdurasi pendek mungkin tidak memiliki cukup modul untuk ditampilkan atau kursus ini hanya mencakup pengantar/materi dasar tanpa membagi isi kedalam modul. Lalu dilakukan analisis lanjut, berdasarkan variabel **_Rating_** hampir seluruh **_Modules_** yang bernilai *Missing value* memiliki *Rating* 0. Akhirnya, berdasarkan analisis yang telah dilakukan, dapat disimpulkan bahwa *missing value* pada kolom **_Modules_** hanya terdapat pada kursus yang disediakan oleh *Google Cloud*. Pola ini dianalisis lebih lanjut dan ditemukan bahwa hampir seluruh kursus yang tidak memiliki modul ini memiliki durasi yang sangat pendek, yaitu sekitar satu unit waktu. Selain itu, sebagian besar kursus *Google Cloud* yang tidak memiliki modul memiliki rating 0, yang mengindikasikan bahwa tidak ada ulasan atau umpan balik dari peserta. Sebagai perbandingan, kursus *Google Cloud* yang memiliki modul menunjukkan rating rata-rata yang lebih tinggi dengan hanya sedikit rating yang rendah.
    
    *Missing value* pada kolom **_Instructor_** sepertinya tersebar merata, tidak seperti *missing value* pada kolom **_Modules_** yang hanya ada pada satu penyedia kursus. Penangan _missing value_ ini akan dilakukan pada tahap **_Data Preparation_**

* **_Univariate Analysis_**

    * **_Rating_**
    
    ![Gambar 2. Univariate Analysis Variabel *Rating* ](https://raw.githubusercontent.com/azri-andrizan/Assets/main/asset2/univariate_rating.png)
    
    Gambar 2. _Univariate Analysis_ Variabel *Rating*

        Berdasarkan Gambar 2 diatas, dapat dilihat bahwa Top-5 *Rating* dari yang tertinggi adalah 4.8, 4.7, 0.0, 4.6 dan 4.9. Terdapat satu _rating_ yang jauh dari _rating_ lainnya yaitu 0.0. Setelah dilakukan analisis, ternyata *rating* 0 ini adalah kursus yang tidak memiliki *review*. Sehingga dapat disimpulkan data ini bukanlah indikator data yang tidak valid, melainkan mencerminkan ketidakhadiran *review* dari pengguna.
    
    * **_Level_**
    *Value* pada variabel **_Level_** dihitung untuk melihat distribusi *level* nya. Berikut adalah *value* dari **_Rating_**

    |Level |Count|
    |:---- |:--- |
    |Beginner level |4871|
    |Intermediate level |2131|
    |Not specified |1106|
    |Advanced level |262|

    Berdasarkan data diatas, level kursus yang paling banyak distribusi nya adalah level *Beginner*. Kemudian terdapat *level* dengan keterangan *Not specified*, hal ini dianggap ketidaksesuaian *value* pada kolom *level*. Sehingga dilakukan penanganan pada bagian **_Data Preparation_** nantinya.

    *   **_Keyword_**

    ![Gambar 3. Univariate Analysis Variabel Keyword ](https://raw.githubusercontent.com/azri-andrizan/Assets/main/asset2/univariate_keyword.png)
    
    Gambar 3. _Univariate Analysis_ Variabel _Keyword_

    Visualisasi distribusi kolom Keyword menunjukkan bahwa terdapat 10 jenis _keyword_ utama yang tersebar dalam dataset. _Keyword_ "**Health**" memiliki frekuensi tertinggi, diikuti oleh "**Computer Science**" dan "**Data Science**" yang menunjukkan minat besar pada topik-topik ini. Sementara itu, *keyword* dengan frekuensi terendah adalah "**Arts and Humanities**" dan "**Math and Logic**". Distribusi ini mengindikasikan bahwa beberapa bidang lebih dominan dibandingkan yang lain, namun tetap memberikan keragaman topik yang cukup luas. Informasi ini memberikan gambaran awal tentang persebaran data yang relevan untuk digunakan dalam pengembangan model sistem rekomendasi nantinya.

    *   **_What you will learn_**
    
    ![Gambar 4. Univariate Analysis Variabel what you will learn ](https://raw.githubusercontent.com/azri-andrizan/Assets/main/asset2/univariate_whatyouwilllearn.PNG)
    
    Gambar 4. _Univariate Analysis_ Variabel _What you will learn_
    
    Kolom "**_What You Will Learn_**" berisi deskripsi materi yang akan dipelajari dalam setiap kursus. Namun, terdapat 3983 nilai "*Not Specified*", yang menunjukkan ketidaklengkapan informasi pada kursus tertentu. Selain itu, analisis awal menunjukkan adanya indikasi redundansi dengan kolom "**_Keyword_**", di mana informasi yang terkandung dalam "**_What You Will Learn_**" sering kali merepresentasikan kata kunci utama yang sudah dijelaskan di kolom tersebut. Oleh karena itu, pada tahap analisis ini, nilai "Not Specified" dibiarkan tanpa penanganan lebih lanjut, dan kolom ini tidak diprioritaskan untuk digunakan dalam model sistem rekomendasi. Jika dilakukan penanganan lebih lanjut akan memakan waktu dan daya komputasi yang lebih besar Langkah ini bertujuan untuk menjaga fokus pada fitur yang lebih relevan dan unik, tanpa mengesampingkan potensi kolom ini untuk pengembangan model yang lebih kompleks di masa depan.

    *   **_Skill Gain_**
    Pada tahap eksplorasi data awal, ditemukan bahwa kolom **_Skill Gain_** memiliki 2.619 nilai "*Not Specified*", yang mencakup sekitar 31% dari total data. Kolom ini memberikan informasi terkait keterampilan yang dapat diperoleh melalui kursus, namun setelah dilihat, dianggap adanya indikasi potensi redundansi dengan kolom **_Keyword_**, yang sudah mencerminkan aspek keahlian atau tema utama dari setiap kursus.
    
    Selain itu, banyaknya nilai "*Not Specified*" pada kolom ini dapat mempersulit pemanfaatannya secara efektif dalam model sistem rekomendasi, terutama pada tahap awal dengan fokus pada model sederhana. Oleh karena itu, untuk menjaga efisiensi dan kesederhanaan, kolom ini akan diabaikan terlebih dahulu. Langkah ini juga diambil agar analisis dan pengembangan model lebih terfokus pada fitur-fitur yang relevan dan memiliki distribusi nilai yang lebih lengkap.

    *   **_Duration to complete (Approx.)_**

    ![Gambar 5. Univariate Analysis Variabel Duration ](https://raw.githubusercontent.com/azri-andrizan/Assets/main/asset2/univariate_duration.PNG)
    
    Gambar 5. _Univariate Analysis_ Variabel _Duration to complete (Approx.)_

    Grafik menunjukkan distribusi durasi penyelesaian yang sangat miring ke kanan, dengan mayoritas tugas selesai dalam durasi kurang dari 50 satuan waktu. Frekuensi puncak terlihat pada interval durasi pendek, mengindikasikan proses penyelesaian yang umumnya cepat. Namun, terdapat beberapa outlier dengan durasi penyelesaian di atas 200 satuan waktu. Outlier ini tidak perlu dilakukan penanganan, karena jumlahnya yang tidak signifikan sehingga tidak memengaruhi pola utama distribusi data. Selain itu, durasi yang ekstrem dapat merepresentasikan kondisi khusus yang memang wajar terjadi, sehingga tidak relevan untuk dihapus atau diubah jika data tersebut masih memiliki konteks yang valid. Distribusi ini secara keseluruhan mencerminkan efisiensi dalam sebagian besar tugas, tanpa perlunya intervensi terhadap outlier.

    *   **_Number of Review_**
    
    ![Gambar 6. Univariate Analysis Variabel Number of Review ](https://raw.githubusercontent.com/azri-andrizan/Assets/main/asset2/univariate_review.png)
    
    Gambar 6. _Univariate Analysis_ Variabel _Number of Review_

    Grafik distribusi di atas menunjukkan bahwa data jumlah ulasan (Number of Review) memiliki skewness positif yang signifikan. Hal ini disebabkan oleh dominasi kursus dengan ulasan rendah dan keberadaan beberapa kursus dengan ulasan sangat tinggi yang menjadi outlier. Meskipun distribusi yang sangat skewed seperti ini terlihat mencolok, skewness tidak akan memengaruhi kinerja model rekomendasi secara signifikan.
    
    Alasan utama adalah karena sistem rekomendasi biasanya tidak bergantung langsung pada distribusi variabel tertentu, melainkan pada pola interaksi antar fitur.
    
# **_Data Preparation_**
Pada tahap _data preparation_, beberapa langkah dilakukan untuk memastikan kualitas data, memfasilitasi analisis yang lebih baik, dan meningkatkan kinerja model. Tahapan yang dilakukan meliputi:

## **_Missing Value Handling_** 
Berdasarkan identifikasi *missing value* pada tahap EDA sebelumnya, terdapat bari data yang kosong. Langkah yang diambil untuk penanganan adalah menghapus baris data yang memiliki *missing value* pada _**Modules**_, hal ini dianggap tidak akan mempengaruhi kualitas model rekomendasi secara signifikan, mengingat rendahnya *rating* dan ketiadaan ulasan pada kursus tersebut. Keputusan ini didasarkan pada kenyataan bahwa data yang hilang tersebut tidak memberikan kontribusi penting terhadap performa model, baik dari segi *rating* maupun relevansi konten. Penghapusan dilakukan dengan kode berikut:

```python
df_cleaned = df.dropna(subset=['Modules'])
df_cleaned.shape
```
Setelah dihapus total baris data pada dataset yang sebelumnya berjumlah 8370 menjadi 8337.

Kemudian, Berdasarkan EDA yang dilakukan sebelumnya, pada kolom _**Instructor**_ juga terdapat *missing value*. Maka dari itu dilakukan pendekatan berbasis pola data yang ada. *Missing value* diisi menggunakan nilai _**Instructor**_ yang paling sering muncul (*modus*) untuk setiap kombinasi unik dari _**module**_ dan _**offered_by**_. Pendekatan ini dipilih karena nilai _**instructor**_ berbentuk string yang merepresentasikan nama pengajar, dan modus memungkinkan pengisian berdasarkan instruktur yang paling umum dikaitkan dengan modul dan institusi tertentu. Dengan cara ini, konsistensi data dapat terjaga tanpa menambah bias atau kehilangan informasi penting, sekaligus memastikan dataset tetap lengkap untuk keperluan analisis lebih lanjut.

Dalam menangani *missing value* pada kolom _**Instructor**_, diterapkan metode *grouped mode* sebagai langkah utama untuk mengisi nilai yang hilang berdasarkan kombinasi kolom _**Modules**_ dan _**Offered By**_. Pendekatan ini dipilih karena secara logis, setiap kombinasi modul dan institusi penyedia seharusnya memiliki pengajar (*Instructor*) yang konsisten. Namun, setelah analisis mendalam, ditemukan beberapa kendala berikut:

1. Dari sekitar 8337 baris data, terdapat 62 kombinasi unik yang tidak memiliki nilai modus karena datanya terlalu beragam atau tidak cukup untuk menentukan instruktur yang dominan. Hal ini menyebabkan 88 baris data tetap memiliki nilai NaN atau diisi dengan *placeholder* (*Unknown*).

2. Setelah ditinjau lebih lanjut, baris-baris dengan *Unknown* pada kolom _**Instructor**_ cenderung tidak memiliki informasi tambahan yang signifikan di kolom lain, sehingga kontribusinya terhadap proses rekomendasi menjadi minimal.

3. Memasukkan baris dengan *Unknown* sebagai nilai *placeholder* berisiko memperkenalkan bias atau ketidaksesuaian dalam model rekomendasi. Hal ini dapat memengaruhi kualitas hasil rekomendasi.

4. Dengan total sekitar 8370 baris data, penghapusan 88 baris hanya memengaruhi 1.06% dari total data, sehingga tidak akan berdampak signifikan terhadap distribusi data atau performa model.

Berdasarkan evaluasi di atas, diputuskan untuk menghapus 88 baris data dengan nilai *Unknown* di kolom _**Instructor**_. Langkah ini dilakukan untuk:
- Memastikan integritas dataset yang digunakan dalam pelatihan model.

- Menghilangkan potensi bias yang mungkin diperkenalkan oleh nilai *placeholder*.

- Menjaga fokus pada baris data yang memiliki informasi lengkap dan relevan.

Setelah dilakukan penghapusan, dataset yang sebelumnya terdiri dari 8337 baris data menjadi 8249.

## **_Inproppriate Value_**
Seperti yang telah dilakukan analisis pada tahap EDA, terdapat ketidaksesuaian *value* pada variabel **_Level_** yaitu *Not specified*. 

|Level |Count|
|:---- |:--- |
|*Beginner level* |4871|
|*Intermediate level* |2131|
|*Not specified* |1106|
|*Advanced level* |262|

Untuk menangani hal itu dilakukan pendekatan dengan mencari pola berdasarkan hubungan dengan variabel lainnya. Kemudian mencoba mengkategorikan ulang baris data *Not specified* pada variabel **_Level_** ini diantara 3 *level* lainnya. (*Beginner*, *Intermediate*, *Advanced*).

Mencari pola kesamaan berdasarkan rata-rata nilai *rating*:
|Level | |
|:---- |:--- |
|*Beginner level* |4.02|
|*Intermediate level* |3.80|
|*Not specified* |4.37|
|*Advanced level* |3.82|

Berdasarkan pola rata-rata nilai *rating* *level not specified*, rata-ratanya lebih tinggi dibanding nilai *level* lainnya. Untuk sementara, belum terdapat pola yang jelas. Kemudian dilanjutkan dengan memeriksa pola kesamaan berdasarkan Durasi.

|Level | |
|:---- |:--- |
|*Beginner level* |31.25|
|*Intermediate level* |29.65|
|*Not specified* |16.20|
|*Advanced level* |43.69|

Berdasarkan rata-rata nilai *Duration to complete (Approx.)*, rata-rata nilai *not specified* jauh lebih rendah daripada *level* lainnya. Ini mengindikasikan bahwa *not specified* adalah kursus yang dapat diselesaikan dengan waktu yang relatif cepat. Bisa jadi ini termasuk kedalam level *Intermediate* atau *Beginner* karena rata-rata durasi mendekati *level* tersebut.

![Gambar 7. Inproppriate value ](https://raw.githubusercontent.com/azri-andrizan/Assets/main/asset2/inpropriate_value.png)

Gambar 7. Distribusi _Inproppriate Value_ *rating* dan durasi

Berdasarkan Boxplot diatas, dapat dilihat bahwa untuk level *Not specified* lebih cenderung mirip pola nya dengan level *Beginner* dan *Intermediate*. Sehingga langkah yang diambil selanjutnya adalah mengkategorikan ulang level *Not specified* ini berdasarkan rentang _**Rating**_ dan _**Duration to complete (Approx.)**_.

Sehingga dilakukan pengkategorian ulang level *not specified* dengan ketentuan jika durasi lebih kecil dari nilai 30 maka akan dikategorikan sebagai *Intermediate level*, dan jika durasi lebih kecil dari 50 maka akan dikategorikan sebagai *Beginner Level*. Hasilnya setelah dilakukan pengkategorian ulang berdasarkan *rating* dan durasi, ternyata masih terdapat 104 buah data yang masih tidak terkategorikan ke *Beginner* ataupun *Intermediate* berdasarkan *rating* dan durasi. Data ini dianggap ambigu dan tidak mempunyai pola yang jelas yang terdistribusi pada dataset. Sehingga diputuskan untuk menghapus sisa pengkategorian ulang ini. Alasan penghapusan ini adalah :
1. Dari total data yang ada, 104 baris hanya merupakan bagian kecil dari dataset. Penghapusan ini tidak akan berdampak signifikan pada hasil analisis.

2. Data *Not specified* tidak dapat dikelompokkan ke dalam kategori *Beginner*, *Intermediate*, atau *Advanced* bahkan setelah beberapa kriteria diterapkan. Hal ini menunjukkan data ini memiliki karakteristik yang ambigu.

3. Keberadaan kategori *Not specified* dapat mengurangi akurasi dan interpretasi analisis. Sebagai contoh, jika dilakukan analisis hubungan antara _**Level**_ dan _**Rating**_, kategori ini dapat menimbulkan bias karena tidak mencerminkan level yang sebenarnya.

## **_Numerical Features Normalization_**
Langkah normalisasi fitur numerik dalam proyek ini dilakukan untuk memastikan bahwa nilai dari setiap fitur berada dalam rentang yang sama, yaitu antara 0 dan 1. Normalisasi ini penting untuk menghindari dominasi fitur dengan skala nilai yang lebih besar dalam proses analisis atau pemodelan.

Pada proyek ini, terdapat tiga fitur numerik yang dinormalisasi, yaitu:

*   *Rating*: Merepresentasikan penilaian yang diberikan pada level tertentu.
*   Duration to complete (Approx.): Estimasi waktu yang dibutuhkan untuk menyelesaikan.
*   Number of review: Jumlah ulasan yang diberikan oleh pengguna.

Proses normalisasi menggunakan metode MinMaxScaler, yang menormalisasikan nilai pada ketiga variabel tersebut dalam rentang 0 dan 1.

## **_Categorical Encoding Features_**
Dalam proyek ini, proses *categorical encoding* diterapkan pada fitur **_Level_**, yang merupakan satu-satunya fitur kategorikal yang digunakan dalam model. Fitur ini berisi informasi tingkat kesulitan kursus yang terbagi menjadi tiga kategori: *Beginner*, *Intermediate*, dan *Advanced*. Karena fitur ini bersifat ordinal, yaitu memiliki urutan logis antar kategori, metode *Label Encoding* dipilih sebagai teknik *encoding* yang paling sesuai.

Metode *Label Encoding* mengubah setiap kategori menjadi representasi numerik yang merefleksikan urutan logisnya. Sebagai contoh, *Beginner* direpresentasikan dengan nilai 0, *Intermediate* dengan nilai 1, dan *Advanced* dengan nilai 2. Proses ini memastikan bahwa model dapat menangkap hubungan hierarkis antar kategori, sehingga informasi mengenai tingkat kesulitan tetap terjaga.

*Encoding* pada fitur **_Level_** memberikan manfaat signifikan dalam mempermudah model memahami perbedaan tingkat kesulitan kursus, yang merupakan salah satu faktor penting dalam merekomendasikan kursus yang relevan kepada pengguna. Dengan transformasi ini, model dapat mengintegrasikan fitur tersebut tanpa menimbulkan bias atau kehilangan informasi.

Selain itu, karena hanya satu fitur kategorikal yang diterapkan proses encoding, dampaknya terhadap dimensi dataset dan kompleksitas komputasi model sangat minimal. Hal ini juga mengurangi risiko *overfitting*, karena representasi numerik yang sederhana tidak memperkenalkan hubungan non-linear yang tidak relevan.

Penerapan *encoding* ini menunjukkan perhatian terhadap pentingnya menjaga integritas data, sambil tetap memastikan model dapat memanfaatkan fitur ini untuk menghasilkan prediksi yang lebih akurat dan relevan bagi pengguna. 

```python
# Melakukan encoding pada kolom Level
df_prep['Level_encoded'] = label_encoder.fit_transform(df_prep['Level'])
```
## **_Text Features Preprocessing_**
Dalam proyek ini, dilakukan text preprocessing untuk kolom teks seperti **_Modules_**, **_Instructor_**, dan **_Keyword_**. Langkah-langkah yang diterapkan meliputi:

1. Pembersihan Teks:
  - Menghapus karakter khusus, tanda baca, atau simbol yang tidak relevan untuk mengurangi kebisingan dalam data.
  - Mengubah semua teks menjadi huruf kecil (_lowercase_) agar konsisten dalam pemrosesan.
2. Representasi Teks dengan *Transformer Sentence Embedding*:
  - Menggunakan model *pre-trained* berbasis *transformer*, yaitu *SentenceTransformer*, untuk merepresentasikan teks ke dalam bentuk *embedding* vektor. Metode ini memungkinkan teks diproses dengan mempertimbangkan hubungan semantik antar kata dan frasa.

Model *transformer* digunakan karena kemampuannya dalam memahami konteks bahasa secara mendalam dan menghasilkan representasi numerik berkualitas tinggi yang dapat langsung digunakan oleh model sistem rekomendasi.

Pendekatan ini dipilih karena fleksibilitas dan efektivitasnya dalam menangkap makna semantik dari teks, termasuk pada kolom yang mengandung variasi bahasa atau istilah teknis seperti pada **_Modules_** dan **_Instructor_**. Dengan transformasi ini, data teks menjadi format numerik yang dapat diproses oleh algoritma **_machine learning_**, sehingga meningkatkan akurasi dan relevansi hasil rekomendasi.

*Preprocessing* menggunakan kode definisi berikut, untuk menghapus karakter non-alfabet namun masih tetap mendukung karakter *Unicode*/multibahasa. Namun, sebelumnya telah dilakukan pengecekan bahasa apa saja yang terdapat dalam kolom *Text features* menggunakan library **langdetect**.

```python
import re
def clean_text(text):
    # Hanya menghapus karakter non-alfabet, namun tetap mendukung karakter Unicode (multibahasa)
    return re.sub(r'[^\w\s]', '', text, flags=re.UNICODE)
```

Kemudian, proses *Embedding* dilakukan dengan *SentenceTransformer* direalisasikan dengan kode berikut :
```python
def get_sentence_embedding(text):
    if isinstance(text, str):
        return model.encode(text)
    return [0] * 512  # Ukuran default embedding untuk model ini
```

berikut adalah contoh hasil **embedding*nya :

![Gambar 8. Hasil Embedding ](https://raw.githubusercontent.com/azri-andrizan/Assets/main/asset2/embedding.PNG)

Gambar 8. Hasil *Embedding*

Hasil *embedding* ini dikonversi menjadi array agar lebih kompatibel saat digunakan untuk model nantinya. Selanjutnya hasil *embedding* ini mempunyai dimensi yang cukup besar, agar lebih efisien maka digunakan teknik PCA (*Principal Component Analysis*). Sehingga dimensi awal *embedding* yang berdimensi (8145, 1536) setelah di lakukan teknik PCA menjadi (8145, 239).

## **_Features for Content-Based Filtering_**
Pada pendekatan content-based filtering (CBF), fitur-fitur yang digunakan bertujuan untuk memahami karakteristik kursus berdasarkan atribut deskriptifnya. Fitur-fitur yang dipilih adalah:

1. **_Modules_**
    Berisi deskripsi topik atau materi yang dibahas dalam kursus. Kolom ini diproses menggunakan *transformer-based embeddings* untuk menangkap makna semantik yang relevan, sehingga memungkinkan sistem memahami konteks konten kursus.

2. **_Instructor_**
    Menyediakan informasi mengenai pengajar kursus. Nama instruktur sering kali dapat memengaruhi relevansi atau daya tarik kursus, terutama jika pengajar memiliki reputasi atau spesialisasi tertentu.

3. **_Level_**
    Mengindikasikan tingkat kesulitan kursus, seperti "*Beginner*," "*Intermediate*," atau "*Advanced*." Informasi ini membantu sistem merekomendasikan kursus yang sesuai dengan tingkat kemampuan pengguna.

4. **_Keyword_**
    Berisi kata kunci utama yang terkait dengan konten kursus. Kata kunci ini membantu memperjelas fokus kursus, sehingga dapat mencocokkan kebutuhan pengguna dengan kursus yang relevan.

Fitur-fitur ini dirancang untuk memastikan rekomendasi berbasis konten sesuai dengan preferensi pengguna berdasarkan karakteristik kursus.


## **_Features for Popularity-Based Filtering_**
Pada pendekatan _popularity-based filtering_ (PBF), fitur-fitur yang digunakan berfokus pada indikator popularitas kursus. Fitur yang digunakan adalah:

1. **_Rating_**
    Merupakan rata-rata skor yang diberikan pengguna terhadap kursus. Kursus dengan rating tinggi cenderung dianggap lebih berkualitas dan diminati banyak orang.

2. **_Number of Review_**
    Mengacu pada jumlah ulasan yang diterima oleh kursus. Jumlah ulasan digunakan sebagai metrik popularitas tambahan, di mana kursus dengan banyak ulasan biasanya memiliki tingkat partisipasi atau kepuasan yang tinggi.

Pendekatan ini memastikan sistem dapat merekomendasikan kursus berdasarkan popularitasnya di antara pengguna secara umum, tanpa memperhitungkan preferensi personal.


# **_Modelling_**
## Modelling of System Recommendation

Pada proyek ini, proses *modelling* dilakukan untuk mengembangkan sistem rekomendasi menggunakan pendekatan *Content-Based Filtering* (CBF) dan *Popularity-Based Filtering* (PBF). 

1. *Modelling* untuk *Content-Based Filtering* (CBF):
Model ini dirancang untuk merekomendasikan kursus berdasarkan kesamaan konten antara kursus dan preferensi pengguna. Metode yang digunakan adalah *Algoritme cosine similarity*. Algoritma ini digunakan untuk menghitung tingkat kesamaan antar kursus. Hasil perhitungan ini digunakan untuk merekomendasikan kursus dengan konten yang paling mirip dengan preferensi pengguna.

2. *Modelling* untuk *Popularity-Based Filtering* (PBF):
Pendekatan ini memanfaatkan fitur populer, seperti *Rating* dan *Number of Review*, untuk menentukan rekomendasi berdasarkan popularitas kursus secara umum. 

Kedua model ini digunakan untuk memberikan rekomendasi yang relevan dan bervariasi, menggabungkan pendekatan personalisasi melalui CBF dan rekomendasi berbasis popularitas dengan PBF. Model ini memungkinkan sistem rekomendasi untuk melayani kebutuhan pengguna yang berbeda, baik yang memiliki preferensi spesifik maupun yang baru memulai eksplorasi kursus.

## **_Content-Based Filtering_**
Pada model ini, digunakan algoritma **_Cosine Similarity_**. *Cosine Similarity* adalah metode pengukuran kesamaan antara dua vektor dalam ruang multidimensi. Metode ini sering digunakan dalam *information retrieval*, *natural language processing*, dan sistem rekomendasi untuk membandingkan dokumen, teks, atau elemen lain yang direpresentasikan dalam bentuk vektor. *Cosine Similarity* mengukur kesamaan berdasarkan sudut antara dua vektor, bukan panjangnya. Nilainya berkisar antara -1 hingga 1:
*   Nilai 1 menunjukkan bahwa vektor sepenuhnya serupa (arahnya sama).
*   Nilai 0 menunjukkan tidak ada kesamaan (vektor ortogonal).
*   Nilai -1 menunjukkan bahwa vektor sepenuhnya berlawanan.

Dalam konteks sistem rekomendasi, vektor bisa berupa representasi fitur item (seperti kursus, produk, atau dokumen). *Cosine Similarity* digunakan untuk mengukur kesamaan antar item untuk memberikan rekomendasi berdasarkan kedekatan item di ruang vektor.

Pada proyek ini dibuat sebuah fungsi yang akan menghitung *Cosine Similarity* dengan nama fungsi *recommend_cbf_with_names*. Awalnya fungsi ini akan menemukan indeks kursus berdasarkan judul kursus yang diinput. Lalu akan menghitung kemiripan kursus tersebut dengan semua kursus lainnya. Indeks kursus dengan skor tertinggi akan diambil, kemudian berdasarkan indeks hasil rekomendasi tersebut akan ditampilkan *course title* nya sebagai hasil rekomendasi nama kursus.

Hasilnya setelah dilakukan percobaan adalah sebagai berikut.

![Gambar 9. Percobaan cbf ](https://raw.githubusercontent.com/azri-andrizan/Assets/main/asset2/cbf_contoh.PNG)

Gambar 9. Hasil Rekomendasi dari model CBF

Dari hasil tersebut dapat dilihat bahwa disaat kursus dengan judul "_Applied AI with DeepLearning_" diinput maka hasil rekomendasinya adalah kursus yang memiliki kesamaan/relevan. Top-5 kursus yang direkomendasikan terlihat cocok dengan judul kursus yang diinputkan dan semuanya adalah tentang *Machine Learning* dan AI (*Artificial Intelligence*).

## **_Popularity-Based Filtering_**
Pada model *Popularity-Based Filtering* (PBF) ini, akan menampilkan Top-N *recommendation* kursus yang paling populer. Rekomendasi akan diberikan berdasarkan *top rating* dan *top review*. Pada proyek ini digunakan sebuah fungsi dengan nama *recommend_pbf*, fungsi ini bekerja dengan tahapan yang terstruktur. Dimulai dengan membuat skor popularitas, skor popularitas didapatkan melalui perkalian *rating* dan *Number of review*. Lalu fungsi *recommend_pbf* akan mengurutkan kursus berdasarkan skor popularitas. Setelah diurutkan indeks top-n akan dicocokkan dengan judul kursus pada dataset, lalu menampilkan judul kursus yang paling populer. Fungsi ini ditambah dengan logika, untuk tidak menampilkan nama kursus yang sama sebagai duplikat pada hasil rekomendasi. Jadi judul kursus yang diambil adalah top-n rekomendasi yang unik.

Hasilnya setelah dilakukan percobaan adalah sebagai berikut.

![Gambar 10. Percobaan pbf ](https://raw.githubusercontent.com/azri-andrizan/Assets/main/asset2/pbf.PNG)

Gambar 10. Hasil Rekomendasi dari model PBF

Dari hasil diatas dapat dilihat kursus yang paling populer adalah kursus dengan bidang *Computer Science* dan *Information Technology*. Sesuai dengan hasil EDA pada kolom *Keyword* bahwa kedua bidang ini adalah yang paling banyak distribusi nya pada dataset.

## **_Hybrid Recommendation Model_**
Dua model sebelumnya digabungkan untuk mendapatkan hasil rekomendasi yang lebih tepat. Pada *Hybrid Recommendation Model* ini digunakan fungsi **hybrid_recommend**, dimana pada fungsi ini terdapat perbedaan pada fungsi-fungsi sebelumnya. Terdapat pembobotan antara dua model sebelumnya, pada contoh penggunaan ini, pembobotan dilakukan dengan masing-masing CBF=0.5 dan PBF=0.5. Skor PBF dan CBF digabungkan dan dikonversi keskala yang sama, menambahkan bobot dari kedua model tersebut. Hasilnya akan menampilkan judul kursus yang relevan dengan judul yang diinput, seperti pada contoh penggunaan berikut.

![Gambar 11. Percobaan hybrid ](https://raw.githubusercontent.com/azri-andrizan/Assets/main/asset2/hybrid.PNG)

Gambar 11. Hasil Rekomendasi dari model *Hybrid*

Sama seperti sebelumnya, hasil rekomendasi relevan dengan judul kursus yang diinputkan namun rekomendasi ini juga berdasarkan *top rating* dan *top review*, sehingga selain kursus yang relevan sistem juga lebih mengutamakan kursus yang memiliki rating yang tinggi. 
# **Model Evaluasi**
Untuk mengevaluasi performa model prediktif kegagalan mesin, digunakan tiga metrik utama yang saling melengkapi, yaitu _precision_, _coverage_ dan _recall_. Metrik-metrik ini dipilih untuk memberikan evaluasi yang komprehensif terkait kualitas rekomendasi yang dihasilkan.

Berikut adalah beberapa metrik yang digunakan pada proyek ini [[5], [6]]:
1. **Precision**. 
    *Precision* mengukur seberapa relevan item yang direkomendasikan oleh model terhadap pengguna tertentu. *Precision* dihitung sebagai proporsi item relevan yang benar-benar direkomendasikan terhadap total item yang direkomendasikan.
    $$
    Precision = \frac{Jumlah   item   relevan   yang   direkomendasikan}{Jumlah   Total   Item   yang   direkomendasikan}

2. **Recall**
    Recall mengukur sejauh mana model berhasil merekomendasikan seluruh item relevan yang tersedia dalam dataset. Ini dihitung sebagai proporsi item relevan yang direkomendasikan terhadap total item relevan yang ada.
    $$
    Recall = \frac{Jumlah   Item   Relevan   yang   Direkomendasikan}{Jumlah   Total   Item   Relevant   Didataset}
    $$
    
    Recall relevan dalam konteks di mana sistem rekomendasi bertujuan untuk memastikan bahwa sebanyak mungkin item relevan diungkapkan kepada pengguna.

3. **Coverage**
    Coverage adalah metrik yang mengukur keragaman item yang direkomendasikan. Coverage mengevaluasi apakah model dapat merekomendasikan beragam item dari keseluruhan katalog, bukan hanya fokus pada subset item populer.
    $$
    Coverage = \frac{Jumlah   Item   Unik   yang   Direkomenasikan}{Jumlah    Total     Item     Dalam     Katalog}
    $$
    
    Metrik ini penting untuk memastikan bahwa sistem rekomendasi memberikan rekomendasi yang lebih inklusif, mendorong eksplorasi, dan tidak hanya terfokus pada item yang sering muncul.




# **Referensi**
[[1]]  E-learning Market: Size and Forecasts with Impact Analysis of COVID-19 (2020-2024)," Daedal Research, Research and Markets, Sept. 2020. [Online]. Available: https://www.researchandmarkets.com/reports/5012540/e-learning-market-growth-trends-covid-19. [Accessed: Dec. 11, 2024].

[[2]]  T. Beck, "3 Technology Solutions to Provide Support in the Post-COVID-19 Classroom," EdTech Magazine, May 18, 2021. [Online]. Available: https://edtechmagazine.com/k12/article/2021/05/3-technology-solutions-provide-support-post-covid-19-classroom-perfcon. [Accessed: Dec. 11, 2024].

[[3]]  [Accessed: Dec. 11, 2024].

[[4]] [Accessed: Dec. 11, 2024].

[[5]] C. C. Aggarwal, *Recommender Systems: The Textbook*. Springer, 2016. [Online]. Available: https://link.springer.com/book/10.1007/978-3-319-29659-3[Accessed: Dec. 11, 2024].

[[6]] F. Ricci, L. Rokach, and B. Shapira, *Recommender Systems Handbook*. Springer, 2015. [Online]. Available: https://link.springer.com/book/10.1007/978-1-4899-7637-6 [Accessed: Dec. 11, 2024].






[1]: https://www.researchandmarkets.com/reports/5012540/e-learning-market-growth-trends-covid-19
[2]: https://edtechmagazine.com/k12/article/2021/05/3-technology-solutions-provide-support-post-covid-19-classroom-perfcon
[3]:
[4]:
[5]: https://link.springer.com/book/10.1007/978-3-319-29659-3
[6]: https://link.springer.com/book/10.1007/978-1-4899-7637-6