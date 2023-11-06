---
title: 'Panduan Lengkap CRUD dengan PHP dan MySQL: Contoh Tabel Buku'
description: 'Tutorial CRUD PHP dengan MySQL : Tabel Buku'
pubDate: '2023-11-05T13:21:15.031Z'
heroImage: '/blog-placeholder.jpg'
categories: ['Tutorial PHP']
authors: ['Arya Dwi Putra']
tags: ['php', 'basic', 'web', 'programming', 'beginner']
---

CRUD (Create, Read, Update, Delete) adalah operasi dasar dalam pengelolaan data di dalam database. Pada artikel ini, kita akan menjelaskan cara melakukan operasi CRUD dengan menggunakan PHP dan MySQL. Sebagai contoh, kita akan fokus pada pengelolaan data buku dalam satu tabel.

## Persiapan

Sebelum kita mulai, pastikan Anda telah menginstal server web (seperti Apache), MySQL, dan PHP di lingkungan pengembangan Anda. Selain itu, pastikan Anda memiliki database MySQL yang telah dibuat. Misalnya, kita akan menggunakan database dengan nama "perpustakaan" dan tabel "buku".

### Struktur Tabel Buku

Tabel "buku" akan memiliki struktur dasar seperti ini:

```sql
CREATE TABLE buku (
  id INT PRIMARY KEY AUTO_INCREMENT,
  judul VARCHAR(255) NOT NULL,
  pengarang VARCHAR(255) NOT NULL,
  penerbit VARCHAR(255) NOT NULL,
  tahun_terbit INT
);
```

## Create (Membuat Data)

### Membuat Form Tambah Buku

Buat formulir HTML untuk menambahkan buku baru:

```html
<form action="create.php" method="POST">
  <label for="judul">Judul:</label>
  <input type="text" name="judul" required />
  <label for="pengarang">Pengarang:</label>
  <input type="text" name="pengarang" required />
  <label for="penerbit">Penerbit:</label>
  <input type="text" name="penerbit" required />
  <label for="tahun_terbit">Tahun Terbit:</label>
  <input type="number" name="tahun_terbit" />
  <button type="submit">Tambah Buku</button>
</form>
```

### Script PHP untuk Menyimpan Data

Buat file "create.php" untuk menyimpan data buku ke dalam database:

```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
  $judul = $_POST["judul"];
  $pengarang = $_POST["pengarang"];
  $penerbit = $_POST["penerbit"];
  $tahun_terbit = $_POST["tahun_terbit"];

  $koneksi = new mysqli("localhost", "username", "password", "perpustakaan");

  if ($koneksi->connect_error) {
    die("Koneksi gagal: " . $koneksi->connect_error);
  }

  $sql = "INSERT INTO buku (judul, pengarang, penerbit, tahun_terbit) VALUES ('$judul', '$pengarang', '$penerbit', $tahun_terbit)";

  if ($koneksi->query($sql) === TRUE) {
    echo "Buku berhasil ditambahkan";
  } else {
    echo "Gagal menambahkan buku: " . $koneksi->error;
  }

  $koneksi->close();
}
?>
```

## Read (Membaca Data)

### Menampilkan Data Buku

Buat file "read.php" untuk menampilkan data buku yang telah ada di database:

```php
<?php
$koneksi = new mysqli("localhost", "username", "password", "perpustakaan");

if ($koneksi->connect_error) {
  die("Koneksi gagal: " . $koneksi->connect_error);
}

$sql = "SELECT * FROM buku";
$result = $koneksi->query($sql);

if ($result->num_rows > 0) {
  echo "<table>";
  echo "<tr><th>ID</th><th>Judul</th><th>Pengarang</th><th>Penerbit</th><th>Tahun Terbit</th></tr>";
  while ($row = $result->fetch_assoc()) {
    echo "<tr><td>" . $row["id"] . "</td><td>" . $row["judul"] . "</td><td>" . $row["pengarang"] . "</td><td>" . $row["penerbit"] . "</td><td>" . $row["tahun_terbit"] . "</td></tr>";
  }
  echo "</table>";
} else {
  echo "Tidak ada data buku.";
}

$koneksi->close();
?>
```

## Update (Mengubah Data)

### Membuat Form Edit Buku

Buat formulir HTML untuk mengedit buku:

```html
<form action="update.php" method="POST">
  <label for="id">ID Buku:</label>
  <input type="number" name="id" required />
  <label for="judul">Judul:</label>
  <input type="text" name="judul" required />
  <label for="pengarang">Pengarang:</label>
  <input type="text" name="pengarang" required />
  <label for="penerbit">Penerbit:</label>
  <input type="text" name="penerbit" required />
  <label for="tahun_terbit">Tahun Terbit:</label>
  <input type="number" name="tahun_terbit" />
  <button type="submit">Edit Buku</button>
</form>
```

### Script PHP untuk Mengupdate Data

Buat file "update.php" untuk mengupdate data buku:

```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
  $id = $_POST["id"];
  $judul = $_POST["judul"];
  $pengarang = $_POST["pengarang"];
  $penerbit = $_POST["penerbit"];
  $tahun_terbit = $_POST["tahun_terbit"];

  $koneksi = new mysqli("localhost", "username", "password", "perpustakaan");

  if ($koneksi->connect_error) {
    die("Koneksi gagal: " . $koneksi->connect_error);
  }

  $sql = "UPDATE buku SET judul='$judul', pengarang='$pengarang', penerbit='$penerbit', tahun_terbit=$tahun_terbit WHERE id=$id";

  if ($koneksi->query($sql) === TRUE) {
    echo "Buku berhasil diubah";
  } else {
    echo "Gagal mengubah buku: " . $koneksi->error;
  }

  $koneksi->close();
}
?>
```

## Delete (Menghapus Data)

### Membuat Form Hapus Buku

Buat formulir HTML untuk menghapus buku:

```html
<form action="delete.php" method="POST">
  <label for="id">ID Buku yang akan dihapus:</label>
  <input type="number" name="id" required />
  <button type="submit">Hapus Buku</button>
</form>
```

### Script PHP untuk Menghapus Data

Buat file "delete.php" untuk menghapus data buku:

```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
  $id = $_POST["id"];

  $koneksi = new mysqli("localhost", "username", "password", "perpustakaan");

  if ($koneksi->connect_error) {
    die("Koneksi gagal: " . $koneksi->connect_error);
  }

  $sql = "DELETE FROM buku WHERE id=$id";

  if ($koneksi->query($sql) === TRUE) {
    echo "Buku berhasil dihapus";
  } else {
    echo "Gagal menghapus buku: " . $koneksi->error;
  }

  $koneksi->close();
}
?>
```

## Kesimpulan

Dengan mengikuti langkah-langkah di atas, Anda telah berhasil membuat aplikasi sederhana untuk mengelola data buku dengan operasi CRUD menggunakan PHP dan MySQL. Anda dapat memodifikasinya dan menambahkan fitur tambahan sesuai kebutuhan Anda, seperti validasi input, tampilan yang lebih menarik, atau manajemen pengguna. Ini hanya merupakan dasar dari pengembangan aplikasi database, dan Anda dapat memperluas pengetahuan Anda untuk mengembangkan aplikasi yang lebih kompleks.
