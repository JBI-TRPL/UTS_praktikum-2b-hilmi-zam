# Ujian Praktikum Flutter POS SQLite
**Nama Mahasiswa:** M. Hilmi Zamzami  
**NIM:** 362458302071  
**Kelompok:** 1

## Deskripsi Fitur yang Ditambahkan

* Ubah tampilan halaman login dengan background gradasi dan tombol berikon.
* Tambahkan konfirmasi “Apakah Anda yakin ingin keluar?” sebelum logout.

---

## Mengubah tampilan halaman login dengan background gradasi dan tombol berikon.

Implementasi ini berfokus pada estetika visual yang bersih dan fungsionalitas yang jelas untuk formulir autentikasi.

### 1. Latar Belakang Gradien (Background Gradasi)

Latar belakang halaman diimplementasikan menggunakan widget `Container` yang dilengkapi dengan dekorasi `BoxDecoration` dan properti `LinearGradient`.

- Tujuan: Memberikan kedalaman visual dan nuansa profesional.
- Arah: Gradien diterapkan dari atas ke bawah (Top-to-Bottom).
- Warna: Transisi dari Biru Muda (`#2196F3`) menuju Biru Tua (`#1976D2`).

### 2. Tombol Berikon untuk Aksi Utama

Semua tombol penting disajikan dengan ikon untuk meningkatkan pemahaman visual dan aksesibilitas. Menggunakan konstruktor `*Button.icon()`.

- Tombol Login
  - Tipe: `ElevatedButton.icon`
  - Ikon: `Icons.login`
  - Fungsi: Aksi utama untuk masuk

- Tombol Register
  - Tipe: `OutlinedButton.icon` / `TextButton.icon`
  - Ikon: `Icons.person_add`
  - Fungsi: Navigasi ke halaman pendaftaran

- Tombol Lupa Kata Sandi
  - Tipe: `TextButton.icon`
  - Ikon: `Icons.help_outline`
  - Fungsi: Navigasi ke bantuan atau reset password

## Cara Menambahkan Konfirmasi Logout

### Deskripsi
Menambahkan dialog konfirmasi saat user menekan tombol logout di AppBar untuk mencegah logout yang tidak disengaja. Implementasi berikut memastikan navigasi dilakukan setelah dialog ditutup (praktik yang lebih bersih).

### Kode (disesuaikan untuk program)
```dart
appBar: AppBar(
    title: Text('Dashboard - ${_currentUser.fullname}'),
    actions: [
        IconButton(
            icon: const Icon(Icons.logout),
            onPressed: () async {
                final shouldLogout = await showDialog<bool>(
                    context: context,
                    builder: (context) {
                        return AlertDialog(
                            title: const Text('Konfirmasi Logout'),
                            content: const Text('Apakah Anda yakin ingin keluar?'),
                            actions: [
                                TextButton(
                                    onPressed: () => Navigator.of(context).pop(false), // Batal
                                    child: const Text('Batal'),
                                ),
                                ElevatedButton(
                                    onPressed: () => Navigator.of(context).pop(true), // Konfirmasi
                                    child: const Text('Keluar'),
                                ),
                            ],
                        );
                    },
                );

                if (shouldLogout == true) {
                    // Navigasi setelah dialog ditutup
                    Navigator.pushReplacement(
                        context,
                        MaterialPageRoute(builder: (context) => const LoginScreen()),
                    );

                    // Atau, jika Anda memakai named routes:
                    // Navigator.pushReplacementNamed(context, '/login');
                }
            },
        ),
    ],
),
```

### Penjelasan singkat
- showDialog mengembalikan Future<bool?>; kita kembalikan true saat konfirmasi dan false saat batal.  
- Navigasi dilakukan setelah dialog ditutup (menghindari menumpuk Navigator calls dari dalam dialog).  
- Jika menggunakan named routes, gunakan pushReplacementNamed untuk konsistensi rute.

## Alur Kerja
- **User klik logout** → Dialog muncul
- **Pilih "Batal"** → Dialog tertutup, tetap di dashboard
- **Pilih "Keluar"** → Dialog tertutup, kembali ke login screen

## File yang dimodifikasi
- \lib\screens\auth\login_screen.dart → Mengubah background menjadi gradian dan tombol ber icon
- \lib\screens\home\home_screen.dart → Menbambahkan konfirmasi sebelum logout

