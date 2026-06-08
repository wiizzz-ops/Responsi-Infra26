# Analisis Perbaikan

Nama : Wisnu Satya Herlambang
NIM  : W1H024033
Shift : A

---

## Permasalahan 1

### Gejala
Docker Compose gagal dijalankan dengan pesan:

```
mapping values are not allowed in this context
```

### Penyebab
File `docker-compose.yml` memiliki kesalahan sintaks pada bagian `services` karena tidak diakhiri dengan tanda titik dua (`:`).

### Solusi
Menambahkan tanda titik dua (`:`) setelah `services` sehingga format YAML menjadi valid.

---

## Permasalahan 2

### Gejala
Docker Compose menampilkan pesan:

```
service "db" refers to undefined volume db-data
```

### Penyebab
Service database menggunakan volume `db-data`, tetapi volume yang didefinisikan bernama `database-data`.

### Solusi
Mengubah nama volume menjadi `db-data` agar sesuai dengan referensi yang digunakan oleh service database.

---

## Permasalahan 3

### Gejala
Proses build gagal dengan pesan:

```
path ./web33 not found
```

### Penyebab
Service `web3` menggunakan build context `./web33`, sedangkan folder yang tersedia adalah `./web3`.

### Solusi
Mengubah build context dari `./web33` menjadi `./web3`.

---

## Permasalahan 4

### Gejala
Build image web1 gagal.

### Penyebab
Dockerfile web1 menggunakan image yang salah:

```
FROM php:8.2-apach
```

### Solusi
Mengubah image menjadi:

```
FROM php:8.2-apache
```

---

## Permasalahan 5

### Gejala
Build image web3 gagal.

### Penyebab
Dockerfile web3 menggunakan image yang salah:

```
FROM php:8.2-apche
```

### Solusi
Mengubah image menjadi:

```
FROM php:8.2-apache
```

---

## Permasalahan 6

### Gejala
Container Nginx gagal berjalan.

### Penyebab
File `nginx.conf` masih mengandung syntax markdown berupa:

```nginx
```nginx
```

dan penutup:

```
```
```

yang dianggap sebagai konfigurasi oleh Nginx.

### Solusi
Menghapus seluruh syntax markdown sehingga file hanya berisi konfigurasi Nginx yang valid.

---

## Permasalahan 7

### Gejala
Container Nginx gagal dijalankan dengan pesan:

```
host not found in upstream "web11"
```

### Penyebab
Konfigurasi upstream menggunakan hostname `web11`, sedangkan service yang tersedia bernama `web1`.

### Solusi
Mengubah hostname dari `web11` menjadi `web1`.

---

## Permasalahan 8

### Gejala
Nginx gagal melakukan komunikasi dengan web3.

### Penyebab
Konfigurasi upstream menggunakan:

```
server web3:8080;
```

padahal service web3 berjalan pada port 80.

### Solusi
Mengubah konfigurasi menjadi:

```
server web3:80;
```

---

## Permasalahan 9

### Gejala
Container Nginx berhenti dengan pesan:

```
host not found in upstream "web3:80"
```

### Penyebab
Service web3 hanya terhubung ke network `backend`, sehingga tidak dapat diakses oleh Nginx yang berada pada network `frontend`.

### Solusi
Menambahkan web3 ke network `frontend` dan `backend`.

---

## Permasalahan 10

### Gejala
Identitas praktikan belum ditampilkan pada aplikasi.

### Penyebab
File aplikasi masih menggunakan placeholder:

```
ganti ke namamu
ganti ke nimmu
```

### Solusi
Mengganti placeholder dengan identitas praktikan:

Nama : Wisnu

NIM : W1H024033

pada seluruh web server.

---

## Hasil Akhir

Setelah seluruh perbaikan dilakukan:

- Seluruh container berhasil dijalankan menggunakan Docker Compose.
- Nginx berhasil berjalan sebagai load balancer.
- Aplikasi dapat diakses melalui port 8080.
- Load balancing berjalan menggunakan metode Round Robin.
- WEB-1, WEB-2, dan WEB-3 dapat diakses melalui Nginx.
- Seluruh service terhubung ke database yang sama.
- Identitas praktikan berhasil ditampilkan pada seluruh web server.
