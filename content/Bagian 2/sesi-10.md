---
title: "Memahami Template Dasar di Hugo"
weight: 10
---

Template adalah fondasi dari bagaimana situs Hugo Anda ditampilkan. Mereka adalah file HTML yang berisi kerangka atau struktur dasar yang sama yang akan digunakan oleh banyak halaman, sementara konten spesifiknya diisi secara dinamis.

## Apa Itu Template?

Bayangkan template sebagai **cetakan kue**. Cetakannya sama, tetapi Anda bisa memasukkan adonan yang berbeda (konten) ke dalamnya untuk menghasilkan kue (halaman web) yang bentuknya sama tetapi isinya berbeda.

Dalam konteks Hugo:

- Template menentukan tata letak, header, footer, navbar, dan elemen umum lainnya yang konsisten di seluruh situs.

- Konten dari file Markdown Anda ("isi adonan") akan di-"cetak" ke dalam template ini untuk menghasilkan halaman HTML akhir.

## Dua Jenis Halaman dan Template Utama

Hugo pada dasarnya mengenali dua jenis halaman, yang masing-masing membutuhkan template berbeda:

### 1. Halaman Daftar (List Pages)

Halaman ini menampilkan **kumpulan** atau **daftar** konten.

- **Contoh:** Halaman beranda (homepage) yang menampilkan postingan terbaru, halaman kategori yang menampilkan semua postingan dalam kategori tertentu, atau halaman arsip.

- Template default untuk halaman daftar adalah `layouts/_default/list.html`.

### 2. Halaman Tunggal (Single Pages)

Halaman ini menampilkan **satu buah** konten secara utuh.

- **Contoh:** Halaman sebuah blog post, halaman "Tentang Kami", atau halaman kontak.

- Template default untuk halaman tunggal adalah `layouts/_default/single.html`.

## Di Mana Template Disimpan?

Template berada di dalam folder `layouts` pada root project Hugo Anda atau di dalam folder tema. Struktur yang umum adalah:

```tree
- your-hugo-site/ | folder
    - archetypes/ | folder-open
    - content/ | folder-open
    - layouts/   <-- Template kustom Anda diletakkan di sini | folder-open
        - _default/ | folder-open
            - list.html  <-- Template untuk halaman daftar | fa-brands fa-html5 | magenta
            - single.html <-- Template untuk halaman tunggal | fa-brands fa-html5 | magenta
    - static/ | folder-open
    - themes/ | folder-open
        - nama-tema-anda/ | folder-open
            - layouts/  <-- Template dari tema | folder-open
                - _default/ | folder-open
                    - list.html | fa-brands fa-html5 | magenta
                    - single.html | fa-brands fa-html5 | magenta
```

Hugo akan memprioritaskan template yang Anda buat di folder `layouts` root project Anda. Jika tidak ditemukan, barulah ia akan menggunakan template dari folder tema.

### Cara Kerja Template: Contoh Sederhana

Mari kita lihat potongan kode dari sebuah template `single.html` yang sangat mendasar.

```html {title="html" wrap="true"}
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <title>{{ .Title }} | Situs Saya</title>
    <!-- Title dari front matter konten -->
    <link rel="stylesheet" href="/style.css" />
  </head>
  <body>
    <header>
      <h1>Header Situs Saya</h1>
      <!-- Header yang sama di setiap halaman -->
      <nav><!-- Navigasi --></nav>
    </header>

    <main>
      <!-- Bagian ini akan diisi oleh konten spesifik dari file Markdown -->
      <article>
        <h2>{{ .Title }}</h2>
        <!-- Menampilkan judul -->
        <p>Diterbitkan pada: {{ .Date.Format "2 January 2006" }}</p>
        <!-- Menampilkan tanggal -->
        {{ .Content }}
        <!-- Menampilkan isi konten Markdown -->
      </article>

      <!-- Kita tambahkan teks percobaan -->
      <p>Ini adalah teks percobaan yang ditambahkan ke template. Ini akan muncul di SETIAP halaman tunggal.</p>
    </main>

    <footer>
      &copy; {{ now.Format "2006" }} Situs Saya.
      <!-- Footer yang sama di setiap halaman -->
    </footer>
  </body>
</html>
```

**Penjelasan Kode:**

- `{{ .Title }}`, `{{ .Date }}`, `{{ .Content }}` adalah variabel dari Hugo yang akan diganti dengan nilai sebenarnya dari front matter dan isi konten file Markdown.

- Elemen seperti `<header>`, `<nav>`, dan `<footer>` akan tetap sama di setiap halaman yang menggunakan template ini.

- Baris `<p>Ini adalah teks percobaan...</p>` membuktikan bahwa perubahan pada template memengaruhi semua halaman tunggal. Jika Anda menambahkannya, teks itu akan muncul di bawah setiap artikel.

### Kesimpulan

Template adalah mekanisme Hugo untuk menjaga konsistensi dan **DRY (Don't Repeat Yourself)**. Daripada menulis ulang kode HTML yang sama untuk setiap halaman, Anda cukup membuat satu template yang bagus dan membiarkan Hugo mengisi bagian yang dinamis dengan konten Anda.

Untuk memulai, Anda bisa menyalin file `list.html` dan `single.html` dari tema yang Anda gunakan ke dalam folder `layouts/_default/` di root project Anda dan mulai memodifikasinya sesuai keinginan.

