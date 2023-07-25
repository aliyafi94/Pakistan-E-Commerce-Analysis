# Data-Analytics_Pakistan_E-Commerce_Datasets

Project ini sebagai bahan penilaian Capstone Purwadhika Data Science

## **1. Latar Belakang**
E-Commerce didefinisikan sebagai proses jual dan beli barang atau jasa termasuk produk digital melalui transaksi elektronik menggunakan jaringan internet atau media yang berbasis komputer lainnya (State Bank of Pakistan). Pertumbuhan E-Commerce di Pakistan sangat cepat dalam beberapa tahun terakhir. menurut Forbes, Pakistan berada di Top 5 Negara dengan laju pertumbuhan pasar freelance tercepat di Dunia mengalahkan India dan Russia yang memiliki jumlah penduduk yang jauh lebih besar ([E-Commerce Policy of Pakistan, hal. 29](https://www.commerce.gov.pk/wp-content/uploads/2019/11/e-Commerce_Policy_of_Pakistan_Web.pdf)). Dengan kondisi tersebut, Perusahaan akan melakukan study dengan data yang sudah diperoleh yang akan dianalisa supaya dapat memanfaatkan kondisi E-Commerce yang akan naik di masa-masa mendatang. 

## **2. Pernyataan Masalah**
Dalam E-Commerce, terdapat sebuah fitur bernama **DISKON** dimana fitur ini tentunya cukup digemari oleh sebagian orang karena memberikan potongan harga yang tentunya membuat harga barang yang dibeli menjadi lebih murah dari harga normalnya.<br>
Perusahaan ingin mengetahui apakah fitur **DISKON** tersebut memiliki terhadap hubungan perilaku konsumen dalam bertransaksi di E-Commerce. informasi ini akan membantu Perusahaan dalam menentukan strategi jual beli di masa-masa mendatang.<br>

Sebagai seorang *data analyst*, kita akan mencoba menjawab pertanyaan berikut:

**Bagaimana hubungan diskon dengan karakteristik transaksi pada E-Commerce, terutama dibandingkan dengan tidak menggunakan fitur diskon**

## **3. Data**

dataset ini didapat dari [di sini](https://www.kaggle.com/datasets/zusmani/pakistans-largest-ecommerce-dataset)<br>
Mengacu dari informasi Kaggle bahwa Kumpulan data *pakistan's Largest E-Commerce Dataset* ini dikumpulkan sebagai bagian dari studi penelitian (Sensus Startup) di Startup E-Commerce Pakistan antara Januari 2016 hingga Desember 2018.
dataset ini memiliki catatan transaksi dari bulan Maret 2016 - Agustus 2018.

Secara umum, kita bisa melihat bahwa:
* dataset ini memiliki 26 kolom dan 1.048.575 baris.
* semua kolom memiliki data kosong, yang diwakili dengan data NaN.
* kolom `Unnamed: 21`,  `Unnamed: 22`,  `Unnamed: 23`,  `Unnamed: 24`, dan `Unnamed: 25` berisi 100% data kosong sehingga tidak relevan dalam analisis dan bisa dihapus saja.
* kolom `status`, `category_name_1`, dan `sales_comission_code` memiliki data dengan value '\N', sedangkan kolom `BI Status` memiliki data dengan value '#REF!' sehingga akan ditangani.
* kolom `grand_total` dan `discount_amount` terdapat data minus, dan pada kolom `price` terdapat data dengan value 0. hal ini tidak masuk akal sehingga akan ditangani.
* beberapa data pada kolom `grand_total` tidak mencerminkan perhitungan yang semestinya, sehingga akan ditangani.
* kolom ` MV` terdapat spasi ((spasi)MV(spasi)) sehingga akan dirubah dan merubah kolom `category_name_1` menjadi `category`.
* beberapa kolom, seperti `Working Date`, `BI Status`, `Year`, `Month`, `Customer Since`, `FY` dan `Customer ID` memiliki huruf Kapital dalam penulisannya, sehingga akan dirubah menjadi huruf kecil semua dan diberikan separator (_) pada kolom yang memiliki 2 kata.
* Urutan kolom akan diatur ulang untuk mempermudah proses analisis selanjutnya.

##### **3.2.2 Missing Value**<br>
Secara garis besar:  
* *missing value* di kolom `Unnamed: 21`,  `Unnamed: 22`,  `Unnamed: 23`,  `Unnamed: 24`, dan `Unnamed: 25` sebanyak **100%**.
* *missing value* untuk kolom lain sebesar > **44%** sedangkan pada kolom `sales_comission_code` di angka **57%**.

Ada 2 cara untuk menangani *missing value*:
* **pertama**, menghapus baris/kolom yang berisi *missing value*.\
a) kolom `Unnamed: 21`,  `Unnamed: 22`,  `Unnamed: 23`,  `Unnamed: 24`, dan `Unnamed: 25` akan dihapus karena **100%** datanya adalah *missing value*.\
b) untuk kolom `item_id`, `status`, `created_at`, `sku`, `price`, `qty_ordered`, `grand_total`, `increment_id`, `category_name_1`, `sales_comission_code`, `discount_amount`, `payment_method`, `Working Date`, `BI Status`, `MV`, `Year`, `Month`, `Customer Since`, `M-Y`, `FY`, dan `Customer ID` akan dihapus juga *missing value* nya karena setelah dilihat melalui heatmap **posisi data** *missing value* relatif pada baris yang sama walaupun presentase *missing value* nya sangat tinggi (> 44%).
* **kedua**, mengisi data yang hilang. Ada beberapa metode yang bisa digunakan untuk mengisi missing value, cara yang paling baik adalah dengan mengisi data yang hilang dengan nilai sebenarnya, atau sedekat mungkin dengan nilai asli. Dalam kasus ini, kita akan mencoba mengisi *missing value* berdasarkan kolom lain yang secara domain knowledge atau secara statistik berkaitan dengan kolom yang memiliki *missing value*. Jika masih ada kolom yang tidak bisa diisi, barulah kita mengisi dengan angka *mean, median* atau *modus*. Menghapus data akan menjadi opsi terakhir.

##### **3.2.3 Data Formatting**<br>
Ada beberapa hal yang perlu kita tangani supaya data menjadi lebih clean:
* kolom `grand_total` dan `discount_amount` terdapat data minus.
* beberapa data pada kolom `grand_total` tidak mencerminkan perhitungan yang semestinya.
* kolom ` MV` terdapat spasi `(spasi)MV(spasi)` sehingga akan dirubah dan merubah kolom `category_name_1` menjadi `category`
* data type setiap kolom perlu disesuaikan
* kolom `M-Y` akan dirubah namanya menjadi `month_year`.
* beberapa kolom, seperti `Working Date`, `BI Status`, `Customer Since`, `Month`,`Year`, `FY` dan `Customer ID` memiliki huruf Kapital dalam penulisannya, sehingga akan dirubah menjadi huruf kecil semua dan diberikan separator `_` pada kolom yang memiliki 2 kata.
* Urutan kolom akan diatur ulang untuk mempermudah proses analisis selanjutnya.
* mengkelompokkan kolom `status` dan `payment_method` untuk memudahkan proses analisa.

Sebelum dibersihkan, kita memiliki 1.048.575 baris data, sekarang kita memiliki 582.992 baris. Sekitar 420.000 baris data yang kosong dihapus, dan sisa data kosong diisi dengan data yang dirasa relevan.

## **4. Analisis**

Kita sudah melakukan tahap *data cleaning*. Sekarang, kita bisa mulai melakukan analisis untuk mencari tahu **Bagaimana hubungan diskon dengan karakteristik transaksi pada E-Commerce, terutama dibandingkan dengan tidak menggunakan fitur diskon**.

Pertama, kita perlu mengkategorikan transaksi yang memiliki diskon dan tidak memiliki diskon. untuk membantu kita mempermudah proses analisa.

### **4.1 Tren Revenue E-Commerce**

* Data yang digunakan setiap tahun berbeda, 2016 (7 bulan), 2017 (12 bulan), 2018 (7 bulan) sehingga kita akan melihat tren Revenue menggunakan Nilai Tengah. supaya kita ada gambaran bagaimana prospek E-Commerce kedepannya.
* Data yang digunakan pun adalah data dengan status transaksinya berhasil atau *completed* karena Revenue adalah dana yang sudah masuk kepada penjual [sumber](https://www.investopedia.com/terms/r/revenue.asp).

### **4.2 Hubungan Diskon terhadap Jumlah Transaksi**

Untuk Jumlah Transaksi, kita menggunakan seluruh transaksi tanpa melihat statusnya supaya ada gambaran *behaviour* pembeli di E-Commerce.<br>
mari kita lihat, hubungan diskon terhadap Jumlah Transaksi. kita akan menganalisis banyak diskon yang dipakai dengan jumlah transaksi untuk menjawab pertanyaan sebagai berikut:
* bagaimana banyak diskon yang dipakai setiap bulan dari 2016 sampai 2018?
* bagaimana banyak diskon yang dipakai setiap bulan dari 2016 sampai 2018 dibandingkan dengan jumlah transaksi?
* Apakah ada hubungan antara banyak diskon yang dipakai dengan jumlah transaksi?

### **4.3 Diskon Berdasarkan Category**

mari kita lihat, hubungan diskon berdasarkan category. kita akan menganalisis banyak diskon yang dipakai dengan category untuk menjawab pertanyaan sebagai berikut:
* Manakah Kategori dengan transaksi terbanyak?
* Manakah Kategori yang memakai diskon terbanyak?
* Apakah ada hubungan antara Banyak diskon yang dipakai dengan Kategori?

### **4.4 Diskon Berdasarkan Payment Method**

mari kita lihat, Hubungan diskon berdasarkan payment method. kita akan menganalisis banyak diskon yang dipakai dengan payment method untuk menjawab pertanyaan sebagai berikut:
* Manakah Payment Method dengan transaksi terbanyak?
* Manakah Payment Method yang memakai diskon terbanyak?
* Apakah ada hubungan antara diskon dengan payment method?

### **4.5 Diskon Berdasarkan Status**

mari kita lihat, transaksi dengan diskon maupun tidak berdasarkan Status. kita akan menganalisis banyak diskon yang dipakai dengan Status untuk menjawab pertanyaan sebagai berikut:
* Bagaimana status transaksi Pakistan E-Commerce?
* Apakah ada hubungan antara diskon dengan status transaksi?

### **4.6 Hubungan Diskon terhadap Total Revenue**

Untuk Revenue kita menggunakan transaksi dengan status *completed* karena kita beranggapan revenue adalah dana yang sudah masuk ke penjual.<br>
mari kita lihat, hubungan diskon terhadap Jumlah Revenue pada setiap kategori dan payment method. kita akan menganalisis diskon yang dipakai dengan Total Revenue untuk menjawab pertanyaan sebagai berikut:
* Manakah kategori yang transaksi memilki Total Revenue tertinggi?
* Manakah payment method yang transaksi memilki Total Revenue tertinggi?
* Apakah rata-rata transaksi menggunakan diskon sama dengan rata-rata transaksi tanpa diskon?

## **5. Kesimpulan dan Rekomendasi**
### **5.1 Kesimpulan**

Dari analisis yang telah dilakukan, kita dapat menarik kesimpulan tentang transaksi pada E-Commerce di Pakistan:
* Tren Revenue E-Commerce di Pakistan naik dari 2016 sampai 2018
* Dari 582.992 data transaksi, 208.153 transaksi yang menggunakan diskon atau 35.70% dari keseluruhan data.
* Jumlah diskon yang dipakai setiap bulannya memiliki variasi yang cukup tinggi.
* `Mobiles & Tablets` menjadi kategori yang paling banyak jumlah transaksinya.
* Transaksi dengan `COD` merupakan cara yang paling digemari di Pakistan.
* Jumlah transaksi *canceled* dan *problem* relatif cukup tinggi, meskipun transaksi *completed* masih yang tertinggi.
* Total Revenue pada kategori `Mobiles & Tablets` menjadi yang tertinggi
* Transaksi menggunakan `Vouchers` menyumbang total revenue tertinggi.

Hubungan diskon dengan karakteristik transaksi pada E-Commerce Pakistan , dibandingkan dengan transaksi tanpa diskon:
* Jumlah transaksi yang menggunakan diskon memiliki hubungan yang kuat dengan jumlah transaksi, artinya semakin banyak transaksi yang menggunakan diskon maka semakin banyak pula transaksi yang terjadi.
* Transaksi menggunakan diskon cenderung terjadi pada kategori dengan harga yang relatif lebih tinggi yaitu pada `Entertainment` dan `Appliances`.
* Orang Pakistan lebih suka menggunakan diskon pada pembayaran menggunakan `Vouchers` dan `Mobile Wallet`.
* Meskipun cenderung tidak terjadi *problem*, angka transaksi *canceled* pada transaksi yang menggunakan diskon relatif cukup tinggi.
* Rata-rata revenue transaksi menggunakan diskon lebih besar daripada tanpa diskon

### **5.2 Rekomendasi**

Diskon menjadi fitur yang sangat penting karena terbukti dapat meningkatkan jumlah transaksi dan mendapatkan revenue yang lebih baik dibanding tanpa menggunakan diskon. Kita mencoba memberikan rekomendasi guna semakin meningkatkan jumlah transaksi dan revenue.
1. Penawaran diskon dilakukan lebih merata setiap bulannya, tidak terpaku pada *Black Friday* yang terjadi di bulan November. Bisa dilakukan dengan metode `1.1` artinya tanggal 1 di bulan Januari dan dilakukan sama di bulan selanjutnya `2.2`, `3.3` dst. atau bisa juga dengan memanfaatkan momen Hari Pakistan maupun Hari Kemerdekaan.
2. Berikan diskon untuk item yang harganya relatif lebih tinggi.
3. Fokus pemberian diskon pada transaksi yang menggunakan `Vouchers` dan `Mobile Wallet` guna mendorong masyarakat beralih dari transaksi `COD` untuk memperkecil potensi terjadinya masalah terutama pada aliran dana transaksi.
4. Transaksi *canceled* dan *problem* tentunya menghambat revenue yang didapatkan. Namun, belum bisa dipastikan penyebab dari transaksi *canceled* maupun *problem*. Perlu analisa lebih mendalam untuk mendapatkan informasi yang relevan terkait hal tersebut. Namun, kita coba untuk memberikan saran guna memperkecil transaksi *canceled* maupun *problem*:
    * Berikan informasi yang jelas pada kolom deskripsi supaya menghindari *miss-information*
    * Lakukan QC dan Video proses pengemasan sebelum produk dikirim ke pembeli
    * Update Stok secara berkala
    * Cantumkan gambar yang sesungguhnya dengan resolusi yang baik
    * Process pengiriman sebelum due date
    * Meminta pembeli untuk melakukan proses video saat unboxing
    * Memberikan jasa asuransi pada barang
