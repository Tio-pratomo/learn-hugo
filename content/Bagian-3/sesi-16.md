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

Secara mendasar, semua variabel di dalam template Hugo diakses melalui sebuah objek "konteks" yang dilambangkan dengan tanda titik {{< bold >}}(.){{< /bold >}}.

Anggap saja tanda titik (context) adalah sebuah kantong data ajaib yang isinya berubah-ubah tergantung halaman apa yang sedang Hugo buat.

Ada 3 sumber utama data yang bisa Anda akses:

1.  Variabel Halaman {{< bold >}}(.){{< /bold >}} : Informasi spesifik tentang halaman yang sedang dirender.

2.  Variabel File {{< bold >}}(.File){{< /bold >}} : Informasi tentang file sumber (.md) dari halaman tersebut.

3.  Variabel Situs {{< bold >}}(.Site){{< /bold >}} : Informasi global tentang keseluruhan situs Anda.

Mari kita bahas satu per satu secara lengkap.

---

## Variabel Halaman (Page Variables)

Ini adalah variabel yang paling sering Anda gunakan. Ketika Hugo merender sebuah halaman (misalnya sebuah postingan blog), . akan berisi semua
informasi tentang halaman tersebut.

- {{< bold >}}.Title :{{< /bold >}} Judul halaman, diambil dari front matter title.

- {{< bold >}}.Content :{{< /bold >}} Isi utama halaman Anda (yang sudah diubah dari Markdown ke HTML).

- {{< bold >}}.Date :{{< /bold >}} Tanggal dari front matter. Ini adalah sebuah objek tanggal, jadi Anda bisa mengambil bagiannya (.Date.Year) atau memformatnya (.Date.Format "2
  January 2006").

- .Summary: Ringkasan otomatis dari konten Anda. Hugo akan mengambil 70 kata pertama. Anda bisa menentukannya secara manual dengan variabel summary di
  front matter atau menggunakan <!--more--> di dalam konten Anda.

- .Description: Deskripsi dari front matter, berguna untuk SEO.

- .Permalink: URL lengkap ke halaman tersebut (misal: https://situsanda.com/posts/postingan-saya/).

- .RelPermalink: URL relatif ke halaman tersebut (misal: /posts/postingan-saya/). Ini lebih aman digunakan di template agar situs tetap berfungsi baik
  di-hosting di mana saja.

- .WordCount: Jumlah kata di dalam .Content.

- .ReadingTime: Perkiraan waktu baca dalam menit.

- .Draft: Nilai true atau false dari front matter draft.

- .Weight: Nilai weight dari front matter untuk pengurutan manual.

- .Kind: Jenis halaman yang sedang dirender. Sangat penting untuk dipahami. Jenisnya bisa:

  - page: Halaman konten biasa (seperti postingan blog).

  - home: Halaman beranda.

  - section: Halaman daftar dari sebuah folder (misal: halaman /posts/).

  - taxonomy: Halaman daftar dari sebuah taksonomi (misal: halaman /tags/).

  - taxonomyTerm: Halaman daftar dari sebuah istilah taksonomi (misal: halaman /tags/hugo/).

- .Type: Tipe konten, biasanya nama folder tempat file berada.

- .Section: Nama seksi (folder) tempat konten berada.

- .Params: Ini adalah "kantong" khusus untuk semua variabel yang Anda buat sendiri di front matter. Misalnya, jika Anda punya thumbnail = "gambar.jpg"
  di front matter, Anda bisa memanggilnya dengan .Params.thumbnail.

- .Next, .Prev: Halaman berikutnya/sebelumnya berdasarkan urutan tanggal.

- .NextInSection, .PrevInSection: Halaman berikutnya/sebelumnya di dalam seksi yang sama.

---

## Variabel File (File Variables)

Variabel ini memberikan informasi tentang file fisik (.md) yang menjadi sumber halaman, diakses melalui .File. Ini sangat berguna di dalam archetype.

- .File.Path: Path lengkap file relatif dari folder content/ (misal: posts/postingan-pertama.md).

- .File.Dir: Direktori tempat file berada (misal: posts/).

- .File.BaseFileName: Nama file tanpa ekstensi (misal: postingan-pertama). Ini kemungkinan yang Anda maksud dengan `.Name`.

- .File.Ext: Ekstensi file (misal: md).

- .File.LogicalName: Nama file lengkap dengan ekstensi (misal: postingan-pertama.md).

- .File.UniqueID: Sebuah ID unik (hash MD5) dari path file, berguna untuk ID HTML yang dijamin tidak akan sama.

Jadi, di archetype Anda, {{ replace .File.ContentBaseName "-" " " | title }} menggunakan variabel dari .File untuk membuat judul secara otomatis dari
nama file.

---

## Variabel Situs (Site Variables)

Ini adalah variabel global yang bisa Anda akses dari halaman mana pun untuk mendapatkan informasi tentang keseluruhan situs. Variabel ini diakses
melalui .Site.

- .Site.Title: Judul situs Anda, dari hugo.toml.

- .Site.BaseURL: URL dasar situs Anda.

- .Site.Copyright: Teks hak cipta dari hugo.toml.

- .Site.Params: "Kantong" untuk semua variabel kustom yang Anda definisikan di bawah [params] dalam hugo.toml.

- .Site.Pages: Daftar semua halaman di situs Anda (termasuk halaman section, taksonomi, dll).

- .Site.RegularPages: Daftar yang lebih berguna, berisi hanya halaman konten biasa (semua postingan Anda, misalnya). Sering digunakan untuk membuat
  daftar "Semua Postingan".

- .Site.Sections: Daftar semua halaman seksi.

- .Site.Taxonomies: Objek yang berisi semua taksonomi Anda. Anda bisa mengakses daftar semua tag dengan .Site.Taxonomies.tags.

- .Site.LastChange: Objek tanggal kapan situs terakhir kali mengalami perubahan.

- .Site.Data: Untuk mengakses data dari folder /data Anda (misal: file JSON, TOML, atau YAML).

## Kesimpulan

- Jika Anda ingin data spesifik halaman (judul, konten, tanggal), gunakan .Title, .Content, .Date.

- Jika Anda ingin data kustom dari front matter, gunakan .Params.namaVariabelAnda.

- Jika Anda ingin data tentang file sumbernya (terutama di archetype), gunakan .File.BaseFileName.

- Jika Anda ingin data global situs (judul situs, daftar semua postingan), gunakan .Site.Title, .Site.RegularPages.

Pemahaman tentang tiga "sumber" data ini adalah kunci untuk menguasai sistem template Hugo.

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

