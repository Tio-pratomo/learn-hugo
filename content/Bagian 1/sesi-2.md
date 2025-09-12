---
Title: "Instalasi"
Weight: 2
---

## **Instalasi Hugo: Panduan untuk Berbagai OS**

Hugo adalah program tunggal (binary) yang bisa Anda unduh dan jalankan langsung. Tidak ada banyak ketergantungan (dependencies) yang perlu diinstal, membuat prosesnya sangat sederhana dan cepat.

**Untuk instalasi, sangat disarankan untuk mengunduh versi extended**. Versi ini mencakup fitur tambahan untuk memproses Sass/SCSS, yang sering digunakan oleh banyak tema Hugo. Menggunakan versi ini akan memastikan kompatibilitas yang lebih baik dan menghindari masalah di kemudian hari.

**Anda bisa menemukan semua file instalasi di halaman rilis Hugo di GitHub: [https://github.com/gohugoio/hugo/releases](https://github.com/gohugoio/hugo/releases)**

Tinggal pilih file instalasi sesuai OS yang kamu gunakan.

### **1. Menginstal di Windows**

Ada dua cara utama untuk menginstal Hugo di Windows:

**Cara 1: Menggunakan Manajer Paket (Paling Direkomendasikan)**

Gunakan manajer paket seperti **Chocolatey** atau **Scoop** untuk instalasi yang otomatis dan mudah.

- **Jika menggunakan Chocolatey**: Buka PowerShell atau Command Prompt sebagai Administrator, lalu jalankan perintah ini:
  ```bash {title="bash"}
  choco install hugo-extended -confirm
  ```
- **Jika menggunakan Scoop**: Buka PowerShell dan jalankan perintah ini:
  ```bash {title="bash"}
  scoop install hugo-extended
  ```

Manajer paket akan mengunduh dan menginstal Hugo versi **extended** serta menambahkannya ke PATH lingkungan Anda.

**Cara 2: Menginstal Manual**

1.  Kunjungi halaman rilis Hugo di GitHub dan unduh file `.zip` versi **extended** yang sesuai dengan sistem Anda (misalnya, `hugo_extended_0.xx.x_Windows-64bit.zip`).
2.  Ekstrak file `.zip` tersebut. Anda akan menemukan file `hugo.exe`.
3.  Pindahkan `hugo.exe` ke folder khusus untuk program Anda, seperti `C:\Hugo\bin`.
4.  Tambahkan folder ini (`C:\Hugo\bin`) ke **PATH lingkungan** Windows Anda. Ini akan memungkinkan Anda menjalankan perintah `hugo` dari terminal mana saja.

**Cara Mengecek Instalasi:**
Buka terminal (Command Prompt atau PowerShell) dan ketik:

```bash {title="bash"}
hugo version
```

Jika instalasi berhasil, akan muncul versi Hugo yang terinstal, dan Anda akan melihat kata "extended" di sana.

### **2. Menginstal di macOS**

Cara paling mudah dan direkomendasikan adalah menggunakan Homebrew.

1.  Pastikan Anda sudah menginstal [Homebrew](https://brew.sh/).
2.  Buka terminal dan jalankan perintah ini:

    ```bash {title="bash"}
    brew install hugo
    ```

Homebrew akan secara otomatis menginstal versi **extended** secara _default_.

### **3. Menginstal di Linux**

Di Linux, Anda bisa menggunakan manajer paket bawaan sistem Anda. Versi yang diinstal biasanya sudah **extended**.

- **Debian/Ubuntu**:
  ```bash {title="bash"}
  sudo apt install hugo
  ```
- **Arch Linux**:
  ```bash {title="bash"}
  sudo pacman -S hugo
  ```
- **Fedora**:
  ```bash {title="bash"}
  sudo dnf install hugo
  ```

Setelah instalasi berhasil, Anda sudah siap untuk mulai membuat situs web pertama Anda dengan Hugo\!
