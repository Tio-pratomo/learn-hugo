---
title: "Template Halaman Beranda (Homepage Templates)"
weight: 13
---

Halaman beranda (homepage) adalah halaman khusus yang memiliki peran unik dalam situs Hugo. Meskipun secara teknis termasuk dalam kategori halaman daftar (list page), homepage seringkali memerlukan tampilan dan tata letak yang berbeda dari halaman daftar biasa.

## Keunikan Halaman Beranda

Beranda biasanya merupakan halaman pertama yang dilihat pengunjung, sehingga sering membutuhkan:

- Desain yang lebih menarik
- Pengenalan singkat tentang situs
- Highlights konten terbaru atau terpopuler
- Navigasi yang berbeda dari halaman lainnya

## Membuat Template Beranda Kustom

Untuk membuat template beranda khusus, buat file **index.html** di direktori **layouts** root project Anda:

```tree
- your-hugo-site/ | folder
    - layouts/ | folder-open
        - _default/ | folder-open
            - list.html    <-- Template untuk halaman daftar biasa | fa-brands fa-html5 | magenta
            - single.html  <-- Template untuk halaman tunggal | fa-brands fa-html5 | magenta
    - index.html       <-- Template khusus untuk homepage | fa-brands fa-html5 | magenta
```

Dengan membuat file {{<bold>}} index.html {{</bold>}} di lokasi ini, Anda membuat template khusus yang hanya akan digunakan untuk halaman beranda, bukan halaman daftar lainnya.

## Contoh Dasar Template Beranda

```html {title="html" wrap="true"}
<!-- layouts/index.html -->
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <title>Beranda - {{ .Site.Title }}</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        max-width: 1000px;
        margin: 0 auto;
        padding: 20px;
      }
      .hero {
        text-align: center;
        padding: 50px 0;
        background-color: #f5f5f5;
        margin-bottom: 40px;
      }
      .featured-posts {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
        gap: 20px;
      }
      .post-card {
        border: 1px solid #ddd;
        padding: 20px;
        border-radius: 5px;
      }
    </style>
  </head>
  <body>
    <!-- Header khusus untuk beranda -->
    <header>
      <h1>Selamat Datang di {{ .Site.Title }}</h1>
      <nav>
        <a href="/">Beranda</a>
        <a href="/tentang">Tentang</a>
        <a href="/blog">Blog</a>
        <a href="/kontak">Kontak</a>
      </nav>
    </header>

    <!-- Section hero untuk pengenalan -->
    <section class="hero">
      <h2>{{ .Site.Params.tagline | default "Situs web saya yang keren" }}</h2>
      <p>Temukan berbagai konten menarik dan informatif di sini</p>
    </section>

    <!-- Daftar postingan terbaru -->
    <section>
      <h2>Postingan Terbaru</h2>
      <div class="featured-posts">
        {{ range first 3 (where .Site.RegularPages "Type" "post") }}
        <article class="post-card">
          <h3><a href="{{ .Permalink }}">{{ .Title }}</a></h3>
          <p>{{ .Date.Format "2 January 2006" }}</p>
          <p>{{ .Summary }}</p>
          <a href="{{ .Permalink }}">Baca selengkapnya →</a>
        </article>
        {{ end }}
      </div>
    </section>

    <!-- Section tentang singkat -->
    <section>
      <h2>Tentang Situs Ini</h2>
      <p>{{ .Site.Params.description | default "Ini adalah situs web yang dibangun dengan Hugo static site generator." }}</p>
    </section>

    <!-- Footer -->
    <footer>
      <p>&copy; {{ now.Format "2006" }} {{ .Site.Title }}. All rights reserved.</p>
    </footer>
  </body>
</html>
```

## Variabel Khusus untuk Halaman Beranda

Dalam template beranda, Anda dapat mengakses variabel khusus:

1.  {{<bold>}} .Site.Title : {{</bold>}} Judul situs dari konfigurasi

2.  {{<bold>}} .Site.Params : {{</bold>}} Parameter kustom dari file konfigurasi

3.  {{< bold >}} .Site.RegularPages :{{< /bold >}} Semua halaman biasa (bukan halaman bagian)

4.  {{< bold >}} .Site.Sections : {{< /bold >}} Semua bagian utama situs

## Mengambil Konten dari `_index.md`

Anda juga dapat menambahkan file `content/_index.md` untuk menyediakan konten khusus untuk beranda:

**File `content/_index.md`:**

```markdown {title="markdown" wrap="true"}
---
title: "Selamat Datang di Saya Saya"
date: 2023-10-27T10:00:00+07:00
---

Ini adalah teks pengantar untuk halaman beranda saya. Saya bisa menulis apa saja di sini dan akan muncul di bagian atas halaman beranda.
```

{{< bold >}} **Template layouts/index.html (tambahkan ini) :** {{< /bold >}}

```html {title="html" wrap="true"}
<!-- Di bagian setelah hero section -->
<section class="intro">
  {{ .Content }}
  <!-- Ini akan menampilkan konten dari content/_index.md -->
</section>
```

## Template Beranda yang Lebih Dinamis

```html {title="html" wrap="true"}
<!-- layouts/index.html -->
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <title>{{ .Site.Title }}</title>
  </head>
  <body>
    <header>
      <!-- Navigasi utama -->
    </header>

    <main>
      <!-- Konten dari _index.md -->
      <section class="welcome">{{ .Content }}</section>

      <!-- Postingan terbaru -->
      <section class="recent-posts">
        <h2>Postingan Terbaru</h2>
        <div class="posts-grid">
          {{ range first 6 (where .Site.RegularPages "Type" "post") }}
          <article class="post-item">
            <h3><a href="{{ .Permalink }}">{{ .Title }}</a></h3>
            <p class="date">{{ .Date.Format "2 January 2006" }}</p>
            <p class="summary">{{ .Summary }}</p>
            {{ with .Params.tags }}
            <div class="tags">
              {{ range . }}
              <span class="tag">{{ . }}</span>
              {{ end }}
            </div>
            {{ end }}
          </article>
          {{ end }}
        </div>
      </section>

      <!-- Daftar kategori -->
      <section class="categories">
        <h2>Jelajahi Kategori</h2>
        <div class="category-list">
          {{ range .Site.Taxonomies.categories }}
          <a href="{{ .Page.Permalink }}" class="category-item"> {{ .Page.Title }} ({{ .Count }}) </a>
          {{ end }}
        </div>
      </section>
    </main>

    <footer>
      <!-- Footer -->
    </footer>
  </body>
</html>
```

## Kesimpulan

Template halaman beranda khusus memungkinkan Anda membuat kesan pertama yang kuat bagi pengunjung situs Anda. Dengan membuat file `index.html` di direktori `layouts/`, Anda dapat mendesain beranda yang unik dan berbeda dari halaman lainnya di situs Anda.

Manfaatkan variabel seperti `.Site.RegularPages`, `.Site.Taxonomies`, dan `.Site.Params` untuk membuat beranda yang dinamis dan informatif. Jangan lupa untuk juga menggunakan file `content/_index.md` untuk memberikan konten pengantar yang khusus untuk halaman beranda Anda.

