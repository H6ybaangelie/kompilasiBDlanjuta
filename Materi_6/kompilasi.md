# Optimasi Bottleneck dalam MySQL

## Latar Belakang
Bottleneck dalam MySQL adalah kondisi di mana kinerja database mengalami penurunan akibat keterbatasan sumber daya atau eksekusi query yang tidak optimal. Beberapa faktor penyebab bottleneck meliputi full table scan, jumlah koneksi yang berlebihan, serta kurangnya indeks pada kolom yang sering digunakan dalam pencarian. Optimasi database diperlukan agar kinerja MySQL tetap efisien dan dapat menangani permintaan dengan cepat.

## Problem yang Diangkat
Beberapa masalah umum yang menyebabkan bottleneck dalam MySQL meliputi:
1. Full table scan akibat tidak adanya indeks yang sesuai.
2. Banyaknya koneksi yang tidak dikelola dengan baik, menyebabkan error "Too many connections".
3. Deadlock akibat transaksi yang berjalan bersamaan.
4. Ukuran buffer pool yang kecil, sehingga sering membaca dari disk.
5. Penggunaan SELECT * yang tidak efisien.

## Skenario Aktivitas
1. Menambahkan Indeks untuk Menghindari Full Table Scan:
   Full table scan terjadi jika MySQL membaca seluruh tabel untuk menemukan hasil query. Kita akan menambahkan indeks pada kolom yang sering digunakan dalam WHERE, JOIN, ORDER BY, atau GROUP BY.
   - Menambahkan Indeks Tunggal
     ![image](https://github.com/user-attachments/assets/eb40bd3e-3a1b-473b-8ff3-7781574a59b6)
     Indeks ini mempercepat pencarian data berdasarkan tanggal transaksi, kode cabang, kode kasir, dan kode produk. 
   - Mengevaluasi Efektivitas Indeks
     ![image](https://github.com/user-attachments/assets/4e41846a-ff6d-488f-a5fa-a40bae3f9082)
     Kesimpulannya
     1. Menambahkan index untuk mempercepat pencarian
     2. Menggunakan Prepared Statements untuk query berulang
     3. Meningkatkan caching dengan InnoDB Buffer Pool
     4. Mengecek efektivitas dengan EXPLAIN
   - Script insert utk tahun 2009
     ![image](https://github.com/user-attachments/assets/6a70c4cb-f9b0-4a31-9d2e-e421b50de7b1)
2. Query berikut apakah sudah optimal?? Jika belum, lakukan optimasi.
   
   **Before**
   ![image](https://github.com/user-attachments/assets/f46bb615-f2a3-4d43-b1c7-9a15e1e70d37)
   **After**
   ![image](https://github.com/user-attachments/assets/38cae69d-f741-41c3-abc3-7536f8c6fc21)

   Penjelasan
   - Menghapus SELECT *
     Menggunakan hanya kolom yang diperlukan (kode_cabang, jumlah_pembelian, harga)
     Mengurangi beban jaringan dan pemrosesan data
   - Menggunakan GROUP BY kode_caban
     Mengelompokkan data berdasarkan kode_cabang, sehingga dapat melihat total penjualan dan pendapatan per cabang.
   - Menggunakan SUM(jumlah_pembelian) dan SUM(harga)
     Melakukan agregasi langsung dalam query untuk menghindari pengolahan data tambahan di aplikasi.
3. Query berikut apakah sudah optimal?? Jika belum, lakukan optimasi
   
   **Before**
   ![image](https://github.com/user-attachments/assets/d2ded481-8f82-4166-a295-039b4ef33c98)
   **After**
   ![image](https://github.com/user-attachments/assets/8cf48da3-e151-4c92-97ad-d4274974c1b4)

   Kesimpulan, Hasil optimasi Query lebih cepat, lebih ringan, dan lebih efisien dalam menghitung total penjualan berdasarkan kode item.
   -	Query awal kurang optimal karena mengambil semua kolom (`SELECT *`), tidak menggunakan agregasi, dan berpotensi melakukan full table scan, yang memperlambat eksekusi.
   -	Query optimal lebih efisien karena hanya mengambil kolom yang dibutuhkan (`kode_item` dan total penjualan), menggunakan agregasi (`SUM()`), serta mengelompokkan data dengan `GROUP BY`.
   -	Penggunaan indeks pada `kode_item` dapat meningkatkan performa dengan mempercepat proses pencarian data dan menghindari pemindaian seluruh tabel.
4. Query berikut apakah sudah optimal?? Jika belum, lakukan optimasi
   
   **Before**
   ![image](https://github.com/user-attachments/assets/abf7edc9-6db2-497c-b5c4-df6c3c49f3c7)
   **After**
   ![image](https://github.com/user-attachments/assets/fda472ab-17d9-4433-8729-40bc1dbada3f)

   Kesimpulan, Hasil optimasi Query lebih cepat, lebih ringan, dan lebih efisien dalam menghitung total penjualan berdasarkan kode item.
   -	Query awal kurang optimal karena menggunakan SELECT *, yang mengambil seluruh kolom tabel meskipun tidak semuanya diperlukan. Selain itu, penggunaan LIKE '%Galang%' tanpa indeks akan menyebabkan full table scan, yang memperlambat pencarian data.
   -	Query optimal lebih efisien karena:
         1. Menggunakan COUNT(*) untuk menghitung jumlah transaksi per kasir.
         2. Menggunakan SUM(harga) untuk menghitung total pendapatan per kasir.
         3. Menyusun hasil dengan GROUP BY nama_kasir, yang membantu dalam menganalisis data berdasarkan nama kasir.
   -	Hasil optimasi: Query lebih cepat, lebih spesifik, dan lebih ringan dalam pemrosesan data.
4. Diberikan query berikut. Pada kolom harga belum ada index. Apakah query berikut sudah optimal?? Jelaskan langkah2 optimasinya.
   - Pertama tama Drop index terlebih dahulu
     ![image](https://github.com/user-attachments/assets/e0357866-51e6-4885-a8fb-86101a19ab36)
   - Lalu tambahkan index terlebih dahulu
     CREATE INDEX idx_kode_cabang ON tr_penjualan_raw(kode_cabang);
     ![image](https://github.com/user-attachments/assets/d64ff38c-e3c1-4012-a6b2-2d8970d269d2)
   
## Kesimpulan
Optimasi MySQL sangat penting untuk meningkatkan kinerja database dan menghindari bottleneck. Dengan menambahkan indeks, meningkatkan buffer pool, menggunakan query cache, serta menghindari SELECT *, performa database dapat meningkat secara signifikan.
