# Lab8Web
# Pratikum 8
# Pemograman Web
~~~
Nama  : Endrik
NIM   : 311910088
Kelas : TI.19.C1
~~~
## Langkah-langkah Praktikum
Persiapan
Untuk memulai membuat aplikasi CRUD sederhana, yang perlu disiapkan adalah database server menggunakan MySQL. Pastikan MySQL Server sudah dapat dijalankan melalui XAMPP.

## Menjalankan MySQL Server
Untuk menjalankan MySQL Server dari menu XAMPP Contol.
![1b](https://user-images.githubusercontent.com/81820421/121042635-1392ff80-c7de-11eb-9ecd-61183b16b9a9.JPG)

## Mengakses MySQL Client menggunakan PHP MyAdmin
Pastikan webserver Apache dan MySQL server sudah dijalankan. Kemudian buka melalui browser: http://localhost/phpmyadmin/

## Membuat Database: Studi Kasus Data Barang
![1a](https://user-images.githubusercontent.com/81820421/121042013-7b951600-c7dd-11eb-9c21-40b585061897.jpg)
## Membuat Database
~~~
CREATE DATABASE latihan1;
~~~
![1c](https://user-images.githubusercontent.com/81820421/121042939-610f6c80-c7de-11eb-9804-33e5a5802f1f.JPG)
## Membuat Tabel
~~~
CREATE TABLE data_barang (
  id_barang int(10) auto_increment Primary Key,
  kategori varchar(30),
  nama varchar(30),
  gambar varchar(100),
  harga_beli decimal(10,0),
  harga_jual decimal(10,0),
  stok int(4)
);
~~~
![1d](https://user-images.githubusercontent.com/81820421/121043425-cebb9880-c7de-11eb-99cd-f31e6d5e5023.JPG)

## Menambahkan Data 
~~~INSERT INTO data_barang (kategori, nama, gambar, harga_beli, harga_jual, stok) VALUES ('Motor', 'Honda beat',
'motorbeat.jpg', 15000000, 24000000, 5), ('Mobil', 'Ertiga', 'ertiga.jpg', 100000000, 140000000, 5),
('Sepeda', 'Pixel', 'pixel.jpg', 5000000, 7000000, 5);
~~~
![1e](https://user-images.githubusercontent.com/81820421/121047467-72f20f00-c7e0-11eb-8cfb-48d15a24f06d.JPG)

## Membuat Program CRUD
Buat folder lab8_php_database pada root directory web server (d:\xampp\htdocs)
![1f](https://user-images.githubusercontent.com/81820421/121048522-180ce780-c7e1-11eb-8716-440f4629702f.JPG)

Kemudian untuk mengakses direktory tersebut pada web server dengan mengakses URL: http://localhost/lab8_php_database/
![1g](https://user-images.githubusercontent.com/81820421/121048930-75089d80-c7e1-11eb-9706-149aad313747.JPG)

## Membuat file koneksi database
Buka visual code
Buat file baru dengan nama koneksi.php
~~~
<?php
    $host = "localhost";
    $user = "root";
    $pass = "";
    $db = "latihan1";

    $conn = mysqli_connect($host, $user, $pass, $db);
    if ($conn == false)
    {
        echo "Koneksi ke server gagal.";
        die();
    } #else echo "Koneksi berhasil";
?>
~~~
Buka melalui browser untuk menguji koneksi database (untuk menyampilkan pesan koneksi berhasil, uncomment pada perintah echo “koneksi berhasil”;

![1bb](https://user-images.githubusercontent.com/81820421/121051570-c023b000-c7e3-11eb-87c4-db83ec374847.JPG)
## Membuat file index untuk menampilkan data (Read)
Buat file baru dengan nama index.php
~~~
<?php
include("koneksi.php");

// query untuk menampilkan data
$sql = 'SELECT * FROM data_barang';
$result = mysqli_query($conn, $sql);

?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link href="style.css" rel="stylesheet" type="text/css" />
    <title>Data Barang</title>
</head>
<body>
    <div class="container">
        <h1>Data Barang</h1>
        <div class="main">
            <table>
            <tr>
                <th>Gambar</th>
                <th>Nama Barang</th>
                <th>Katagori</th>
                <th>Harga Jual</th>
                <th>Harga Beli</th>
                <th>Stok</th>
                <th>Aksi</th>
            </tr>
            <?php if($result): ?>
            <?php while($row = mysqli_fetch_array($result)): ?>
            <tr>
                <td><img src="gambar/<?= $row['gambar'];?>" alt="<?=
$row['nama'];?>"></td>
                <td><?= $row['nama'];?></td>
                <td><?= $row['kategori'];?></td>
                <td><?= $row['harga_beli'];?></td>
                <td><?= $row['harga_jual'];?></td>
                <td><?= $row['stok'];?></td>
                <td><?= $row['id_barang'];?></td>
            </tr>
            <?php endwhile; else: ?>
            <tr>
                <td colspan="7">Belum ada data</td>
            </tr>
            <?php endif; ?>
            </table>
        </div>
    </div>
</body>
</html>
~~~




