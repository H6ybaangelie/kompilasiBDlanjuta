# Optimasi Database: Partisi Tabel

## Latar Belakang
Dalam pengelolaan basis data yang memiliki volume data besar, performa menjadi salah satu faktor penting dalam memastikan akses dan manipulasi data yang efisien. Salah satu teknik optimasi yang umum digunakan adalah partisi tabel (table partitioning), yang memungkinkan pemecahan tabel besar menjadi bagian yang lebih kecil berdasarkan kriteria tertentu. Dengan adanya partisi tabel, waktu eksekusi query dapat dipersingkat, beban sistem dapat didistribusikan dengan lebih baik, dan manajemen data menjadi lebih mudah.

## Masalah yang Diangkat
Ketika jumlah data dalam sebuah tabel semakin besar, operasi seperti pencarian (SELECT), penyisipan (INSERT), dan penghapusan (DELETE) dapat menjadi lebih lambat karena MySQL harus memproses seluruh tabel. Dalam studi kasus ini, kita akan menguji bagaimana penggunaan partisi tabel dapat meningkatkan performa database dengan membandingkan eksekusi query antara tabel yang terpartisi dan tabel tanpa partisi.

## Skenario Aktivitas
**Latihan Materi**
Import dKita akan membuat partisi berdasarkan wilayah menggunakan List Partition.
Membuat Tabel dengan List Partitionata
Pertama Create database dengan script
![image](https://github.com/user-attachments/assets/986fa49b-75c0-4c51-84fd-34218968c6cf)
Menambahkan Data ke Tabel
![image](https://github.com/user-attachments/assets/9c4c3e81-3768-4ddb-95cc-03de31d9f306)
Mengecek Partisi yang Digunakan
![image](https://github.com/user-attachments/assets/519a24f1-3ce1-4977-841e-7f039fdf4635)
Jalankan query dengan optimasi Partisi
![image](https://github.com/user-attachments/assets/ce262013-46e1-4f5f-9517-93d08dd65403)
Menambahkan Partisi Baru
![image](https://github.com/user-attachments/assets/94d89e0c-6841-456e-8e3f-f5df3ce05827)
Menghapus Partisi Lama
![image](https://github.com/user-attachments/assets/5b31adc2-2fb3-420f-80ce-0ac74f0acf69)
   
**Tugas**
1. Redesaian tabel tr_penjualan, tambahkan partisi pada tabel tersebut. Sehingga ada tabel baru tr_penjualan_partisi
   ![image](https://github.com/user-attachments/assets/90276bb9-69c6-42ba-8bb0-1da0558ee0cb)
   Isikan tabel tr_penjualan_partisi.
   - Insert utk tahun 2008
     ![image](https://github.com/user-attachments/assets/2722798d-0f26-4bc3-ad50-9537c4f8b6db)
   - Script insert utk tahun 2009
     ![image](https://github.com/user-attachments/assets/ab065300-3e1b-4e1e-b64f-33fd89084fca)
   - Script insert utk tahun 2010
     ![image](https://github.com/user-attachments/assets/cad2c8c8-29b2-4752-8056-4f166d807422)
   - Script insert utk tahun 2011
     ![image](https://github.com/user-attachments/assets/793e5d20-1c7b-47e4-bc4e-202748be059a)
   - Script insert utk tahun 2012
     ![image](https://github.com/user-attachments/assets/3f5c0cf6-39f9-45f3-ac45-53897ca4b489)
   - Script insert utk tahun 2013
     ![image](https://github.com/user-attachments/assets/242bde0b-6473-4f55-a651-dd917749e6dc)
   - Script insert utk tahun 2014
     ![image](https://github.com/user-attachments/assets/95a8b01b-1c02-488a-b5f3-afed7a927acc)

   Setelah diisikan, maka susunan record sesuai partisi akan ditampilkan seperti berikut:
   ![image](https://github.com/user-attachments/assets/3df03f11-7c0f-4e3c-a2d0-1a30e85bfbd6)
2. Buat tabel tr_penjualan_raw yang isinya sama persis dengan tabel tr_penjualan_partisi.
   Yang membedakan hanya struktur tabel nya saja
   Tr_penjualan_raw = struktur biasa
   Tr_penjualan_partisi = struktur tabel ter partisi
   ![image](https://github.com/user-attachments/assets/2f557249-30bf-4771-91bf-8ff26b9ae422)
3. Jalankan query berikut dengan perulangan 10x. lakukan pencatatan waktu running setiap query.
   Dan ambil rata-ratanya.
   SELECT * FROM tr_penjualan_partisi
   WHERE tgl_transaksi > DATE('2013-08-01')
   AND tgl_transaksi < DATE('2014-07-31');
   ![image](https://github.com/user-attachments/assets/f2171393-0f43-4529-bfe7-406a6617c5db)

   SELECT * FROM tr_penjualan_raw
   WHERE tgl_transaksi > DATE('2013-08-01')
   AND tgl_transaksi < DATE('2014-07-31');

   ![image](https://github.com/user-attachments/assets/a6fc77ad-3249-442a-a5de-5d650753c100)
   
## Pembahasan
- Setelah melakukan pengujian, hasil yang diperoleh menunjukkan bahwa:
  1. Query pada tabel terpartisi lebih cepat dibandingkan tabel non-partisi, karena MySQL hanya mencari di partisi yang relevan.
  2. Penghapusan data lebih efisien, karena kita dapat menghapus partisi tertentu tanpa harus menghapus seluruh isi tabel.
  3. Manajemen data historis menjadi lebih mudah, terutama dalam skenario backup dan restore.
- Dari percobaan yang telah dilakukan, dapat disimpulkan bahwa:
  1. Partisi tabel sangat efektif dalam meningkatkan performa query jika query menggunakan kolom yang dijadikan dasar partisi.
  2. Manajemen data menjadi lebih fleksibel dengan memungkinkan penghapusan dan penyimpanan data berdasarkan partisi tertentu.
  3. Partisi tidak selalu memberikan keuntungan jika query tidak menggunakan kolom partisi, sehingga perancangan skema partisi harus mempertimbangkan pola akses data yang dominan.
  4. Database dengan jumlah data yang sangat besar lebih mendapatkan manfaat dari partisi dibandingkan database dengan jumlah data kecil.

## Sumber Referensi
1. Hasil percobaan dan pengujian dari tugas yang telah dilakukan.
