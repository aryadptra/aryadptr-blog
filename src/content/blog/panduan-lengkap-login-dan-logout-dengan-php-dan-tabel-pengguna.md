---
title: 'Panduan Lengkap Login dan Logout dengan PHP dan Tabel Users'
description: 'Tutorial Login dan Logout PHP dengan Tabel Users'
pubDate: '2023-11-06T13:21:15.031Z'
heroImage: '/blog-placeholder.jpg'
categories: ['Tutorial PHP']
authors: ['Arya Dwi Putra']
tags: ['php', 'basic', 'web', 'programming', 'beginner']
---

Sistem login dan logout adalah salah satu komponen paling penting dalam pengembangan situs web yang melibatkan pengguna terdaftar. Pada artikel ini, kita akan membahas bagaimana membuat sistem login dan logout dengan menggunakan PHP dan tabel pengguna (users) dalam database.

## Persiapan

Sebelum kita mulai, pastikan Anda telah menginstal server web (seperti Apache), MySQL, dan PHP di lingkungan pengembangan Anda. Selain itu, pastikan Anda memiliki tabel pengguna dalam database MySQL Anda. Struktur tabel pengguna mungkin terlihat seperti ini:

```sql
CREATE TABLE users (
  id INT PRIMARY KEY AUTO_INCREMENT,
  username VARCHAR(255) NOT NULL,
  password VARCHAR(255) NOT NULL
);
```

## Login

### Membuat Form Login

Buat formulir HTML untuk login:

```html
<form action="login.php" method="POST">
  <label for="username">Username:</label>
  <input type="text" name="username" required />
  <label for="password">Password:</label>
  <input type="password" name="password" required />
  <button type="submit">Login</button>
</form>
```

### Script PHP untuk Proses Login

Buat file "login.php" untuk memproses login:

```php
<?php
session_start();

if ($_SERVER["REQUEST_METHOD"] == "POST") {
  $username = $_POST["username"];
  $password = $_POST["password"];

  $koneksi = new mysqli("localhost", "username", "password", "database");

  if ($koneksi->connect_error) {
    die("Koneksi gagal: " . $koneksi->connect_error);
  }

  $sql = "SELECT * FROM users WHERE username='$username' AND password='$password'";
  $result = $koneksi->query($sql);

  if ($result->num_rows == 1) {
    $_SESSION["username"] = $username;
    header("location: welcome.php");
  } else {
    echo "Login gagal. Silakan coba lagi.";
  }

  $koneksi->close();
}
?>
```

### Halaman Selamat Datang (welcome.php)

Buat halaman "welcome.php" yang hanya dapat diakses oleh pengguna yang telah berhasil login:

```php
<?php
session_start();

if (!isset($_SESSION["username"])) {
  header("location: login.php");
}

$username = $_SESSION["username"];
?>

<!DOCTYPE html>
<html>
<head>
  <title>Selamat Datang, <?php echo $username; ?></title>
</head>
<body>
  <h1>Selamat Datang, <?php echo $username; ?></h1>
  <a href="logout.php">Logout</a>
</body>
</html>
```

## Logout

### Script PHP untuk Logout

Buat file "logout.php" untuk memproses logout:

```php
<?php
session_start();
session_destroy();
header("location: login.php");
?>
```

## Kesimpulan

Dengan mengikuti langkah-langkah di atas, Anda telah berhasil membuat sistem login dan logout dengan menggunakan PHP dan tabel pengguna dalam database. Sistem ini memungkinkan pengguna untuk masuk ke situs web Anda dengan akun mereka, dan juga untuk keluar dengan aman. Anda dapat memodifikasinya dan menambahkan fitur keamanan tambahan, seperti enkripsi kata sandi, manajemen sesi yang lebih baik, dan manajemen hak akses pengguna sesuai kebutuhan Anda. Ini hanya merupakan dasar dari pengembangan sistem keamanan dalam aplikasi web, dan Anda dapat memperluas pengetahuan Anda untuk mengembangkan aplikasi yang lebih canggih.
