<p align="center">
  <a href="https://github.com/JawaTengahXploit1337/AutoSSH" alt="AutoSSH">
    <img src="image.png" alt="AutoSSH">
  </a>
</p>

# Deskripsi

*AutoSSH adalah script Bash sederhana untuk menjaga koneksi SSH tetap aktif dengan fitur auto-reconnect. Jika koneksi terputus, script akan otomatis mencoba menghubungkan kembali ke server. Tools ini dirancang untuk jaringan tidak stabil, memberikan animasi visual progres, dan user-friendly dengan input fleksibel untuk username dan hostname.*

# Installation

```bash
wget https://raw.githubusercontent.com/JawaTengahXploit1337/AutoSSH/main/autossh.sh -O /usr/local/bin/autossh
```
# Usage

This usage is as same as `ssh` command but I suggest you use SSH aliases instead of IP, for example

```bash
autossh root@prod-server
```
Or you can enter to interactive mode by just use it without any paramters

```bash
autossh
```
It will ask you to enter SSH Username and SSH IP/Aliases.

Reference to SSH aliases, please take a look to [this guide](https://coderwall.com/p/dou7uw/multiple-aliases-on-every-entry-of-ssh-s-config-file).

SC : [dulldusk](https://github.com/dulldusk/autossh)

Script yang Anda berikan adalah **tool berbasis Bash** untuk membuat sesi **SSH (Secure Shell) yang berfungsi secara otomatis reconnect** jika koneksi terputus. Berikut adalah penjelasan lebih mendalam tentang cara kerja dan fungsinya:

---

### **Fungsi dan Tujuan Script**
1. **Auto-reconnect SSH**  
   - Script ini mencoba untuk menjaga sesi SSH tetap hidup (persistent). Jika sesi SSH ke server tertentu terputus, script secara otomatis akan mencoba menghubungkan kembali ke server.

2. **User Input untuk Detail Koneksi SSH**  
   - Pengguna akan diminta untuk memberikan:
     - **Username SSH** (misalnya, `root`)
     - **IP Address/Hostname SSH** (misalnya, `192.168.1.100`)
   - Data ini disimpan dalam history untuk mempermudah penggunaan berikutnya.

3. **Visualisasi Progres dengan Animasi**  
   - Script memberikan animasi sederhana saat mencoba menghubungkan ke server, seperti **titik-titik (#)** atau **progress bar** untuk memberi umpan balik visual kepada pengguna.

4. **Pengecekan Status Koneksi**  
   - Script memantau apakah sesi SSH sudah aktif atau tidak:
     - Jika aktif, ia mencetak pesan **"I'm alive"**.
     - Jika tidak aktif, ia mencoba menyambung ulang ke server dan mencetak pesan **"I'm dead... God is bringing me back..."**.

---

### **Cara Kerja Script**

1. **Inisialisasi Variabel dan Pengaturan Warna**  
   - Script mendeteksi apakah terminal mendukung warna, lalu mengatur variabel warna seperti `RED`, `GREEN`, `BLUE`, dll., untuk digunakan dalam mencetak teks berwarna.

2. **Mendapatkan Data Input SSH**  
   - Jika data username atau IP server tidak diberikan sebagai parameter script, script akan meminta pengguna untuk memasukkan detail tersebut.

3. **Fungsi `auto_connect`**  
   - Fungsi inti yang terus berjalan untuk memantau sesi SSH:
     1. **Pengecekan Sesi Aktif**  
        - Menggunakan perintah `ps aux` untuk melihat apakah sesi SSH sudah berjalan.
     2. **Reconnect Otomatis**  
        - Jika sesi tidak ditemukan, script mencoba menyambungkan kembali menggunakan perintah `ssh`.

4. **Loop Tak Berujung**  
   - Fungsi utama script (`main`) memanggil fungsi `auto_connect`, yang berjalan dalam loop tanpa henti untuk terus memantau dan menjaga koneksi SSH tetap hidup.

---

### **Cara Menggunakan**
1. Simpan script dengan nama file, misalnya `autossh.sh`.
2. Berikan izin eksekusi:  
   ```bash
   chmod +x autossh.sh
   ```
3. Jalankan script:
   - Jika username dan IP belum diberikan:  
     ```bash
     ./autossh.sh
     ```
     Script akan meminta input username dan IP.
   - Jika username dan IP sudah diketahui, berikan sebagai parameter:  
     ```bash
     ./autossh.sh user@hostname
     ```
     Contoh:
     ```bash
     ./autossh.sh root@192.168.1.100
     ```

---

### **Kelebihan**
- **Reliabilitas Koneksi**: Sangat berguna untuk menjaga koneksi SSH tetap hidup pada jaringan yang tidak stabil.
- **User-Friendly**: Memberikan animasi dan pesan visual yang membantu pengguna memahami status koneksi.
- **Otomatis**: Tidak perlu memulai koneksi ulang secara manual jika terputus.

---

### **Potensi Pengembangan**
- **Parameter Opsional**: Menambahkan opsi seperti port SSH (`-p`) atau file kunci privat (`-i`).
- **Log Aktivitas**: Menyimpan log ke file untuk memantau waktu koneksi atau pemutusan.
- **Batas Waktu Reconnect**: Menambahkan opsi untuk membatasi jumlah upaya reconnect sebelum berhenti.

