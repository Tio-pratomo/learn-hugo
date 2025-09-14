---
title: "Mengenal Shortcode di Hugo"
weight: 8
---

Kita akan membahas **Shortcode**. Shortcode adalah salah satu fitur paling praktis di Hugo. Anggap saja Shortcode sebagai **cuplikan HTML (HTML snippets) yang sudah disiapkan sebelumnya** yang bisa Anda sisipkan langsung ke dalam file Markdown Anda.

## Mengapa Kita Perlu Shortcode?

Bayangkan Anda ingin menyematkan (embed) video YouTube di dalam sebuah artikel blog. Biasanya, Anda harus menyalin kode `<iframe>` yang panjang dan rumit dari YouTube dan menempelkannya ke file Markdown Anda. Ini bisa membuat file Markdown terlihat berantakan dan sulit dibaca.

Dengan Shortcode, Anda tidak perlu lagi berurusan dengan kode HTML yang rumit. Hugo sudah memiliki beberapa Shortcode bawaan yang siap digunakan, memungkinkan Anda menambahkan fitur seperti video, galeri gambar, atau elemen lainnya hanya dengan satu baris kode sederhana.

## Cara Menggunakan Shortcode

Sintaks dasar untuk Shortcode sangat sederhana. Anda hanya perlu mengetikkan nama Shortcode di antara dua kurung kurawal ganda dan tanda `< >`.

**&lbrace;&lbrace;&lt; shortcode-name parameter1 parameter2 &gt;&rbrace;&rbrace;**

- **`shortcode-name`**: Nama dari Shortcode yang ingin Anda gunakan.
- **`parameter1`**, **`parameter2`**: Nilai yang Anda berikan ke Shortcode. Parameter ini bisa berupa teks, angka, atau ID.

## Contoh: Menyematkan Video YouTube

Hugo sudah menyediakan Shortcode bawaan untuk YouTube. Anda hanya perlu menyisipkan ID video yang ingin Anda tampilkan.

1.  **Temukan ID Video YouTube**:

    - Buka video YouTube di browser Anda.
    - ID video adalah bagian terakhir dari URL-nya. Misalnya, dari URL `https://www.youtube.com/watch?v=dQw4w9WgXcQ`, ID-nya adalah `dQw4w9WgXcQ`.

2.  **Sisipkan Shortcode**:

    - Buka file Markdown Anda (misalnya `a.md`).
    - Masukkan Shortcode dengan format :

    **&lbrace;&lbrace;&lt; youtube ID_video &gt;&rbrace;&rbrace;**

    \---

    title: "Artikel dengan Video YouTube"

    date: 2025-09-12T15:43:07+07:00

    \---

    Ini adalah artikel saya. Di bawah ini, saya akan menyisipkan video YouTube.

    **&lbrace;&lbrace;&lt; youtube dQw4w9WgXcQ &gt;&rbrace;&rbrace;**

    ***

    Sangat mudah,bukan?

    Ketika Anda menyimpan file ini dan Hugo merender situs web, Hugo akan mengenali Shortcode :

    **&lbrace;&lbrace;&lt; youtube ... &gt;&rbrace;&rbrace;**

    Kemudian, mencari template HTML yang sesuai, dan secara otomatis menyematkan video YouTube di tempat yang Anda inginkan.

## Mengapa Shortcode Sangat Efisien?

- **Sederhana**: Anda tidak perlu menulis kode HTML yang panjang. Hanya satu baris Shortcode sudah cukup.

- **Bersih**: File Markdown Anda tetap bersih dan mudah dibaca, tanpa terganggu oleh kode-kode teknis.

- **Fleksibel**: Hugo dilengkapi dengan banyak Shortcode bawaan (seperti `youtube`, `vimeo`, `instagram`, dll.). Anda dapat melihat daftar lengkapnya di [dokumentasi resmi Hugo](https://gohugo.io/content-management/shortcodes/).

Di pelajaran selanjutnya, kita akan belajar cara membuat Shortcode kustom Anda sendiri. Ini akan sangat berguna jika Anda ingin menambahkan elemen HTML unik yang sering Anda gunakan di situs Anda.

Apakah materi ini sudah cukup jelas? Apakah ada pertanyaan lain tentang cara kerja Shortcode?
