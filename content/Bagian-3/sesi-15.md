---
title: "Base Templates & Blocks"
weight: 15
---

## Apa itu Base Template?

Base Template (template dasar) adalah sebuah file layout tingkat tinggi yang bertindak sebagai **kerangka utama (master template)** untuk seluruh halaman website Anda. Alih-alih menulis kode HTML yang sama (seperti `<head>`, `<header>`, `<footer>`) di setiap file template (seperti `single.html`, `list.html`), kita menulisnya sekali saja di Base Template.

## Apa itu Block?

Block adalah **sebuah tempat atau area** di dalam Base Template yang dapat diisi dengan konten spesifik oleh template lainnya (seperti {{< bold >}} single.html {{< /bold >}} atau {{< bold >}} list.html {{< /bold >}}). Ini mirip dengan "lubang" atau "slot" yang bisa diisi dengan kode yang berbeda-beda tergantung halamannya.

## Mengapa Menggunakan Base Template & Block?

1.  **DRY (Don't Repeat Yourself) :** Hindari duplikasi kode. Ubah satu file, perubahannya berlaku untuk seluruh situs.

2.  **Modular :** Layout menjadi lebih terstruktur dan mudah dikelola.

3.  **Flexibel :** Kita bisa mendefinisikan konten default untuk sebuah block dan meng-override (menimpa)-nya hanya di halaman yang membutuhkan.

---

## Langkah-langkah Implementasi

**1. Membuat Struktur Folder**
Langkah pertama adalah membuat folder `_default` di dalam direktori `layouts` Anda. Jika belum ada, buatlah. Contohnya seperti di bawah ini :

```tree
- your-hugo-site/ | folder
    - content/ | folder
    - layouts/ | folder-open
        - _default/       <-- Folder ini | folder-open
            - baseof.html <-- File Base Template | fa-brands fa-html5 | magenta
            - list.html   <-- Template untuk halaman list | fa-brands fa-html5 | magenta
            - single.html <-- Template untuk halaman single (artikel) | fa-brands fa-html5 | magenta
    - .....
```

**2. Membuat Base Template {{< bold >}} baseof.html {{< /bold >}}**
Buat file dengan nama persis `baseof.html` di dalam folder `layouts/_default/`. File ini berisi struktur HTML dasar website Anda.

```html {title="html" wrap="true"}
<!-- layouts/_default/baseof.html -->
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Website Saya</title>
  </head>
  <body>
    <hr />
    <strong>Top of Baseof</strong>
    <hr />

    <!-- BLOCK MAIN: Ini adalah "slot" untuk konten utama -->
    {{ block "main" . }}
    <!-- Konten di sini adalah DEFAULT jika block "main" tidak diisi oleh template lain -->
    <p>Ini adalah konten default dari baseof.</p>
    {{ end }}

    <hr />
    <strong>Bottom of Baseof</strong>
    <hr />

    <!-- BLOCK FOOTER: "Slot" lain untuk footer -->
    {{ block "footer" . }}
    <br />
    <p>Ini adalah default baseof footer.</p>
    {{ end }}
  </body>
</html>
```

**3. Membuat Template untuk Halaman Spesifik**
Sekarang, kita akan membuat template yang "mewarisi" kerangka dari `baseof.html` dan mengisi `block` yang telah disediakan.

**a. Template untuk Halaman Single (Artikel)**

```html {title="html" wrap="true"}
<!-- layouts/_default/single.html -->
{{ define "main" }}
<!-- Kode ini akan masuk ke dalam block "main" di baseof.html -->
<h1>Ini adalah Template untuk Halaman Single</h1>
<article>{{ .Content }}</article>
{{ end }} {{ define "footer" }}
<!-- Kita bahkan bisa override block "footer" khusus untuk halaman single -->
<p>Ini adalah footer khusus untuk halaman Single.</p>
{{ end }}
```

**b. Template untuk Halaman List (Daftar Artikel)**

```html {title="html" wrap="true"}
<!-- layouts/_default/list.html -->
{{ define "main" }}
<!-- Kode ini akan masuk ke dalam block "main" di baseof.html -->
<h1>Ini adalah Template untuk Halaman List</h1>
<ul>
  {{ range .Pages }}
  <li><a href="{{ .Permalink }}">{{ .Title }}</a></li>
  {{ end }}
</ul>
{{ end }}
```

> [!note] **Perhatikan**
>
> Template `list.html` **tidak** mendefinisikan block "footer".
> Sehingga akan menggunakan footer **default** dari `baseof.html`.

---

## Hasil yang Akan Ditampilkan

Dengan konfigurasi di atas:

1.  **Jika Anda membuka halaman List (e.g., homepage):**

    - Browser akan menampilkan:

      ```plaintext
      Top of Baseof
      [Konten dari list.html: "Ini adalah Template untuk Halaman List", dan daftar artikel]
      Bottom of Baseof
      [Footer default dari baseof.html: "Ini adalah default baseof footer."]
      ```

2.  **Jika Anda membuka halaman Single (e.g., sebuah artikel):**

    - Browser akan menampilkan:

      ```plaintext
      Top of Baseof
      [Konten dari single.html: Judul artikel dan isi kontennya]
      Bottom of Baseof
      [Footer khusus dari single.html: "Ini adalah footer khusus untuk halaman Single."]
      ```

---

## Kesimpulan

- **`baseof.html`** adalah **inti** dari struktur layout situs Anda.

- **`block`** adalah **placeholder** yang dapat diisi oleh template lain.

- **`define`** digunakan di dalam template anak (seperti `single.html`) untuk **mengisi** sebuah block.

- Kelebihan utama sistem ini adalah **kekuatan dan fleksibilitasnya**. Anda dapat memiliki elemen default yang konsisten di seluruh situs, tetapi tetap memiliki kebebasan untuk mengubahnya pada halaman-halaman tertentu sesuai kebutuhan.

Dengan menggunakan Base Templates dan Blocks, organisasi layout website Hugo Anda akan menjadi jauh lebih rapi, powerful, dan mudah dikembangkan.

