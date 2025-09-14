---
title: "Variabel"
weight: 16
---

## Apa Itu Variabel dalam Hugo?

Variabel adalah **potongan informasi** tentang halaman atau situs web Anda yang dapat digunakan di dalam **template** untuk membuat situs menjadi lebih dinamis dan powerful. Variabel bisa berisi judul, tanggal, URL, atau informasi kustom yang Anda tentukan sendiri.

> [!important] **Penting :**
> Variabel hanya dapat diakses di dalam file template (di folder `layouts/`) dan **tidak dapat** digunakan langsung di dalam konten markdown biasa.

---

## Jenis-Jenis Variabel dan Cara Mengaksesnya

**1. Variabel Bawaan (Built-in Page Variables)**
Variabel ini sudah tersedia secara otomatis untuk setiap halaman. Cara mengaksesnya sangat sederhana.

**Contoh Variabel Bawaan:**

- **`.Title`** → Judul halaman (diambil dari `title:` di front matter).
- **`.Date`** → Tanggal pembuatan/publikasi halaman.
- **`.Permalink`** atau **`.URL`** → URL lengkap dari halaman.
- **`.Content`** → Isi konten dari file markdown.

**Cara Akses:**
Gunakan sintaks `{{ .NamaVariabel }}` (dengan titik di depannya).

**Contoh Kode dalam Template:**

```html {title="html"}
<!-- layouts/_default/single.html -->
<h1>{{ .Title }}</h1>
<!-- Akan menampilkan judul halaman -->

<time>Diterbitkan pada: {{ .Date }}</time>
<!-- Akan menampilkan tanggal -->

<a href="{{ .Permalink }}">Link permanen</a>
<!-- Akan menampilkan URL -->

<article>{{ .Content }}</article>
<!-- Akan menampilkan isi artikel -->
```

**2. Variabel Kustom dari Front Matter**
Front matter adalah bagian di atas file markdown yang berisi metadata. Anda bisa membuat variabel kustom sendiri di sini.

**Contoh Front Matter dengan Variabel Kustom:**

```yaml {title="md"}
---
title: "Artikel Pertamaku"
date: 2023-10-27
warna: biru
rating: 5
---
```

**Cara Akses:**
Semua variabel kustom dari front matter diakses melalui **`.Params`**.
Gunakan sintaks `{{ .Params.NamaVariabel }}`.

**Contoh Kode dalam Template:**

```html
<p>Warna tema untuk halaman ini: {{ .Params.warna }}</p>
<!-- Akan menampilkan: "biru" -->

<p>Rating: {{ .Params.rating }}/5</p>
<!-- Akan menampilkan: "5/5" -->
```

**3. Membuat Variabel Langsung di Template**
Anda juga bisa mendefinisikan variabel sendiri langsung di dalam file template menggunakan fungsi `$`.

**Sintaks:**

```
{{ $namaVariabel := "nilainya" }}
```

**Contoh Kode dalam Template:**

```html
<!-- Mendefinisikan variabel -->
{{ $namaSaya := "Belajar Hugo" }} {{ $jumlahArtikel := 3 }}

<!-- Menggunakan variabel -->
<h2>{{ $namaSaya }}</h2>
<p>Saya telah menulis {{ $jumlahArtikel }} artikel.</p>
```

Anda juga bisa menggabungkannya dengan elemen HTML:

```html
{{ $highlightColor := "lightblue" }}
<div style="background-color: {{ $highlightColor }}; padding: 1rem;">
  <p>Div ini memiliki warna latar yang bisa diubah-ubah!</p>
</div>
```

---

## Contoh Praktis: Menggunakan Variabel untuk Gaya CSS

Salah satu kegunaan terkuat variabel front matter adalah mengontrol tampilan halaman secara individual.

**Langkah 1: Tambahkan Variabel di Front Matter Tiap Halaman**

- **a.md:**
  ```yaml
  ---
  title: Halaman A
  warna: blue
  ---
  ```
- **b.md:**
  ```yaml
  ---
  title: Halaman B
  warna: red
  ---
  ```
- **c.md:**
  ```yaml
  ---
  title: Halaman C
  warna: green
  ---
  ```

**Langkah 2: Gunakan Variabel Tersebut di Template**

```html
<!-- layouts/_default/single.html -->
<h1 style="color: {{ .Params.warna }};">{{ .Title }}</h1>
{{ .Content }}
```

**Hasil:**

- Halaman A akan memiliki judul berwarna **biru**.
- Halaman B akan memiliki judul berwarna **merah**.
- Halaman C akan memiliki judul berwarna **hijau**.

---

## Sumber Referensi Variabel Hugo

Hugo memiliki sangat banyak variabel bawaan. Cara terbaik untuk mengeksplorasinya adalah melalui dokumentasi resmi.

- **📚 Hugo Variables Documentation:**  
  [https://gohugo.io/variables/](https://gohugo.io/variables/)

Dokumentasi tersebut membagi variabel-variabel ke dalam beberapa kategori:

- **Page Variables:** Variabel yang spesifik untuk sebuah halaman (e.g., `.Title`, `.IsPage`).

- **Site Variables:** Variabel yang mencakup keseluruhan situs (e.g., `.Site.Title`, `.Site.Pages`).

- **Taxonomy Variables:** Variabel untuk kategori dan tag.

- **File Variables:** Variabel tentang file seperti gambar.
- Dan masih banyak lagi.

---

## Kesimpulan

1.  **Variabel adalah inti** dari template dinamis di Hugo.

2.  Gunakan **`.NamaVariabel`** untuk variabel bawaan (e.g., `{{ .Title }}`).

3.  Gunakan **`.Params.NamaVariabel`** untuk variabel kustom dari front matter (e.g., `{{ .Params.warna }}`).

4.  Anda bisa **membuat variabel sendiri** di template dengan `$nama := nilai`.

5.  Variabel sangat powerful untuk **mengontrol konten dan tampilan** berdasarkan metadata.

6.  Selalu **lihat dokumentasi resmi** untuk menemukan variabel-variabel lain yang dapat digunakan.

Dengan menguasai variabel, Anda dapat membuat template Hugo yang jauh lebih fleksibel dan powerful!

