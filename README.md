# Studi Kasus Subquery SQL

Proyek ini berisi contoh penggunaan subquery dalam SQL untuk menyelesaikan berbagai kasus yang sering ditemui dalam pengolahan data karyawan di sebuah perusahaan. File ini menjelaskan cara membuat database, tabel, mengisi data contoh, dan menjalankan perintah SQL untuk menyelesaikan soal-soal yang diberikan.

## 1. Membuat Database

Untuk memulai, buat database `perusahaan` dan gunakan database tersebut:
```
sql
CREATE DATABASE perusahaan;
USE perusahaan;
```
Buat tabel karyawan, departemen, dan tempat_kerja dengan struktur 
```
CREATE TABLE karyawan (
    nik INT PRIMARY KEY,
    nama VARCHAR(100),
    gaji_pokok DECIMAL(15,2),
    id_dept INT,
    sup_nik INT,
    FOREIGN KEY (sup_nik) REFERENCES karyawan(nik)
);
```
TABLE DEPARTEMEN
```
CREATE TABLE departemen (
    id_dept INT PRIMARY KEY,
    nama_dept VARCHAR(100),
    id_p INT
);
```
Tabel tempat_kerja
```
CREATE TABLE tempat_kerja (
    id_p INT PRIMARY KEY,
    nama VARCHAR(100)
);
```
Data untuk Tabel tempat_kerja
```
INSERT INTO tempat_kerja (id_p, nama) VALUES
(1, 'Kantor Pusat'),
(2, 'Kantor Cabang A'),
(3, 'Kantor Cabang B');
```
Data untuk Tabel departemen
```
INSERT INTO departemen (id_dept, nama_dept, id_p) VALUES
(1, 'Departemen IT', 1),
(2, 'Departemen HRD', 2),
(3, 'Departemen Keuangan', 3);
```
Data untuk Tabel karyawan
```
INSERT INTO karyawan (nik, nama, gaji_pokok, id_dept, sup_nik) VALUES
(101, 'Riko', 5000000, 1, NULL),
(102, 'Ari', 6000000, 2, NULL),
(103, 'Dika', 5500000, 1, 101),
(104, 'Budi', 4500000, 3, 102),
(105, 'Sari', 7000000, 2, 102),
(106, 'Lina', 5200000, 1, 103);
```
## Latihan
Tampilkan data karyawan yang bekerja pada departemen yang sama dengan karyawan yang bernama Dika
```
SELECT nik, nama
FROM karyawan
WHERE id_dept = (
    SELECT id_dept 
    FROM karyawan
    WHERE nama = 'Dika'
);
```
Tampilkan data karyawan yang gajinya lebih besar dari rata-rata gaji semua karyawan, urutkan menurun berdasarkan besaran gaji:
```
SELECT nik, nama, gaji_pokok
FROM karyawan
WHERE gaji_pokok > (
    SELECT AVG(gaji_pokok) 
    FROM karyawan
)
ORDER BY gaji_pokok DESC;
```
Tampilkan nik dan nama karyawan untuk semua karyawan yang bekerja di departemen yang sama dengan karyawan dengan nama yang mengandung huruf 'K':
```
SELECT nik, nama
FROM karyawan
WHERE id_dept IN (
    SELECT id_dept 
    FROM karyawan
    WHERE nama LIKE '%K%'
);
```
Tampilkan data karyawan yang bekerja pada departemen yang ada di kantor pusat:
```
SELECT nik, nama
FROM karyawan
WHERE id_dept IN (
    SELECT id_dept 
    FROM departemen
    WHERE id_p = (
        SELECT id_p 
        FROM tempat_kerja
        WHERE nama = 'Kantor Pusat'
    )
);
```
Tampilkan nik dan nama karyawan untuk semua karyawan yang bekerja di departemen yang sama dengan karyawan dengan nama yang mengandung huruf 'K' dan yang gajinya lebih besar dari rata-rata gaji semua karyawan:
```
SELECT nik, nama
FROM karyawan
WHERE id_dept IN (
    SELECT id_dept 
    FROM karyawan
    WHERE nama LIKE '%K%'
)
AND gaji_pokok > (
    SELECT AVG(gaji_pokok) 
    FROM karyawan
);
```

Dengan mengikuti instruksi di atas, Anda akan dapat membuat database, tabel, dan mengisi data contoh yang diperlukan untuk menjalankan contoh subquery SQL yang disediakan. Pastikan data yang dimasukkan sesuai dengan struktur yang telah ditentukan agar perintah SQL dapat dieksekusi dengan benar.






