---
title: "Template Halaman Tunggal (Single Templates)"
weight: 12
---

Template halaman tunggal adalah jenis template dalam Hugo yang digunakan untuk menampilkan satu konten individual secara utuh, seperti artikel blog, halaman tentang, atau halaman kontak.

## Apa Itu Halaman Tunggal?

Halaman tunggal adalah halaman yang menampilkan satu unit konten lengkap. Berbeda dengan halaman daftar yang menampilkan banyak konten sekaligus, halaman tunggal fokus pada satu konten tertentu.

**Contoh halaman tunggal:**

- Sebuah artikel blog

- Halaman "Tentang Kami"

- Halaman "Kontak"

- Dokumentasi produk

## Membuat Template Tunggal Kustom

Untuk membuat template tunggal kustom Anda sendiri, buat struktur folder berikut di root project Hugo:

```tree
- your-hugo-site/ | folder
    - layouts/ | folder-open
        - _default/ | folder-open
            - single.html  <-- Template tunggal kustom Anda | fa-brands fa-html5 | magenta
```

Dengan membuat file `single.html` di lokasi ini, Anda akan **menggantikan** template tunggal default dari tema yang Anda gunakan.

## Contoh Dasar Template Tunggal

```html
<!-- layouts/_default/single.html -->
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <title>{{ .Title }} | Situs Saya</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        max-width: 800px;
        margin: 0 auto;
        padding: 20px;
      }
      header {
        border-bottom: 2px solid #eee;
        margin-bottom: 30px;
        padding-bottom: 10px;
      }
      footer {
        border-top: 2px solid #eee;
        margin-top: 30px;
        padding-top: 10px;
        font-size: 0.9em;
      }
    </style>
  </head>
  <body>
    <!-- Header yang konsisten di setiap halaman -->
    <header>
      <h1>{{ .Title }}</h1>
      <p>Diterbitkan pada: {{ .Date.Format "2 January 2006" }}</p>
    </header>

    <!-- Konten utama dari file Markdown -->
    <main>{{ .Content }}</main>

    <!-- Footer yang konsisten di setiap halaman -->
    <footer>
      <p>&copy; {{ now.Format "2006" }} Situs Saya. Semua hak dilindungi.</p>
    </footer>
  </body>
</html>
```

## Memahami Variabel dalam Template Tunggal

Dalam template tunggal, Anda dapat mengakses berbagai variabel dari front matter dan metadata halaman:

1.  **`.Content`:** Menampilkan isi konten dari file Markdown.

2.  **`.Title`:** Judul halaman dari front matter.

3.  **`.Date`:** Tanggal publikasi dari front matter.

4.  **`.Permalink`:** URL permanen ke halaman ini.

## Mengakses Variabel Front Matter Kustom

Jika Anda memiliki variabel front matter kustom, Anda dapat mengaksesnya dengan sintaks yang sama:

**File Markdown (`content/posts/post-pertama.md`):**

```markdown
---
title: "Postingan Pertama Saya"
date: 2023-10-27T10:00:00+07:00
draft: false
penulis: "Nama Anda"
rating: 5
---

Ini adalah konten postingan pertama saya...
```

**Template Tunggal (`layouts/_default/single.html`):**

```html
<article>
  <h1>{{ .Title }}</h1>

  <div class="meta-info">
    <p>Ditulis oleh: {{ .Params.penulis }}</p>
    <p>Diterbitkan: {{ .Date.Format "2 January 2006" }}</p>
    <p>Rating: {{ .Params.rating }}/5</p>
  </div>

  <div class="content">{{ .Content }}</div>
</article>
```

## Template yang Lebih Kompleks dengan Navigasi

```html
<!-- layouts/_default/single.html -->
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>{{ .Title }} | Situs Saya</title>
    <link rel="stylesheet" href="/css/style.css">
</head>
<body>
    <nav>
        <a href="{{ "/" | relURL }}">Beranda</a>
        <a href="{{ "/tentang" | relURL }}">Tentang</a>
        <a href="{{ "/blog" | relURL }}">Blog</a>
    </nav>

    <article>
        <header>
            <h1>{{ .Title }}</h1>
            <div class="meta">
                <time datetime="{{ .Date.Format "2006-01-02" }}">
                    {{ .Date.Format "2 January 2006" }}
                </time>
                {{ if .Params.penulis }}
                    <span class="penulis">Oleh: {{ .Params.penulis }}</span>
                {{ end }}
            </div>
        </header>

        <div class="content">
            {{ .Content }}
        </div>

        <footer>
            {{ with .Params.tags }}
            <div class="tags">
                <strong>Tag:</strong>
                {{ range . }}
                <a href="{{ "/tags/" | relURL }}{{ . | urlize }}">{{ . }}</a>
                {{ end }}
            </div>
            {{ end }}
        </footer>
    </article>

    <footer>
        <p>&copy; {{ now.Format "2006" }} Situs Saya</p>
    </footer>
</body>
</html>
```

## Cara Kerja Prioritas Template

Seperti template daftar, Hugo memiliki sistem prioritas untuk template tunggal:

1.  `layouts/section/NAMA-SECTION/single.html`

2.  `layouts/_default/single.html`

3.  `themes/NAMA-TEMA/layouts/section/NAMA-SECTION/single.html`

4.  `themes/NAMA-TEMA/layouts/_default/single.html`

Ini berarti Anda dapat membuat template tunggal khusus untuk section tertentu. Misalnya, untuk membuat template khusus untuk postingan blog, buat file di:
`layouts/blog/single.html`

## Kesimpulan

Template halaman tunggal memungkinkan Anda mengontrol bagaimana konten individual ditampilkan di situs Hugo Anda. Dengan memahami cara menggunakan variabel seperti `.Content`, `.Title`, dan `.Params`, Anda dapat membuat pengalaman tampilan yang konsisten dan menarik untuk semua halaman tunggal di situs Anda.

Kekuatan template tunggal terletak pada kemampuannya untuk memisahkan struktur HTML (yang konsisten di semua halaman) dari konten aktual (yang unik untuk setiap halaman), membuat maintenance situs menjadi lebih mudah dan efisien.
