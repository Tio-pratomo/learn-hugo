---
Title: "Membuat Proyek Baru Dan Strukturnya"
Weight: 3
---

Sekarang, kita akan membuat situs web Hugo pertama kita dan mengenal struktur folder yang dibuat secara otomatis. Memahami struktur ini adalah langkah penting untuk mulai bekerja dengan Hugo.

## **1. Membuat Situs Baru**

Untuk membuat situs Hugo baru, kita akan menggunakan terminal atau _command line_. Pastikan Anda sudah membuka terminal di folder tempat Anda ingin menyimpan proyek Anda. Misalnya, jika Anda ingin menyimpan semua proyek Hugo di folder bernama `HugoProjects`, buka terminal di dalam folder tersebut.

Perintah untuk membuat situs Hugo baru sangat sederhana:

```bash {title="bash"}
hugo new site <nama-situs-anda>
```

- **`hugo`** : Perintah utama untuk berinteraksi dengan Hugo.

- **`new site`** : Sub-perintah yang memberitahu Hugo untuk membuat situs baru.

- **`<nama-situs-anda>`** : Ganti ini dengan nama yang Anda inginkan untuk situs Anda. Misalnya, `situs-pertama` atau `blog-saya`.

**Contoh:**

```bash {title="bash"}
hugo new site situs-pertama
```

Setelah menjalankan perintah ini, Anda akan melihat pesan yang berisi ucapan selamat, dan sebuah folder baru dengan nama `situs-pertama` akan muncul. Folder ini berisi semua file dan folder dasar yang dibutuhkan untuk situs Hugo.

## **2. Memahami Struktur Folder Dasar**

Saat Anda membuat situs Hugo baru, ia secara otomatis membuat beberapa folder dan file untuk Anda. Mari kita bahas fungsi dari masing-masing folder ini.

### **a. Folder `archetypes`**

- **Fungsi** : Folder ini berisi _template_ standar untuk jenis konten yang berbeda. Jika Anda membuat konten baru (misalnya, postingan blog), Hugo akan menggunakan _template_ di sini untuk menambahkan informasi standar secara otomatis (seperti tanggal, penulis, dll.).

- **Contoh Penggunaan** : Anda bisa mendefinisikan _metadata_ umum seperti `author` atau `language` di sini, sehingga setiap kali Anda membuat postingan baru, data tersebut sudah terisi.

### **b. Folder `content`**

- **Fungsi** : Ini adalah folder paling penting karena di sinilah semua konten situs Anda disimpan.

- **Contoh Penggunaan** : Semua postingan blog, halaman "Tentang Kami", atau halaman lainnya yang Anda buat akan disimpan di sini, biasanya dalam format **Markdown** (`.md`).

### **c. Folder `data`**

- **Fungsi** : Bertindak sebagai "database" sederhana untuk situs statis Anda. Anda bisa menyimpan file data (seperti JSON, YAML, atau TOML) di sini.

- **Contoh Penggunaan** : Anda bisa menyimpan daftar anggota tim, portofolio, atau informasi lain yang terstruktur dalam file data, lalu menampilkannya di situs Anda.

### **d. Folder `layouts`**

- **Fungsi** : Berisi _template_ HTML yang mendefinisikan struktur atau tata letak halaman situs Anda.

- **Contoh Penggunaan** : Anda bisa membuat _template_ untuk header, footer, atau tata letak postingan blog yang akan digunakan di seluruh situs, sehingga Anda tidak perlu menulis kode yang sama berulang kali.

### **e. Folder `static`**

- **Fungsi** : Untuk menyimpan semua aset statis yang tidak berubah di situs Anda.

- **Contoh Penggunaan** : Gambar, file CSS, file JavaScript, dan file font disimpan di folder ini.

### **f. Folder `themes`**

- **Fungsi** : Hugo sangat fleksibel karena mendukung tema yang dibuat oleh komunitas. Folder ini adalah tempat Anda menyimpan tema yang Anda unduh.

- **Contoh Penggunaan** : Anda bisa mengunduh tema gratis dari [situs tema Hugo](https://themes.gohugo.io/) dan menyimpannya di sini.

#### **g. File `config.toml` (atau `config.yaml` atau `config.json`)**

- **Fungsi** : Ini adalah file konfigurasi utama situs Anda. Anggap saja sebagai "pusat pengaturan" situs Hugo Anda.

- **Contoh Penggunaan** : Di sini Anda bisa mengatur judul situs, bahasa, URL dasar, dan berbagai opsi lainnya.

---

Meskipun ada banyak folder, jangan merasa kewalahan. Untuk memulai, Anda hanya perlu fokus pada folder **`content`** (untuk menulis) dan folder **`themes`** (untuk tampilan). Seiring berjalannya waktu, Anda akan semakin akrab dengan folder-folder lainnya.
