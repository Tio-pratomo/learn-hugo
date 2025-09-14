---
title: "Memahami Section Templates"
weight: 14
---

Hugo memiliki tiga jenis _template_ dasar yang digunakan untuk mengontrol tampilan konten:

1.  {{< bold >}} Single Templates : {{< /bold >}} Untuk menampilkan satu halaman konten (misalnya, sebuah posting blog).

2.  {{< bold >}} List Templates : {{< /bold >}} Untuk menampilkan daftar beberapa halaman (misalnya, halaman yang menampilkan semua posting blog).

3.  {{< bold >}} Homepage Template : {{< /bold >}} Template khusus untuk halaman beranda (homepage) situs Anda.

Secara _default_, template-template ini diletakkan dalam folder {{< bold >}} layouts/\_default/ {{< /bold >}} . Namun, bagaimana jika kita ingin beberapa bagian {{< bold >}} sections {{< /bold >}} di website kita memiliki tampilan yang berbeda?

Di sinilah **Section Templates** berperan.

---

## Konsep Dasar: Folder `_default`

Biasanya, semua layout untuk halaman single dan list disimpan di:

```tree
- layouts/ | folder
    - _default/ | folder-open
        - list.html     <-- Template untuk daftar halaman | fa-brands fa-html5 | magenta
        - single.html   <-- Template untuk satu halaman | fa-brands fa-html5 | magenta
```

File-file dalam folder {{< bold >}} \_default {{< /bold >}} ini akan digunakan oleh Hugo untuk menampilkan semua halaman yang tidak memiliki template khusus.

## Contoh Struktur Konten:

```tree
- content/ | folder
    - a.md            <-- Halaman di root | fa-brands fa-markdown | magenta
    - directory1/     <-- Ini adalah sebuah 'section' | folder-open
        - b.md | fa-brands fa-markdown | magenta
        - c.md | fa-brands fa-markdown | magenta
```

Dengan setup {{< bold >}} \_default {{< /bold >}}, semua file (`a.md`, `b.md`, `c.md`) akan menggunakan template yang sama, yaitu {{< bold >}} layouts/\_default/single.html {{< /bold >}}.

---

## Apa itu Section Templates?

**Section Templates** adalah template yang dibuat khusus untuk {{< bold >}} _section_ {{< /bold >}} tertentu. {{< bold >}} _Section_ {{< /bold >}} dalam Hugo pada dasarnya adalah setiap folder yang berada langsung di bawah folder `content/` (contoh: `content/directory1/` adalah sebuah _section_).

Dengan membuat template di folder yang namanya sama dengan _section_, kita bisa meng-override template _default_ hanya untuk halaman-halaman yang ada di dalam _section_ tersebut.

---

## Langkah-langkah Membuat Section Template

**1. Identifikasi Nama Section**
Lihat di folder `content/`. Nama folder di dalamnya adalah nama {{< bold >}}_section_{{< /bold >}}. Sebagai contoh, namanya adalah `directory1`.

**2. Buat Folder Section di Layouts**
Buat folder baru di dalam `layouts/` dengan nama yang **persis** sama dengan nama _section_-nya.

- **Lokasi Asal:** `layouts/_default/single.html`
- **Lokasi Baru (Override):** `layouts/directory1/single.html`

Strukturnya akan menjadi seperti ini:

```tree
- layouts/ | folder
    - _default/ | folder-open
        - single.html  <-- Template default untuk semua halaman | fa-brands fa-html5 | magenta
    - directory1/      <-- Folder section khusus | folder-open
        - single.html  <-- Template khusus hanya untuk halaman di dalam content/directory1/ | fa-brands fa-html5 | magenta
```

**3. Buat File Template di Dalam Folder Section**

Buat file template di dalam folder section yang baru Anda buat. Anda bisa membuat `single.html`, `list.html`, atau keduanya.

**Contoh Isi `layouts/directory1/single.html`:**

```html {title="html" wrap="true"}
<!-- Template khusus untuk section 'directory1' -->
<!DOCTYPE html>
<html>
  <head>
    <title>Halaman Section</title>
  </head>
  <body>
    <h1>Ini adalah template khusus untuk section 'directory1'</h1>
    <!-- Untuk menampilkan konten dari file .md -->
    <article>{{ .Content }}</article>
  </body>
</html>
```

**4. Verifikasi Perubahan**
Setelah menyimpan file, jalankan atau refresh server Hugo Anda.

- Halaman `a.md` (yang ada di root `content/`) akan **tetap menggunakan** template default: `layouts/_default/single.html`.

- Halaman `b.md` dan `c.md` (yang ada di dalam `content/directory1/`) sekarang akan **menggunakan** template khusus: `layouts/directory1/single.html`.

---

## Kesimpulan dan Manfaat

- **Kontrol Penuh :** Section Templates memberi Anda kontrol lebih untuk membuat layout yang berbeda untuk bagian yang berbeda pada website (misalnya, layout berbeda untuk halaman "Blog", "Portfolio", dan "Tutorial").

- **Organisasi yang Lebih Baik :** Kode template menjadi lebih terorganisir karena dikelompokkan berdasarkan sectionnya.

- **Prioritas :** Hugo secara otomatis akan memprioritaskan template di folder section daripada template di folder `_default`.

Dengan memanfaatkan Section Templates, Anda dapat meningkatkan kompleksitas dan organisasi website Hugo Anda tanpa perlu menulis kode yang rumit.

