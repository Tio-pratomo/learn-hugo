---
title: "Memahami Shortcode Templates di Hugo"
weight: 21
---

## 1. Konsep Dasar Shortcode

**Shortcode** adalah snippet kode kecil yang dapat disisipkan dalam file markdown untuk menambahkan fungsionalitas khusus tanpa menulis HTML langsung. Mereka seperti "macro" yang memperluas kemampuan markdown.

**Mengapa menggunakan shortcode?**

- Menghindari HTML langsung di konten markdown
- Dapat digunakan kembali di berbagai konten
- Membuat konten lebih modular dan terorganisir
- Memisahkan logika presentasi dari konten

## 2. Struktur Folder Shortcode

```
layouts/
└── shortcodes/
    ├── myshortcode.html
    ├── highlight.html
    └── custom/
        └── banner.html
```

## 3. Membuat Shortcode Sederhana

### Basic shortcode tanpa parameter:

```html
<!-- layouts/shortcodes/myshortcode.html -->
<p>Ini adalah teks dari shortcode</p>
```

### Cara menggunakan di markdown:

```markdown
Ini adalah konten biasa.

{{</* myshortcode */>}}

Lanjutan konten setelah shortcode.
```

## 4. Shortcode dengan Parameter

### Named parameters:

```markdown
{{</* myshortcode color="blue" size="large" */>}}
```

### Positional parameters:

```markdown
{{</* myshortcode "blue" "large" */>}}
```

## 5. Mengakses Parameter di Shortcode

### Shortcode dengan named parameters:

```html
<!-- layouts/shortcodes/color-text.html -->
<p style="color: {{ .Get "color" }};">
  {{ .Inner }}
</p>
```

### Shortcode dengan positional parameters:

```html
<!-- layouts/shortcodes/color-text.html -->
<p style="color: {{ .Get 0 }}; font-size: {{ .Get 1 }};">{{ .Inner }}</p>
```

## 6. Paired Shortcode (Shortcode Berpasangan)

Shortcode yang membungkus konten:

```markdown
{{</* highlight color="yellow" */>}}
Teks ini akan disorot dengan warna kuning
dan **format markdown** akan diproses.
{{</* /highlight */>}}
```

```html
<!-- layouts/shortcodes/highlight.html -->
<div style="background-color: {{ .Get "color" }}; padding: 10px;">
  {{ .Inner | markdownify }}
</div>
```

## 7. Menangani Markdown dalam Shortcode

Gunakan `{{ .Inner | markdownify }}` untuk memproses markdown:

```html
<!-- layouts/shortcodes/note.html -->
<div class="note">{{ .Inner | markdownify }}</div>
```

**Catatan**: Untuk shortcode berpasangan yang memproses markdown, gunakan `%` bukan `<` dan `>`:

```markdown
{{%/* note */%}}
Ini adalah **teks penting** yang akan diproses sebagai markdown.
{{%/* /note */%}}
```

## 8. Contoh Praktis Shortcode

### Shortcode untuk gambar responsif:

```html
<!-- layouts/shortcodes/image.html -->
<figure>
  <img src="{{ .Get "src" }}" alt="{{ .Get "alt" }}" style="max-width: 100%; height: auto;"> {{ with .Get "caption" }}
  <figcaption>{{ . }}</figcaption>
  {{ end }}
</figure>
```

```markdown
{{</* image src="/images/contoh.jpg" alt="Deskripsi gambar" caption="Ini caption" */>}}
```

### Shortcode untuk embed video:

```html
<!-- layouts/shortcodes/youtube.html -->
<div class="video-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/{{ .Get 0 }}" frameborder="0" allowfullscreen> </iframe>
</div>
```

```markdown
{{</* youtube "dQw4w9WgXcQ" */>}}
```

## 9. Best Practices untuk Shortcode

1. **Gunakan nama yang deskriptif**

   - ✅ `image-responsive.html`
   - ❌ `sc1.html`

2. **Validasi parameter**

   ```html
   {{ if .Get "src" }} <img src="{{ .Get "src" }}"> {{ else }}
   <p>Error: Parameter src diperlukan</p>
   {{ end }}
   ```

3. **Sediakan parameter default**

   ```html
   {{ $color := .Get "color" | default "yellow" }}
   <div style="background-color: {{ $color }};">{{ .Inner }}</div>
   ```

4. **Dokumentasi parameter**
   ```html
   {{/* Shortcode: highlight Parameters: - color: Warna latar (default: yellow) */}}
   ```

## 10. Shortcode dengan Logika Kondisional

```html
<!-- layouts/shortcodes/alert.html -->
{{ $type := .Get "type" | default "info" }}
<div class="alert alert-{{ $type }}">{{ if eq $type "warning" }} ⚠️ {{ else if eq $type "danger" }} 🚫 {{ else }} ℹ️ {{ end }} {{ .Inner | markdownify }}</div>
```

```markdown
{{</* alert type="warning" */>}}
Ini adalah **peringatan penting**!
{{</* /alert */>}}
```

## 11. Tips Penting

1. **Gunakan backticks (`)** untuk atribut HTML untuk menghindari konflik quote:

   ```html
   <div style=`color: {{ .Get "color" }};`>
     {{ .Inner }}
   </div>
   ```

2. **Gunakan `partial` dalam shortcode** untuk komponen kompleks:

   ```html
   {{ partial "components/card.html" (dict "Title" (.Get "title") "Content" .Inner ) }}
   ```

3. **Test shortcode** dengan berbagai parameter

## 12. Error Handling

Selalu tangani kasus dimana parameter tidak disediakan:

```html
{{ if .Get "src" }} <img src="{{ .Get "src" }}" alt="{{ .Get "alt" }}"> {{ else }}
<p class="error">Error: Parameter 'src' diperlukan untuk shortcode ini</p>
{{ end }}
```

## 13. Contoh Shortcode Lengkap

```html
<!-- layouts/shortcodes/card.html -->
{{ $title := .Get "title" }} {{ $image := .Get "image" }} {{ $url := .Get "url" | default "#" }}

<div class="card">
  {{ with $image }}
  <img src="{{ . }}" class="card-img" />
  {{ end }}

  <div class="card-body">
    {{ with $title }}
    <h3>{{ . }}</h3>
    {{ end }}

    <div class="card-content">{{ .Inner | markdownify }}</div>

    <a href="{{ $url }}" class="btn">Baca selengkapnya</a>
  </div>
</div>
```

```markdown
{{</* card
  title="Judul Kartu"
  image="/images/contoh.jpg"
  url="/artikel-1"
*/>}}
Ini adalah **konten** kartu yang akan diproses sebagai markdown.
{{</* /card */>}}
```

## 14. Latihan Praktis

Coba buat shortcode untuk:

1. **Tombol** dengan warna custom
2. **Kutipan** dengan sumber dan gaya berbeda
3. **Galeri gambar** sederhana
4. **Embed tweet** atau konten sosial media

---

**Kesimpulan**:
Shortcode adalah fitur powerful Hugo yang memungkinkan:

- 🎨 **Fungsionalitas kustom** dalam markdown
- 🔁 **Reusability** - dapat digunakan berkali-kali
- 🧩 **Modularity** - memisahkan konten dari presentasi
- ⚡ **Efisiensi** - menghemat waktu untuk elemen umum

Dengan menguasai shortcode, Anda dapat membuat konten markdown yang lebih dinamis dan interaktif tanpa kehilangan kemudahan editing yang ditawarkan oleh format markdown.

