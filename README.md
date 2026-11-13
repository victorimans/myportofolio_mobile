Nama : Victoriano Iman Santosa
NPM : 2506544353
Kelas : PBP B

## AI disclosure Tugas 7

AI digunakan untuk membantu menyusun dan merapikan penjelasan jawaban. Daftar widget dan contoh penggunaannya disesuaikan dengan kode proyek pada `lib/main.dart` dan `lib/menu.dart`, lalu perlu ditinjau kembali oleh mahasiswa.

- [Sesi Menjawab Pertanyaan Tugas 7](<docs\AI Disclosure\Tugas 6\session-34e868b5-09bb-4a09-9c1d-734f1500ed4a.md>)

## Tugas 7
# Soal : 
1. Jelaskan apa yang dimaksud dengan widget tree pada Flutter dan bagaimana hubungan induk-anak (parent-child) bekerja antar-widget!

2. Sebutkan semua widget yang kamu gunakan dalam proyek ini dan jelaskan fungsinya masing-masing!

3. Apa fungsi dari widget MaterialApp? Jelaskan mengapa widget ini umumnya digunakan sebagai root widget pada aplikasi Flutter!

4. Jelaskan perbedaan antara StatelessWidget dan StatefulWidget! Kapan kita sebaiknya memilih StatelessWidget dan kapan harus menggunakan StatefulWidget?

5. Apa itu BuildContext dan mengapa penting di Flutter? Bagaimana penggunaannya di dalam metode build?

6. Jelaskan konsep hot reload di Flutter dan apa perbedaannya dengan hot restart! Kapan kita tidak bisa hanya mengandalkan hot reload dan harus melakukan hot restart atau full restart?

# Jawaban :

1. Widget tree adalah susunan widget yang membentuk antarmuka aplikasi Flutter. Setiap widget dapat menjadi induk (parent) bagi satu atau beberapa widget anak (child). Induk menentukan bagaimana anak disusun, diberi batasan ukuran, atau diberi gaya; anak mengisi bagian antarmuka yang ditentukan induknya. Contohnya, pada halaman ini `Scaffold` menjadi induk untuk `AppBar` dan `body`, lalu `Padding` membungkus `Column`, dan `Column` berisi widget-widget seperti `Row`, `Center`, dan `Text`. Struktur ini disusun secara deklaratif di dalam metode `build`.

2. Berikut widget yang digunakan di `lib/main.dart` dan `lib/menu.dart`:

- `MyApp`: widget kustom sekaligus titik awal pohon antarmuka; mengembalikan `MaterialApp`.
- `MaterialApp`: menyediakan konfigurasi dasar aplikasi Material, seperti tema dan halaman awal.
- `MyHomePage`: widget kustom yang menyusun halaman utama portofolio.
- `Scaffold`: kerangka halaman, termasuk area app bar dan body.
- `AppBar`: menampilkan bilah atas dengan judul `MyPortfolio`.
- `Text`: menampilkan judul, sambutan, informasi profil, dan pesan pada snackbar.
- `Padding`: memberi jarak di sekeliling konten atau anaknya.
- `Column`: menyusun anak-anak secara vertikal.
- `Row`: menyusun kartu informasi secara horizontal.
- `InfoCard`: widget kustom untuk menampilkan judul dan isi informasi (NPM, nama, dan kelas) dalam kartu.
- `SizedBox`: memberi jarak kosong dengan ukuran tertentu.
- `Center`: menempatkan konten anak di tengah.
- `GridView.count`: menyusun daftar item menu ke dalam kisi dengan jumlah kolom tertentu.
- `ItemCard`: widget kustom yang menampilkan satu item menu sebagai kartu yang dapat ditekan.
- `Card`: memberi tampilan kartu pada informasi profil.
- `Container`: menjadi wadah untuk mengatur ukuran, padding, dan tata letak konten.
- `Material`: menyediakan permukaan Material berwarna dan sudut membulat bagi kartu menu.
- `InkWell`: membuat kartu menu merespons ketukan dan menjalankan aksi `onTap`.
- `Icon`: menampilkan ikon sesuai item menu.
- `SnackBar`: menampilkan pesan sementara setelah kartu menu ditekan.

`ItemHomepage` adalah kelas model data untuk menyimpan nama, ikon, dan warna item menu, bukan widget. Hal-hal seperti `ThemeData`, `TextStyle`, `MediaQuery`, `ScaffoldMessenger`, `EdgeInsets`, dan `Colors` juga dipakai dalam kode, tetapi bukan widget; semuanya merupakan konfigurasi, utilitas, atau data pendukung widget.

3. Fungsi `MaterialApp` adalah widget tingkat atas yang menyiapkan struktur dan fitur umum aplikasi dengan desain Material. Pada proyek ini, `MaterialApp` mengatur judul aplikasi, tema warna dan Material 3, serta halaman awal melalui properti `home: MyHomePage()`. Widget ini umum dijadikan root karena menyediakan konfigurasi yang dibutuhkan halaman-halaman di bawahnya, termasuk tema dan layanan navigasi, serta menjadi konteks aplikasi bagi widget turunannya.

4. `StatelessWidget` tidak memiliki state internal yang dapat berubah selama widget hidup. Tampilan dibangun dari konfigurasi yang diberikan, sehingga cocok untuk bagian UI yang relatif tetap. `MyApp`, `MyHomePage`, `InfoCard`, dan `ItemCard` dalam proyek ini adalah `StatelessWidget`.

`StatefulWidget` memiliki objek `State` terpisah yang dapat menyimpan data yang berubah. Saat state berubah—biasanya melalui `setState`—Flutter membangun ulang bagian UI yang terkait. Gunakan `StatefulWidget` ketika tampilan perlu berubah akibat interaksi atau perubahan data, misalnya penghitung, formulir, atau pilihan menu yang tersimpan. Jika widget hanya menampilkan data tanpa mengelola perubahan state sendiri, pilih `StatelessWidget`.

5. `BuildContext` adalah referensi ke lokasi suatu widget di dalam widget tree. Flutter menggunakannya untuk menemukan informasi atau layanan yang tersedia dari widget-widget leluhur. Parameter `BuildContext context` tersedia di metode `build` dan dapat dipakai, misalnya, untuk mengambil warna tema dengan `Theme.of(context)` pada `MyHomePage`, membaca ukuran layar melalui `MediaQuery.of(context)` pada `InfoCard`, atau menemukan `ScaffoldMessenger` untuk menampilkan `SnackBar` pada `ItemCard`. Karena konteks bergantung pada posisi widget di tree, konteks yang digunakan harus berada pada bagian tree yang menyediakan layanan tersebut.

6. Hot reload menerapkan perubahan kode Dart ke aplikasi yang sedang berjalan dan membangun ulang UI tanpa menghapus state yang sedang tersimpan. Ini berguna untuk melihat perubahan tampilan dengan cepat. Hot restart memulai ulang kode Dart dari awal sehingga state aplikasi di memori direset, tetapi proses aplikasi host tetap berjalan.

Hot reload tidak selalu cukup, misalnya ketika perubahan mengharuskan `main()` atau `initState()` dijalankan ulang, mengubah inisialisasi global atau struktur state yang tidak dapat dipertahankan, atau mengubah kode native. Untuk kasus terkait inisialisasi/state, lakukan hot restart. Jika mengubah kode native Android/iOS atau konfigurasi/plugin native yang memerlukan pembangunan ulang, hentikan lalu jalankan aplikasi kembali (full restart/rebuild); hot restart saja tidak memuat ulang kode native.