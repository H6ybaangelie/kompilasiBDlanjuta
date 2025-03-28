# Manajemen User, Role, dan Privilege di MySQL

## Latar Belakang
Manajemen pengguna, hak akses, dan monitoring aktivitas dalam database merupakan aspek penting dalam administrasi basis data. Dengan mengelola pengguna dan hak aksesnya dengan baik, keamanan serta integritas data dapat terjaga. Selain itu, pemanfaatan role dalam MySQL (khususnya sejak versi 8.0) memungkinkan pengelolaan hak akses yang lebih efisien.

## Problem yang Diangkat
1. Bagaimana cara membuat dan menghapus user dalam MySQL?
2. Bagaimana cara mengelola hak akses atau privilege pengguna?
3. Bagaimana cara menggunakan role untuk mempermudah manajemen hak akses?
4. Bagaimana cara melakukan monitoring aktivitas pengguna dalam MySQL?

## Skenario Aktivitas
1. Membuat user sesuai jumlah anggota kelompok dengan script CREATE USER ‘username’@’localhost’ IDENTIFIED BY ‘password’;
   ![image](https://github.com/user-attachments/assets/62096dcc-faa0-48e2-a67e-a9c2302ff61c)
   Dari script ini kita telah membut 3 user dengan nama Hayba, Kevin dan Joy. User ini hanya bisa login dari localhost, artinya user tidak bisa diakses dari computer lain.
   ![image](https://github.com/user-attachments/assets/a37f255a-7efb-4ffd-b63c-df321bdcc871)
   Script ini akan mengambil informasi dari tabel user dalam database mysql, yang menyimpan semua akun pengguna MySQL. Dan hasilnya menampilkan daftar user MySQL yang sudah ada di dalam sisten
   ![image](https://github.com/user-attachments/assets/e20cda05-287f-45a2-89f5-fb8a1ebc8d5f)
2. Menghapus username terhadap user yang sudah dibuat, dengan script
   ![image](https://github.com/user-attachments/assets/8ba70908-d331-44b9-b7e7-485df32b1700)
   Script ini digunakan untuk menghapus user ‘Kevin’ dari MySQL. Setelah user dihapus maka user tersebut tidak bisa login atau mengakses database mySQL.
   ![image](https://github.com/user-attachments/assets/3b4e9348-44c4-4895-b379-5d8f0f6156f4)
   Pada scrip ini, digunakan untuk mengambil data dari tabel user dalam database MySQL dan menampilkan daftar user yang masih ada di MySQL setelah penghapusan dilakukan.
   Berikut adalah hasil eksekusi dari script diatas,
   ![image](https://github.com/user-attachments/assets/4f4c4d9d-4c23-41f7-804c-08b880bd6367)
3. Membuat role untuk memudahkan manajemen hak akses, dengan script
   CREATE ROLE ‘role_nama_anda_insert_select”
   ![image](https://github.com/user-attachments/assets/e615257e-291e-40dd-96cd-e2e99c41ffb0)
   Script ini digunakan untuk membuat role baru di MySQL, role sendiri yaitu kumpulan hak akses yang bisa diberikan ke user tertentu. Berikut hasil eksekuis dari script diatas
   ![image](https://github.com/user-attachments/assets/c5de394a-c491-49b3-8892-53edda375ff2)
4. Memberikan privilege select dan insert kedalam role yang sudah dibuat. Sebelum dapat menjalankan privilege select dan insert, langkah pertama yang harus dilakukan adalah membuat tabel pada database kelompok 1 yang sudah dibuat di pertemuan kedua. Berikut adalah script untuk membuat database dan tabelnya.
   ![image](https://github.com/user-attachments/assets/dd5cfbb9-c2fe-4d00-b28e-499f598d7bb6)
   ![image](https://github.com/user-attachments/assets/26af1b36-6026-416c-bb1c-6e386d15a418)
   Kemudian tuliskan script yang akan digunakan untuk memberikan privilege select, insert kepada role user dengan menggunakan script
   GRANT SELECT, INSERT ON namadatabase.* TO ‘role_nama_anda_insert_select’
   ![image](https://github.com/user-attachments/assets/88b647c9-172b-422b-9a86-8c2919ed9c65)
   Hasil dari script tersebut dapat dilihat sebagai berikut, yang artinya script yang dijalankan sudah berhasil dieksekusi.
   ![image](https://github.com/user-attachments/assets/30d1a3a7-87c9-4f75-9aa6-a1abe1d6feac)
5. Membuat role dengan script
   CREATE ROLE  ‘role_nama_anda_drop’;
   ![image](https://github.com/user-attachments/assets/c59ef953-58ce-4dcc-829e-80c938cccd22)
   Setelah menjalankan script berikut, sistem akan menampilkan informasi bahwa proses eksekusi telah berhasil dilakukan.
   ![image](https://github.com/user-attachments/assets/8a99bb09-742c-4a8a-a39a-f25829ef59c3)
6. Memberikan privilege create dan drop kedalam role yang telah dibuat sebelumnya dengan menggunakan script
   GRANT CREATE, DROP ON namadatabase.* TO ‘role_nama_anda_creat_drop’;
   ![image](https://github.com/user-attachments/assets/31a95307-2674-4456-8700-4826d49ac33f)
   Setelah menjalankan script berikut, sistem akan menampilkan informasi bahwa proses eksekusi telah berhasil dilakukan.
   ![image](https://github.com/user-attachments/assets/7ccb63b5-b8f3-4286-82cc-237e594ebf28)
7. Memberikan role kepada masing masing user. Pada langkah langkah sebelumnya kita sudah membuat role dengan nama sebagai berikut
   ![image](https://github.com/user-attachments/assets/8f6c113c-f996-475b-a68f-6981df22186b)
---   
   **Script 1:**
   1. Role role_Pardi_select_insert diberikan kepada pengguna Hayba dengan host localhost.
   2. Role role_Pardi_create_drop diberikan kepada pengguna Joy dengan host localhost.
   ![image](https://github.com/user-attachments/assets/1c8269d0-9333-45a1-a767-88ee464b1838)
   ![image](https://github.com/user-attachments/assets/6c892466-0f9e-48a0-8b8e-302065212ac2)
---
  **Script 2:**
   1. Role role_Kevin_select_insert diberikan kepada pengguna Hayba dengan host localhost.
   2. Role role_Kevin_create_drop diberikan kepada pengguna Joy dengan host localhost.
   ![image](https://github.com/user-attachments/assets/eccf1777-042f-4f81-8188-b8ea356ddaad)
   ![image](https://github.com/user-attachments/assets/b2b4e145-9702-4e58-8c2a-3a4940d2b295)
---
8. Melakukan pengujian sebelum dan sesudah user diberikan role.
   ![image](https://github.com/user-attachments/assets/f845238a-1166-437b-83c5-02a900f06e26)
   ![image](https://github.com/user-attachments/assets/a7a8cbc6-a1c2-4873-a912-8e32efbcc221)
   Perbedaan sebelum dan sesudah pemberian role adalah: GRANT USAGE hanya memberikan akses dasar tanpa izin khusus terhadap database. Sementara itu, GRANT 'role_nama_anda_select_insert' atau GRANT 'role_nama_anda_create_drop' memungkinkan user untuk memiliki hak akses tambahan, seperti menjalankan operasi SELECT dan INSERT atau CREATE dan DROP sesuai dengan peran yang diberikan.
9. Melepaskan role dari user diatas, sehingga user menjadi tidak memiliki role.
   ![image](https://github.com/user-attachments/assets/7e9e4de5-5794-47a3-9440-9c0e62d304c6)
   Hasil dari script diatas sebagai berikut,
   ![image](https://github.com/user-attachments/assets/c189e40f-fe6e-4813-ad09-cf64350467df)
---
   1. Perintah 1 mencabut role role_Kevin_select_insert dan role_Pardi_select_insert dari user Hayba.
   2. Setelah eksekusi berhasil, user Hayba tidak lagi memiliki hak akses yang diberikan oleh role tersebut.
   3. Perintah 2 mencabut role role_Kevin_create_drop dan role_Pardi_create_drop dari user Joy.
   4. Setelah eksekusi berhasil, user Joy tidak lagi memiliki hak akses yang diberikan oleh role tersebut.
---
10. Melakukan konfigurasi untuk proses monitoring proses seperti contoh diatas, dan lakukan beberapa kali proses query. Dan menampilkan log serta hasilnya.
    ![image](https://github.com/user-attachments/assets/cdf3d208-b704-44be-b220-898e2b2b7e0a)

    Penjelasan:
      1. SET GLOBAL general_log = 1; → Mengaktifkan general log, sehingga semua query yang dieksekusi akan dicatat oleh MySQL.
      2. SET GLOBAL log_output = 'TABLE'; → Menentukan bahwa log akan disimpan dalam format tabel (bukan file).

    Penjelasan:
      1. SELECT * FROM kelompok_1.table1; → Menampilkan semua data yang ada dalam tabel table1 dari database kelompok_1.
      2. INSERT INTO kelompok_1.table1 (id, nama, usia) VALUES (175, 'Joshe', 19); → Menambahkan data baru dengan ID 175, nama Joshe, dan usia 19 ke dalam tabel table1.

     Penjelasan:
      1. Perintah ini digunakan untuk menampilkan semua query yang telah dieksekusi sejak general log diaktifkan.
      2. Log ini disimpan dalam tabel mysql.general_log, yang mencatat semua perintah SQL yang dilakukan oleh user di server MySQL.
    
    Hasil dari eksekusi script diatas sebagai berikut
    ![image](https://github.com/user-attachments/assets/3b6ffe8c-9b10-4f21-9261-aa1e8ce94d95)
    ![image](https://github.com/user-attachments/assets/262ad37f-bd26-404b-976e-973e3191ff13)

12. Pengelolaan user, role, dan privilege dalam sistem manajemen basis data adalah aspek krusial untuk mengontrol akses pengguna terhadap database. Dalam praktik ini, dilakukan beberapa langkah penting, antara lain:
    1. Membuat user baru menggunakan perintah CREATE USER.
    2. Menghapus user dengan perintah DROP USER.
    3. Membuat role menggunakan CREATE ROLE dan menetapkan hak akses dengan GRANT.
    4. Menguji hak akses sebelum dan sesudah role diberikan kepada user.
    5. Mencabut role dari user menggunakan REVOKE, sehingga user kembali tanpa hak akses tambahan.
    6. Melakukan monitoring aktivitas database dengan mengaktifkan general_log.
    Hasil pengujian menunjukkan bahwa penggunaan role lebih efisien dalam manajemen hak akses dibandingkan memberikan privilege secara individual ke setiap user. Selain itu, pencatatan log aktivitas mempermudah pemantauan terhadap operasi yang berlangsung dalam database, meningkatkan keamanan dan pengawasan sistem.

## Kesimpulan
1. Manajemen pengguna dalam MySQL meliputi pembuatan, penghapusan, serta pengelolaan hak akses.
2. Role mempermudah pengelolaan hak akses dengan memungkinkan penerapan privilege secara kelompok.
3. Monitoring aktivitas pengguna penting untuk menjaga keamanan dan mendeteksi aktivitas mencurigakan.

## Sumber Referensi




