---
title: 'Tutorial Dasar Form GET dan POST dalam PHP'
description: 'Tutorial Dasar Form GET dan POST Untuk Kamu Yang Ingin Mengetahui Proses Input Data Pada PHP'
pubDate: '2023-11-04T13:21:15.031Z'
heroImage: '/blog-placeholder.jpg'
categories: ['Tutorial PHP']
authors: ['Arya Dwi Putra']
tags: ['php', 'basic', 'web', 'programming', 'beginner']
---

Form adalah salah satu elemen penting dalam pengembangan web yang memungkinkan pengguna untuk berinteraksi dengan situs web Anda. Dalam PHP, Anda dapat mengambil data yang dikirim melalui formulir menggunakan dua metode utama: GET dan POST. Artikel ini akan membahas kedua metode tersebut dan memberikan panduan langkah demi langkah dalam penggunaannya.

## Metode GET

Metode GET digunakan untuk mengambil data dari URL. Data yang dikirim melalui metode GET akan terlihat pada URL, sehingga metode ini cocok untuk mengambil data yang tidak sensitif seperti parameter pencarian atau filter. Berikut langkah-langkah untuk membuat dan memproses formulir GET:

### 1. Membuat Form HTML

Buat formulir HTML dengan tag `<form>` dan setel atribut `method` ke "get". Contoh:

```html
<form method="get" action="proses_get.php">
  <label for="nama">Nama:</label>
  <input type="text" name="nama" id="nama" />
  <input type="submit" value="Kirim" />
</form>
```

### 2. Memproses Data GET

Buat file PHP yang akan memproses data yang dikirim melalui formulir GET, dalam contoh ini disebut "proses_get.php". Gunakan `$_GET` untuk mengakses data yang dikirim dari formulir:

```php
<?php
if (isset($_GET['nama'])) {
  $nama = $_GET['nama'];
  echo "Halo, $nama!";
}
?>
```

Data yang dikirim melalui formulir GET akan muncul pada URL sebagai query string, contoh: `proses_get.php?nama=John`.

## Metode POST

Metode POST digunakan untuk mengirim data yang tidak terlihat pada URL, sehingga lebih aman untuk data sensitif seperti kata sandi. Berikut langkah-langkahnya:

### 1. Membuat Form HTML

Buat formulir HTML dengan tag `<form>` dan setel atribut `method` ke "post". Contoh:

```html
<form method="post" action="proses_post.php">
  <label for="katasandi">Kata Sandi:</label>
  <input type="password" name="katasandi" id="katasandi" />
  <input type="submit" value="Kirim" />
</form>
```

### 2. Memproses Data POST

Buat file PHP yang akan memproses data yang dikirim melalui formulir POST, dalam contoh ini disebut "proses_post.php". Gunakan `$_POST` untuk mengakses data yang dikirim dari formulir:

```php
<?php
if (isset($_POST['katasandi'])) {
  $katasandi = $_POST['katasandi'];
  echo "Kata Sandi yang Anda masukkan: $katasandi";
}
?>
```

Data yang dikirim melalui formulir POST tidak akan muncul pada URL dan lebih aman.

## Kesimpulan

Dengan mengikuti tutorial ini, Anda sekarang memiliki pemahaman dasar tentang penggunaan formulir dengan metode GET dan POST dalam PHP. Anda dapat memanfaatkan informasi ini untuk mengembangkan situs web yang memungkinkan pengguna berinteraksi dan mengirim data ke server dengan aman.
