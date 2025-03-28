![image](https://github.com/user-attachments/assets/b026fc50-6bfb-438d-b818-53eeec44748d)# Pemeliharaan Basis Data dan Penggunaan Index

## Latar Belakang
Dalam pengelolaan basis data, performa menjadi aspek yang sangat penting. Seiring bertambahnya jumlah data dalam tabel, pencarian dan manipulasi data dapat menjadi lambat jika tidak dikelola dengan baik. Salah satu cara untuk meningkatkan performa basis data adalah dengan menggunakan indeks.

## Problem yang Diangkat
1. Bagaimana cara mengimpor data ke dalam MySQL?
2. Apa manfaat penggunaan indeks dalam basis data?
3. Bagaimana cara menambahkan berbagai jenis indeks di MySQL?
4. Bagaimana cara menguji efektivitas indeks dalam mempercepat query?

## Skenario Aktivitas
1. Pertama Create database dengan script
   CREATE DATABASE employee_db;
   USE employee_db;
   
   ![image](https://github.com/user-attachments/assets/987f64ce-6934-4f89-85b7-6c3abc80eab8)
   Setelah itu lakukan import data dengan sript berikut
   SOURCE employee.sql;
   ![image](https://github.com/user-attachments/assets/e5acb7bd-ea59-4ff6-b20d-12e180794c0b)
   Tunggu sampai proses selesai. Kalau sukses, nanti muncul pesan seperti "Query OK" dan tabel akan terbuat di database. Setelah selesai, maka pada database, akan tampak sebagai berikut:
   ![image](https://github.com/user-attachments/assets/98fbcfde-f688-4c5f-b33a-87f1118da2d8)
   ![image](https://github.com/user-attachments/assets/19be4be5-0071-45ef-80e4-8ee46316b224)
2. Jalankan script
   SELECT * FROM employee
   ![image](https://github.com/user-attachments/assets/cafb2d60-0942-45ad-b47d-c7af14c661c5)
   Jalankan query explain
   EXPLAIN SELECT * FROM employee
   WHERE first_name = 'Georgi'
   ![image](https://github.com/user-attachments/assets/76973070-353a-4a32-9a7d-ebeb706316bb)
   Tambahkan index dengan script
   ALTER TABLE employee ADD INDEX idx_full_name (first_name, last_name)
   ![image](https://github.com/user-attachments/assets/c6343aa5-c7c9-4832-90b5-845064d1cef4)
   Lakukan query explain lagi untuk query diatas
   EXPLAIN SELECT * FROM employee
   WHERE first_name = 'Georgi'
   AND last_name = 'Bahr'

   ![image](https://github.com/user-attachments/assets/443459ab-86c1-4077-bb90-745df12730f6)
   Sekarang bisa kita lihat bahwa query yang kita jalankan tidak lagi scaning penuh ke tabel melainkan akses pada index. Ini terlihat pada nilai kolom key dan possible_keys.
   ![image](https://github.com/user-attachments/assets/e2db5b2a-2e11-45fb-ace1-bce177122dc7)

**Latihan Soal**
1. Tambahkan kolom nama departemen pada table dept_manager. Dan lakukan update terhadap kolom tersebut.
   ALTER TABLE dept_manager ADD COLUMN nama_departemen VARCHAR(100);
   ![image](https://github.com/user-attachments/assets/b3128202-9e38-4e9b-b32f-5f19d61666f1)
   Update Data di Kolom nama_departemen, berdasarkan dept_no yang sudah ada
   ![image](https://github.com/user-attachments/assets/2d582b4c-04f1-4a73-b8e5-8be9bfd07635)
   Lalu cek hasilnya update menggunakan query
   SELECT * FROM dept_manager LIMIT 10;
   ![image](https://github.com/user-attachments/assets/a189b408-7821-44aa-81be-eca405e0ceee)
2. Tambahkan kolom nama departemen pada table dept_emp. Dan lakukan update terhadap kolom tersebut. Tambahkan screenshot hasilnya
   ALTER TABLE dept_emp ADD COLUMN dept_name VARCHAR(100);
   ![image](https://github.com/user-attachments/assets/f16812f6-e459-4e8c-bee9-e00cc191f790)
   Update Data di Kolom nama_departemen, berdasarkan dept_no yang sudah ada
   ![image](https://github.com/user-attachments/assets/c1ebf69d-6bd0-4874-a206-d13f5b1716fe)
   Lalu cek hasilnya update menggunakan query
   SELECT * FROM dept_emp;
   ![image](https://github.com/user-attachments/assets/b22d0434-5e5a-4cb3-bcd5-7350b9db68c2)
3. Buat query untuk menampilkan gaji yang tertinggi pada departemen d006. Siapa Namanya?
   ![image](https://github.com/user-attachments/assets/b1167a70-d698-469c-b7eb-b9bf73c75635)
   Penggunaan alias dalam query bertujuan untuk menghindari kebingungan antara subquery dan query utama. s2.amount digunakan dalam subquery untuk membedakan dengan s.amount di query utama, sementara d2.dept_no membantu memperjelas referensi tabel dept_emp.
4. Tambahkan kolom umur pada tabel employee, kemudian lakukan updateterhadap komom tersebut.
   Nilai umur dihitung dari tanggal lahir sampai dengan sekarang
   ![image](https://github.com/user-attachments/assets/b8ca2b49-03fb-4d6d-aff3-f3b8b0a93899)
   Lalu update kolom dengan ketentuan isian umur sesuai dengan tanggal lahir sampai sekarang
   ![image](https://github.com/user-attachments/assets/b260e282-0e93-476c-87dc-ed73f4271e59)
   Lalu cek hasilnya update menggunakan query
   ![image](https://github.com/user-attachments/assets/c8bd8eff-a2e0-4238-9bd7-ecc578bd62b3)
5. Tambahkan masing-masing jenis index diatas composite index dan foreign key index pada table employee
   - Composite index digunakan untuk meningkatkan kinerja query yang sering menggunakan lebih dari satu kolom dalam kondisi pencarian (WHERE, ORDER BY). Contoh, jika kita sering mencari berdasarkan first_name dan last_name
     ![image](https://github.com/user-attachments/assets/28ac3cb2-6e6b-4d01-81ab-bec5e4413b3b)
     Penjelasan singkat
     1. idx_name adalah nama index.
     2. first_name, last_name adalah kolom yang digunakan dalam index.
     3. Query seperti WHERE first_name = 'John' AND last_name = 'Doe' akan lebih cepat
   - Tambahkan Foreign Key Index
     ![image](https://github.com/user-attachments/assets/dd5a0f39-a5af-4330-8a55-f0b33e787075)
     1.	fk_emp adalah nama foreign key.
     2.	emp_no di dept_emp mengacu ke emp_no di employee.
     3.	ON DELETE CASCADE memastikan jika data di employee dihapus, data terkait di dept_emp juga ikut terhapus.
6. Lakukan pengujian terhadap query berikut, apakah sudah mengakses index atau belum
   ![image](https://github.com/user-attachments/assets/057eb06e-8d34-40eb-ad1c-78f47dcec80b)
7. Lakukan pengujian dari query berikut. Apakah ada perbedaan sebelum dan sesudah ditambahkan index
   ![image](https://github.com/user-attachments/assets/8a492181-2a47-4812-a31e-0c9c32f03342)
   Hasil pengujian
   
   ![image](https://github.com/user-attachments/assets/7f7e3700-0b4a-4f13-a809-2dd2c0c9d623)

    Karena sebelumnya kita telah menambahkan index terlebih dahulu, sekarang hapus index untuk pengujian dengan langkah sebagai berikut
   - Hapus Composite Index - Jika kita sebelumnya membuat index bernama idx_name di kolom first_name dan last_name, hapus dengan
     ALTER TABLE employee DROP INDEX idx_name;
   - Hapus Foreign Key Index - Jika kita menambahkan foreign key bernama fk_emp di tabel dept_emp, hapus dengan
   - ALTER TABLE dept_emp DROP FOREIGN KEY fk_emp;
     
    Berikut adalah hasil dari penghapusan composite dan fk index
    ![image](https://github.com/user-attachments/assets/77b7ba10-c865-4647-941a-12d64a0561e2)
    Setelah selesai menghapus index kita cek dahulu jika index sudah benar benar hilang
    ![image](https://github.com/user-attachments/assets/51d7b1b5-eaed-49aa-a662-78341e33b0af)
    Setelah dilakukan pengujian di hapus indexnya
   
    ![image](https://github.com/user-attachments/assets/92533d52-d9e1-404c-9713-185711fd431d)

## Kesimpulan
1. Penggunaan indeks sangat efektif dalam mempercepat proses pencarian data dalam tabel besar.
2. Penggunaan EXPLAIN membantu dalam analisis dan optimasi query.
3. Pengujian sebelum dan sesudah penambahan indeks menunjukkan adanya peningkatan performa.
4. Pemeliharaan indeks diperlukan untuk menghindari overhead penyimpanan dan pembaruan indeks yang dapat memperlambat operasi penulisan data.

## Sumber Referensi
1. Dokumentasi MySQL: https://dev.mysql.com/doc/
2. Artikel tentang indeks MySQL: https://www.mysqltutorial.org/mysql-indexes.aspx
