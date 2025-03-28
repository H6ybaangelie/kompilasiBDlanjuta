# Instalasi dan Konfigurasi Server Database

## Latar Belakang
Dalam dunia pengolahan data, pemahaman akan database relational dan unrelational sangat penting untuk menentukan solusi terbaik dalam penyimpanan dan pengelolaan data. selain itu, penguasaan instalasi serta konfiguasi server database menjadi kompetensi dasar yang harus dimiliki. Oleh karena itu, pada praktikum ini bertujuan untuk memahami perbedaan antar database relational dan unrelational, serta mengimplementasikan instalasi dan konfigurasi server database MySQL.

## Masalah yang diangkat
1. Bagaimana perbedaan antara database relational dan database unrelational?
2. Kapan harus menggunakan database relational dan kapan harus menggunakan database unrelational?
3. Bagaimana cara melakukan instalasi MySQL dengan benar?
4. Bagaimana cara melakukan perubahan konfigurasi server database MySQL?
5. Bagaimana cara membuat database menggunakan command prompt?

## Skenario Aktivitas
1. Pilih versi MySQL Installer (full): Ini adalah versi lengkap yang sudah mencakup semua komponen.
   ![image](https://github.com/user-attachments/assets/80cdcf92-404c-48e4-a072-329ed01c3bf5)
2. Setelah download selesai, buka file installer dan akan diminta untuk memilih tipe instalasi, klik saja server only (hanya menginstall server MySQL)
   ![image](https://github.com/user-attachments/assets/9cbce0b6-bc2f-4474-b9fe-82a3850212dc)
3. Selanjutnya klik lingkaran mirah dan klik ”Execute”, tunggu sebentar sampai 100% dan akan berubah menjadi ”Next”. Lalu klik ”Next” dan tunggu instalasi selesai
   ![image](https://github.com/user-attachments/assets/c68e9071-dd51-477a-a3a2-0c011a047894)
4. Pada layar Type and Networking, biarkan pengaturan default dan klik Next.
   ![image](https://github.com/user-attachments/assets/c9c502d0-0ea7-44dd-9934-8520c0d8bb11)
6. Pada layer Authentication Method pilih Use Strong Password Encryption for Authentication (RECOMMENDED).
   ![image](https://github.com/user-attachments/assets/ed6936aa-5c0d-47ea-9289-26ea85f3b7f3)
7. ada layar Accounts and Roles, masukkan password untuk akar (disini “root”) MySQL. Pastikan anda mengingat password ini karena akan diperlukan untuk mengakses database.
   ![image](https://github.com/user-attachments/assets/5b181795-3041-46af-aa29-e19bd2b648df)
8. Pada layar Windows Service, biarkan pengaturan default dan klik Next.
   ![image](https://github.com/user-attachments/assets/cc1d6f28-534f-4005-9255-3709f4872e18)
   ![image](https://github.com/user-attachments/assets/0d9e8e6d-eaaf-4ed7-ac2a-0958703272ce)
   Selanjutnya Pilih ‘Execute’ dan tunggu
   ![image](https://github.com/user-attachments/assets/deafb67f-aedc-4481-94e5-e48467a10829)
9. Setelah konfigurasi selesai, Anda akan dibawa ke layar Product Configuration. Klik Next. 
   ![image](https://github.com/user-attachments/assets/bd630e8b-0d7a-4888-87e3-9df8ae55ba86)
10. Pada layar Installation Complete, Anda akan melihat ringkasan dari instalasi yang telah dilakukan. Klik finish untuk menyelesaikan instalasi.
   ![image](https://github.com/user-attachments/assets/6282bfb4-8c9f-427d-b9f9-c7b3ce208dfc)

**Konfigurasi**

1. Mencoba masuk ke mysql pertama kali menggunakan user root paswoord yang tadi di set.
   ![image](https://github.com/user-attachments/assets/6cfad8ec-92da-44f7-b100-78734a1dfbbb)
2. Win+R ketik "%PROGRAMDATA%", lalu enter. Lalu ke “MySQL\MySQL Server 8.0\”  lalu buka file  “my.ini”  mengguna text editor.
   ![image](https://github.com/user-attachments/assets/02647b27-3030-42a6-938f-ac57569c8a69)
3. Ganti port 3306 ke port 3309.

   ![image](https://github.com/user-attachments/assets/072abdbf-70ad-4d54-9cc5-068b06fd5405)

   ![image](https://github.com/user-attachments/assets/f0ca854a-9f0b-4ee5-9da0-4420c029537d)
5. Ubah menjadi 25% dari jumlah ram.

   ![image](https://github.com/user-attachments/assets/a9621bfd-6b41-43c4-a552-dad42db7aa7d)
7. Restart server mysql.
   ![image](https://github.com/user-attachments/assets/e11b9c64-69ea-42ee-9781-8a6db508bd8b)
8. Masuk ke mysql dengan port yang baru 3309.
   ![image](https://github.com/user-attachments/assets/a5a7e4e0-31b1-4c63-b0f3-3de13c488b4c)
9. Check port terbaru.

   ![image](https://github.com/user-attachments/assets/9b9268f4-8ae2-4759-8877-042935eec89e)
11. Check innodb_buffer_pool_size baru.
   ![image](https://github.com/user-attachments/assets/63d0d299-401b-428d-8c8e-69075dac8939)
12. Buat database baru, (kelompok_1).
   ![image](https://github.com/user-attachments/assets/fcf02738-2659-45c0-8235-1cc7e1a5ec80)

## Pembahasan
Selama praktikum, proses instalasi berjalan sesuai langkah yang telah ditentuka. Perubahan konfurasi berhasil dilakukan dan terverifikasi. Dengan memahami database relational dan unrelational, kita  dapat menentukan jenis database yang paling sesuai untuk kebutuhan aplikasi atau server tertentu.

## Kesimpulan
1. Database relational cocok untuk aplikasi dengan data terstruktur dan transaksi kompleks.
2. Database unrelational lebih efisien untuk data besar yang tidak memiliki struktur tetap.
3. Instalasi MySQL harus dilakukan dengan langkah yang benar agar server dapat berjalan optimal.
4. Konfigurasi MySQL dapat disesuaikan sesuai kebutuhan sistem.

## Sumber Referensi
1. Oracle Corporation. (2021). MySQL Documentation. Retrieved from https://dev.mysql.com/doc/
2. MongoDB Inc. (2021). MongoDB Documentation. Retrieved from https://www.mongodb.com/docs/
3. PostgreSQL Global Development Group. (2021). PostgreSQL Documentation. Retrieved from https://www.postgresql.org/docs/





