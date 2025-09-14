---
title: "Template Halaman Daftar (List Templates)"
weight: 11
---

Template halaman daftar (list templates) adalah jenis template khusus dalam Hugo yang digunakan untuk menampilkan kumpulan atau daftar konten, bukan satu konten tunggal.

## Apa Itu Halaman Daftar?

Halaman daftar adalah halaman yang berisi rangkuman atau daftar dari beberapa konten. Contohnya:

- **Halaman Beranda (Homepage):** Menampilkan daftar postingan terbaru.

- **Halaman Kategori/Tag:** Menampilkan semua postingan dalam kategori atau tag tertentu.

- **Halaman Arsip:** Menampilkan postingan yang dikelompokkan berdasarkan bulan atau tahun.

Hugo secara otomatis membuat halaman daftar untuk setiap bagian (section) dalam situs Anda. Halaman-halaman ini biasanya menggunakan file bernama `_index.md` di dalam direktori konten.

## Membuat Template Daftar Kustom

Untuk membuat template daftar kustom Anda sendiri, ikuti struktur folder berikut di root project Hugo Anda (bukan di folder tema):

```tree
- your-hugo-site/ | folder
    - layouts/ | folder-open
        - _default/ | folder-open
            - list.html  <-- Template daftar kustom Anda | fa-brands fa-html5 | magenta
```

Dengan membuat file `list.html` di lokasi ini, Anda **mengoverride** template daftar default dari tema yang Anda gunakan.

## Contoh Dasar Template Daftar

Berikut adalah contoh dasar template daftar yang sangat sederhana:

```html {title="html" wrap="true"}
<!-- layouts/_default/list.html -->
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <title>Daftar Konten</title>
  </head>
  <body>
    <h1>Ini adalah Template Daftar Kustom Saya</h1>

    <!-- Menampilkan konten dari file _index.md -->
    <div>{{ .Content }}</div>

    <!-- Daftar semua halaman dalam section ini -->
    <h2>Daftar Halaman:</h2>
    <ul>
      {{ range .Pages }}
      <li>
        <a href="{{ .Permalink }}">{{ .Title }}</a>
      </li>
      {{ end }}
    </ul>
  </body>
</html>
```

## Memahami Variabel dan Fungsi dalam Template Daftar

Dalam contoh di atas, kita menggunakan beberapa variabel dan fungsi penting Hugo:

1.  **`.Content`:** Menampilkan isi dari file `_index.md` yang terkait dengan halaman daftar ini.

2.  **`.Pages`:** Merupakan kumpulan semua halaman biasa (bukan halaman daftar) dalam section saat ini.

3.  **`range`:** Fungsi untuk melakukan perulangan melalui kumpulan halaman. Sintaksnya adalah:

    ```go-html-template
    {{ range .KumpulanHalaman }}
        <!-- Kode yang diulang untuk setiap halaman -->
    {{ end }}
    ```

4.  **`.Permalink` dan `.Title`:** Variabel yang mengembalikan URL permanen dan judul dari setiap halaman.

## Contoh Template Daftar yang Lebih Kompleks

Berikut adalah contoh template daftar yang lebih informatif, menampilkan judul, tanggal publikasi, dan ringkasan untuk setiap halaman:

```html {title="html" wrap="true"}
<!-- layouts/_default/list.html -->
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <title>{{ .Title }} | Situs Saya</title>
  </head>
  <body>
    <header>
      <h1>{{ .Title }}</h1>
    </header>

    <main>
      <!-- Konten dari _index.md -->
      {{ .Content }}

      <!-- Daftar halaman dengan informasi lebih detail -->
      <h2>Konten dalam Kategori Ini:</h2>
      <ul>
        {{ range .Pages }}
        <li>
          <article>
            <h3><a href="{{ .Permalink }}">{{ .Title }}</a></h3>
            <p>Diterbitkan: {{ .Date.Format "2 January 2006" }}</p>
            <p>{{ .Summary }}</p>
            <a href="{{ .Permalink }}">Baca selengkapnya...</a>
          </article>
        </li>
        {{ end }}
      </ul>
    </main>

    <footer>
      <p>&copy; {{ now.Format "2006" }} Situs Saya</p>
    </footer>
  </body>
</html>
```

**Variabel baru yang digunakan:**

- **.Summary:** Menampilkan ringkasan otomatis dari konten (sekitar 70 kata pertama).

- **.Date.Format:** Memformat tanggal publikasi dengan layout tertentu.

- **now.Format:** Menampilkan tahun saat ini untuk copyright footer.

## Cara Kerja Prioritas Template

Hugo memiliki sistem prioritas yang canggih untuk menentukan template mana yang akan digunakan. Untuk halaman daftar, Hugo akan mencari template dalam urutan berikut:

1.  `layouts/section/NAMA-SECTION/list.html`

2.  `layouts/_default/list.html`

3.  `themes/NAMA-TEMA/layouts/section/NAMA-SECTION/list.html`

4.  `themes/NAMA-TEMA/layouts/_default/list.html`

Ini berarti Anda dapat membuat template daftar khusus untuk section tertentu dengan membuat file di `layouts/section/NAMA-SECTION/list.html`.

## Kesimpulan

Template halaman daftar adalah alat yang powerful untuk mengatur dan menampilkan kumpulan konten di situs Hugo Anda. Dengan memahami cara menggunakan variabel seperti `.Pages` dan fungsi seperti `range`, Anda dapat membuat navigasi dan tampilan daftar konten yang sesuai dengan kebutuhan desain situs Anda.

Mulailah dengan template sederhana, lalu secara bertahap tambahkan kompleksitas sesuai kebutuhan. Selalu ingat untuk meletakkan template kustom Anda di folder `layouts/` di root project, bukan di folder tema, agar perubahan Anda tidak tertimpa saat memperbarui tema.

