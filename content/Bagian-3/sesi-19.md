---
title: "Memahami Data Files di Hugo"
weight: 19
---

## Konsep Dasar Data Folder

**Data folder** dalam Hugo berfungsi sebagai "mini database" untuk website Anda. Folder ini digunakan untuk menyimpan data yang akan digunakan di berbagai bagian website, terpisah dari konten utama.

**Lokasi**: `/data/` di root directory project Hugo Anda

## Format File yang Didukung

Hugo mendukung tiga format file untuk data files:

| Format | Ekstensi            | Keterangan                      |
| ------ | ------------------- | ------------------------------- |
| JSON   | `.json`             | JavaScript Object Notation      |
| YAML   | `.yaml` atau `.yml` | YAML Ain't Markup Language      |
| TOML   | `.toml`             | Tom's Obvious, Minimal Language |

## Membuat Data File Pertama

### Contoh File JSON (states.json):

```json
[
  {
    "name": "California",
    "capital": "Sacramento",
    "lat": 38.5556,
    "long": -121.4689
  },
  {
    "name": "New York",
    "capital": "Albany",
    "lat": 42.6525,
    "long": -73.7572
  }
]
```

### Contoh File YAML (states.yaml):

```yaml
- name: California
  capital: Sacramento
  lat: 38.5556
  long: -121.4689
- name: New York
  capital: Albany
  lat: 42.6525
  long: -73.7572
```

## Mengakses Data di Template

### Menggunakan Range untuk Iterasi Data

```go-html-template
{{ range site.Data.states }}
  <div class="state">
    <h3>{{ .name }}</h3>
    <p>Ibu Kota: {{ .capital }}</p>
    <p>Koordinat: {{ .lat }}, {{ .long }}</p>
  </div>
{{ end }}
```

**Penjelasan Kode:**

- `site.Data.states`: Mengakses file `states.json` atau `states.yaml` di folder `/data/`

- `range`: Melooping melalui setiap item dalam array

- `.name`, `.capital`: Mengakses properti dari setiap objek

## Struktur Folder yang Lebih Kompleks

{{< bold >}}Anda dapat mengorganisir data dalam subfolder :{{< /bold >}}

```tree
- /data/ | folder
    - locations/ | folder-open
        - states.json | file-code | magenta
        - cities.yaml | file-code | magenta
    - team/ | folder-open
        - members.toml | file-code | magenta
```

{{< bold >}}Cara mengaksesnya :{{< /bold >}}

```go-html-template
{{ range site.Data.locations.states }}
  <!-- Konten di sini -->
{{ end }}

{{ range site.Data.team.members }}
  <!-- Konten di sini -->
{{ end }}
```

## 6. Contoh Praktis: Menampilkan Data Tim

### File: `/data/team/members.yaml`

```yaml
- name: John Doe
  position: Developer
  social:
    twitter: johndoe
    github: johndoe
- name: Jane Smith
  position: Designer
  social:
    instagram: janesmith
    dribbble: janesmith
```

### Template:

```go-html-template
<section class="team">
  <h2>Tim Kami</h2>
  <div class="team-grid">
    {{ range site.Data.team.members }}
      <div class="team-member">
        <h3>{{ .name }}</h3>
        <p>{{ .position }}</p>
        <div class="social-links">
          {{ with .social.twitter }}
            <a href="https://twitter.com/{{ . }}">Twitter</a>
          {{ end }}
          {{ with .social.github }}
            <a href="https://github.com/{{ . }}">GitHub</a>
          {{ end }}
        </div>
      </div>
    {{ end }}
  </div>
</section>
```

## 7. Menggunakan Data dengan Parameter

Anda dapat menggabungkan data files dengan parameter dari front matter:

```go-html-template
{{ $featuredState := .Params.featured_state }}
{{ range site.Data.states }}
  {{ if eq .name $featuredState }}
    <div class="featured-state">
      <h2>Featured: {{ .name }}</h2>
      <p>Capital: {{ .capital }}</p>
    </div>
  {{ end }}
{{ end }}
```

## 8. Best Practices

1. **Gunakan format yang paling nyama** untuk Anda (JSON, YAML, atau TOML)
2. **Organisir dengan subfolder** jika memiliki banyak data files
3. **Gunakan nama file yang deskriptif** dan konsisten
4. **Pisahkan data berdasarkan jenis** (contoh: team, products, locations)
5. **Validasi struktur data** sebelum digunakan di template

## 9. Error Handling

Selalu periksa jika data tersedia sebelum menggunakannya:

```go-html-template
{{ if site.Data.states }}
  {{ range site.Data.states }}
    <!-- Konten di sini -->
  {{ end }}
{{ else }}
  <p>Data tidak tersedia saat ini.</p>
{{ end }}
```

## 10. Contoh Lanjutan: Data Bersarang (Nested)

### File: `/data/settings.yaml`

```yaml
website:
  name: "My Hugo Site"
  description: "Sebuah website built dengan Hugo"
  social:
    twitter: "myhugosite"
    facebook: "myhugosite"
```

### Cara Mengakses:

```go-html-template
{{ $settings := site.Data.settings }}
<h1>{{ $settings.website.name }}</h1>
<p>{{ $settings.website.description }}</p>

{{ with $settings.website.social }}
  <a href="https://twitter.com/{{ .twitter }}">Twitter</a>
  <a href="https://facebook.com/{{ .facebook }}">Facebook</a>
{{ end }}
```

## 11. Tips Performa

1. **Hugo meng-cache data files** secara otomatis untuk performa
2. **Data files di-process saat build time**, tidak mempengaruhi kecepatan loading website
3. **Gunakan partial caching** untuk data yang kompleks dengan `partialCached`

```go-html-template
{{ partialCached "team-list.html" . }}
```

