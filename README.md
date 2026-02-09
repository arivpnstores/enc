# ENC — Shell Script Encrypter (bzip2 self-extracting)

`enc` adalah shell script untuk **meng-encrypt (membungkus)** dan **decrypt** file script (biasanya `.sh`) menggunakan metode **self-extracting wrapper** berbasis `bzip2`.

File hasil encrypt **tetap bisa dijalankan seperti biasa**, karena script akan mengekstrak dirinya sendiri ke `/tmp` lalu dieksekusi otomatis.

Repo:
https://github.com/arivpnstores/enc/blob/main/enc

---

## Fitur
- Encrypt file script dengan wrapper + kompresi `bzip2`
- Decrypt kembali file yang sudah di-encrypt
- Otomatis membuat backup file asli (`namafile~`)
- Menolak file dengan permission `setuid` / `setgid`
- Aman dari recursive dependency (bzip2, tail, sed, dll)

---

## Requirements
Pastikan tool berikut tersedia di sistem:
- sh
- bzip2
- tail
- sed
- chmod, ln, sleep, rm

Debian / Ubuntu:
```bash
apt update
apt install -y bzip2 coreutils sed
````

---

## Install

```bash
wget -O /usr/bin/enc https://raw.githubusercontent.com/arivpnstores/enc/main/enc
chmod +x /usr/bin/enc
```

Cek:

```bash
enc
```

---

## Cara Pakai

### Encrypt file

```bash
enc namafile.sh
```

Hasil:

* `namafile.sh` → versi encrypted
* `namafile.sh~` → backup file asli

---

### Decrypt file

```bash
enc -d namafile.sh
```

Atau:

```bash
ungzexe namafile.sh
```

---

## Cara Kerja Singkat

1. Script dibungkus dengan loader shell
2. Isi file dikompres menggunakan `bzip2`
3. Saat dijalankan, file akan:

   * Diekstrak ke `/tmp`
   * Diberi permission `700`
   * Dieksekusi
   * Dihapus otomatis setelah selesai

---

## Contoh

```bash
enc install.sh
./install.sh
enc -d install.sh
```

---

## Catatan Penting

* Ini **bukan enkripsi kriptografi** (tidak pakai password / AES)
* Tujuan utama: **obfuscation & proteksi ringan**
* Jangan gunakan untuk menyimpan secret sensitif

---

## Troubleshooting

### Error: cannot find tail

```bash
apt install -y coreutils
```

### File sudah terenkripsi

Script akan mendeteksi dan melewati file tersebut otomatis.

---

## Lisensi

Copyright © ARI (2024)
Digunakan untuk keperluan pribadi & edukasi.

```

