---
title: 'Penjelasan Algoritma Binary Search Beserta Contoh Menggunakan PHP'
description: 'Contoh Singkat Algoritma Binary Search Menggunakan PHP'
pubDate: '2023-11-06T22:45:26.564Z'
heroImage: '/blog-placeholder.jpg'
categories: ['Tutorial Algoritma']
authors: ['Arya Dwi Putra']
tags: ['php', 'web', 'programming', 'beginner', 'algorithms', 'logics']
---

Algoritma Binary Search adalah salah satu algoritma pencarian yang efisien digunakan untuk mencari elemen dalam sebuah himpunan data yang sudah terurut. Algoritma ini bekerja dengan membagi himpunan data menjadi dua bagian dan membandingkan elemen tengahnya dengan elemen yang dicari. Jika elemen yang dicari lebih kecil, maka pencarian dilanjutkan hanya pada separuh bagian kiri himpunan data; jika lebih besar, maka hanya pada separuh bagian kanan. Proses ini berlanjut hingga elemen yang dicari ditemukan atau sampai hanya satu elemen yang tersisa untuk dicari.

Berikut adalah penjelasan lengkap dan contoh penggunaan algoritma Binary Search dalam PHP:

### Penjelasan Algoritma Binary Search

1. Langkah Pertama: Pastikan himpunan data sudah terurut. Binary Search hanya berfungsi pada data yang terurut.

2. Tentukan elemen yang akan dicari (misalnya, "elemen yang dicari").

3. Tentukan dua indeks, `low` dan `high`, yang akan digunakan untuk menandai batas awal dan akhir himpunan data. Awalnya, `low` akan diatur sebagai indeks pertama (0) dan `high` akan diatur sebagai indeks terakhir (jumlah elemen himpunan data - 1).

4. Di dalam loop, hitung indeks tengah `mid` sebagai rata-rata dari `low` dan `high`. Ini adalah elemen yang akan dibandingkan dengan "elemen yang dicari".

5. Bandingkan elemen yang terletak pada indeks `mid` dengan "elemen yang dicari":

   - Jika elemen di indeks `mid` sama dengan "elemen yang dicari," maka pencarian selesai, dan Anda telah menemukan elemen yang dicari.
   - Jika elemen di indeks `mid` lebih besar dari "elemen yang dicari," maka perbarui `high` menjadi `mid - 1`, sehingga pencarian akan dilanjutkan di setengah kiri himpunan data.
   - Jika elemen di indeks `mid` lebih kecil dari "elemen yang dicari," maka perbarui `low` menjadi `mid + 1`, sehingga pencarian akan dilanjutkan di setengah kanan himpunan data.

6. Ulangi langkah 4 dan 5 hingga Anda menemukan "elemen yang dicari" atau `low` melewati `high`, yang menandakan bahwa elemen tidak ditemukan dalam himpunan data.

### Contoh Penggunaan Binary Search dalam PHP

Berikut adalah contoh implementasi algoritma Binary Search dalam PHP:

```php
function binarySearch($arr, $target) {
    $low = 0;
    $high = count($arr) - 1;

    while ($low <= $high) {
        $mid = floor(($low + $high) / 2);

        if ($arr[$mid] == $target) {
            return $mid; // Elemen ditemukan, mengembalikan indeksnya.
        } elseif ($arr[$mid] < $target) {
            $low = $mid + 1;
        } else {
            $high = $mid - 1;
        }
    }

    return -1; // Elemen tidak ditemukan.
}

// Contoh penggunaan algoritma Binary Search
$data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
$target = 7;
$hasil = binarySearch($data, $target);

if ($hasil != -1) {
    echo "Elemen $target ditemukan di indeks ke-$hasil.";
} else {
    echo "Elemen $target tidak ditemukan dalam himpunan data.";
}
```

Dalam contoh ini, fungsi `binarySearch` menerima sebuah himpunan data yang sudah terurut (`$arr`) dan elemen yang dicari (`$target`). Fungsi ini mengembalikan indeks elemen yang dicari jika ditemukan atau -1 jika tidak ditemukan.

Dalam kasus contoh di atas, elemen 7 ditemukan dalam himpunan data, dan indeksnya adalah 6.
