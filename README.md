# Manajemen-Waktu-Mahasiswa
 ---
 ###  Nama : Maitasya Rohmatul Ula
 ###  NRP  : 5027251026
 ### Tugas : Class Diagram Strukdat
 ---
 ### Case: Sistem Prioritas Kegiatan Mahasiswa
 ####  Deskripsi Kasus 
 Sebagai mahasiswa, aku sering merasa  24 jam kurang deh karena banyaknya kegiatan yang harus dijalani. Dalam satu hari saja, aku bisa memiliki jadwal kuliah pagi sampai sore, atau kadang pagi kuliah dilanjutkan praktikum siang, lalu asistensi sore, dan malamnya masih harus join rapat organisasi atau UKM selain itu, kadang juga dikejar-kejar hantu perkuliahan. Ha?? Hantu perkuliahan? ets makausdnya deadline tugas. Belum lagi kalua ada demo project atau demo praktikum, pelatihan,seminar, atau acara departemen yang tiba-tiba muncul dan membuat jadwal semakin ambrul-adul dan padat.

Awalnya tidak masalah sih tapi lambat laut masalah mulai terasa ketika beberapa kegiatan memiliki waktu yang bertabrakan, misalnya jadwal praktikum yang bentrok dengan deadline tugas yang berdekatan dengan jadwal demo project. Aku sering kebingungan menentukan kegiatan mana yang harus diprioritaskan terlebih dahulu, terutama ketika semua kegiatan terasa sama pentingnya. Akibatnya, ada tugas yang terlambat dikerjakan atau kegiatan yang terlewat karena tidak tercatat dengan baik.

Selain itu, prioritas kegiatan juga bisa berubah secara mendadak. Maaf curhat dikit terkadang dosen memberikan tugas baru dengan deadline singkat, belum kalau ada acara dadakan di departemen atau organisasi mengadakan rapat penting secara tiba-tiba. Tanpa sistem pengelolaan waktu yang baik, aku harus mengecek catatan secara manual dan menyesuaikan jadwal satu per satu, yang justru membuat waktu semakin tidak efisien. 

#### Solusi 
Berdasarkan permasalahan tersebut, dibuatlah program Manajemen Waktu Mahasiswa Multi-Kegiatan Adaptif menggunakan paradigma OOP. Program ini membantu menyimpan seluruh daftar kegiatan seperti kuliah, praktikum, asistensi, demo project, organisasi, pelatihan, acara departemen, dan deadline tugas dalam satu sistem. Selain itu, program mampu mendeteksi jadwal yang bentrok, menghitung total jam aktivitas, serta memberikan rekomendasi kegiatan yang harus diprioritaskan berdasarkan tingkat kepentingan dan kedekatan waktu deadline.

Dengan adanya sistem ini, aku dapat melihat jadwal hariannya dengan lebih jelas, mengetahui kegiatan mana yang paling mendesak, dan menghindari konflik waktu antar aktivitas. Program ini tidak hanya berfungsi sebagai pencatat jadwal, tetapi juga membantu mahasiswa mengambil keputusan yang lebih efektif dalam mengatur waktu, sehingga aktivitas akademik dan non-akademik dapat berjalan lebih seimbang.

#### Rancangan Kelas Diagram
diagram hasil di mermaid.ai

<img width="1079" height="1527" alt="mermaid-diagram (2)" src="https://github.com/user-attachments/assets/f9e34fc9-7510-4663-9e4c-7eea640dbff4" />

#### Implementasi Kode
```java
import java.util.*;

class Kegiatan {
    private String namaKegiatan;
    private int prioritas;
    private int jamMulai;
    private int jamSelesai;
    private String kategori;

    public Kegiatan(String namaKegiatan, int prioritas, int jamMulai, int jamSelesai, String kategori) {
        this.namaKegiatan = namaKegiatan;
        this.prioritas = prioritas;
        this.jamMulai = jamMulai;
        this.jamSelesai = jamSelesai;
        this.kategori = kategori;
    }

    public void tampilkan() {
        System.out.printf("%-30s | %-8d | %02d:00-%02d:00 | %-12s\n", namaKegiatan, prioritas, jamMulai, jamSelesai, kategori);
    }

    public String getNamaKegiatan() { return namaKegiatan; }
    public int getPrioritas() { return prioritas; }
    public int getJamMulai() { return jamMulai; }
    public int getJamSelesai() { return jamSelesai; }
    public String getKategori() { return kategori; }

    public boolean bentrok(Kegiatan lain) {
        return !(jamSelesai <= lain.getJamMulai() || jamMulai >= lain.getJamSelesai());
    }

    public int durasi() { return jamSelesai - jamMulai; }
}

class KegiatanAkademik extends Kegiatan {
    private String mataKuliah;
    private String dosen;

    public KegiatanAkademik(String namaKegiatan, int prioritas, int jamMulai, int jamSelesai, String mataKuliah, String dosen) {
        super(namaKegiatan, prioritas, jamMulai, jamSelesai, "Akademik");
        this.mataKuliah = mataKuliah;
        this.dosen = dosen;
    }

    @Override
    public void tampilkan() {
        System.out.printf("%-30s | %-8d | %02d:00-%02d:00 | %-12s | %-15s | %s\n", 
                          getNamaKegiatan(), getPrioritas(), getJamMulai(), getJamSelesai(), getKategori(), mataKuliah, dosen);
    }
}


class KegiatanNonAkademik extends Kegiatan {
    private String organisasi;
    private String lokasiRapat;

    public KegiatanNonAkademik(String namaKegiatan, int prioritas, int jamMulai, int jamSelesai, String organisasi, String lokasiRapat) {
        super(namaKegiatan, prioritas, jamMulai, jamSelesai, "Non-Akademik");
        this.organisasi = organisasi;
        this.lokasiRapat = lokasiRapat;
    }

    @Override
    public void tampilkan() {
        System.out.printf("%-30s | %-8d | %02d:00-%02d:00 | %-12s | %-15s | %s\n", 
                          getNamaKegiatan(), getPrioritas(), getJamMulai(), getJamSelesai(), getKategori(), organisasi, lokasiRapat);
    }
}

// Main App
public class App {
    public static void main(String[] args) {
        String nama = "May";
        String nim = "230123456";

        Kegiatan[] daftar = {
            new KegiatanAkademik("Kuliah Struktur Data", 2, 8, 10, "Struktur Data", "Pak Budi"),
            new KegiatanAkademik("Praktikum Struktur Data", 1, 10, 12, "Struktur Data", "Bu Sari"),
            new KegiatanAkademik("Deadline Tugas Algoritma", 1, 11, 12, "Algoritma", "Pak Joko"),
            new KegiatanAkademik("Asistensi Basis Data", 3, 13, 15, "Basis Data", "Bu Dina"),
            new KegiatanNonAkademik("Rapat Organisasi", 4, 19, 20, "Himpunan Mahasiswa", "Ruang 101"),
            new KegiatanNonAkademik("Demo Project", 1, 20, 21, "Kelompok Project", "Lab 5")
        };

        System.out.println("=== MANAJEMEN WAKTU MAHASISWA ===");
        System.out.println("Nama : " + nama);
        System.out.println("NIM  : " + nim);

        System.out.println("\nDaftar Kegiatan:");
        System.out.printf("%-30s | %-8s | %-11s | %-12s | %-15s | %s\n", "Kegiatan", "Prioritas", "Jam", "Kategori", "MataKuliah/Org", "Dosen/Lokasi");
        System.out.println("-------------------------------------------------------------------------------------------");
        for (Kegiatan k : daftar) k.tampilkan();

        System.out.println("\nDeteksi Bentrok Jadwal:");
        boolean adaBentrok = false;
        for (int i = 0; i < daftar.length; i++) {
            for (int j = i + 1; j < daftar.length; j++) {
                if (daftar[i].bentrok(daftar[j])) {
                    System.out.printf("%-30s <--> %s\n", daftar[i].getNamaKegiatan(), daftar[j].getNamaKegiatan());
                    adaBentrok = true;
                }
            }
        }
        if (!adaBentrok) System.out.println("Tidak ada jadwal yang bentrok.");

        int totalJam = 0;
        for (Kegiatan k : daftar) totalJam += k.durasi();
        System.out.println("\nTotal jam kegiatan hari ini: " + totalJam + " jam");

        Arrays.sort(daftar, Comparator.comparingInt(Kegiatan::getPrioritas));
        System.out.println("\nPrioritas utama:");
        daftar[0].tampilkan();
    }
}
```

#### Screenshot output

<img width="1501" height="753" alt="image" src="https://github.com/user-attachments/assets/6391c820-7437-4124-8308-03ee048178dc" />

#### Prinsip-prinsip OOP yang diterapkan

1. Encapsulation (Enkapsulasi)

Penjelasan:
Encapsulation berarti menyembunyikan atribut dari akses langsung dari luar kelas dan hanya menyediakan `getter/setter` atau method tertentu untuk mengaksesnya. Ini membuat data lebih aman dan terkontrol.

Bukti kode:
```
class Kegiatan {
    private String namaKegiatan;
    private int prioritas;
    private int jamMulai;
    private int jamSelesai;
    private String kategori;

    public Kegiatan(String namaKegiatan, int prioritas, int jamMulai, int jamSelesai, String kategori) {
        this.namaKegiatan = namaKegiatan;
        this.prioritas = prioritas;
        this.jamMulai = jamMulai;
        this.jamSelesai = jamSelesai;
        this.kategori = kategori;
    }

    public String getNamaKegiatan() { return namaKegiatan; }
    public int getPrioritas() { return prioritas; }
    public int getJamMulai() { return jamMulai; }
    public int getJamSelesai() { return jamSelesai; }
    public String getKategori() { return kategori; }
}
```
Yang terjadi:

`namaKegiatan`, `prioritas`, dll. `private`, jadi tidak bisa diubah langsung dari luar.
Untuk akses, kita gunakan `getter` seperti `getNamaKegiatan()`.

2. Inheritance (Pewarisan)

Penjelasan:
Inheritance memungkinkan kita membuat kelas anak (subclass) dari kelas induk (superclass) untuk menambahkan atau mengubah perilaku. Ini mengurangi duplikasi kode.

Bukti kode:
```
// Kelas induk
class Kegiatan { ... }

// Subclass Akademik
class KegiatanAkademik extends Kegiatan {
    private String mataKuliah;
    private String dosen;

    public KegiatanAkademik(String namaKegiatan, int prioritas, int jamMulai, int jamSelesai, String mataKuliah, String dosen) {
        super(namaKegiatan, prioritas, jamMulai, jamSelesai, "Akademik");
        this.mataKuliah = mataKuliah;
        this.dosen = dosen;
    }
}

// Subclass Non-Akademik
class KegiatanNonAkademik extends Kegiatan {
    private String organisasi;
    private String lokasiRapat;

    public KegiatanNonAkademik(String namaKegiatan, int prioritas, int jamMulai, int jamSelesai, String organisasi, String lokasiRapat) {
        super(namaKegiatan, prioritas, jamMulai, jamSelesai, "Non-Akademik");
        this.organisasi = organisasi;
        this.lokasiRapat = lokasiRapat;
    }
}
```
Yang terjadi:

`KegiatanAkademik` dan `KegiatanNonAkademik` mewarisi semua atribut dan method dari `Kegiatan`.
Subclass menambahkan atribut spesifik tanpa menulis ulang atribut umum.

3. Polymorphism (Polimorfisme)

Penjelasan:
Polymorphism memungkinkan objek kelas berbeda diperlakukan sama jika mereka berasal dari kelas induk yang sama. Contohnya, kita bisa menyimpan semua jenis `Kegiatan` dalam satu array `Kegiatan[]`.

Bukti kode:
```
Kegiatan[] daftar = {
    new KegiatanAkademik("Kuliah Struktur Data", 2, 8, 10, "Struktur Data", "Pak Budi"),
    new KegiatanNonAkademik("Rapat Organisasi", 4, 19, 20, "Himpunan Mahasiswa", "Ruang 101")
};

for (Kegiatan k : daftar) {
    k.tampilkan(); // Method tampilkan() yang dipanggil sesuai subclass masing-masing
}
```
Yang terjadi:

Meskipun tipe array Kegiatan, method `tampilkan()` akan dipanggil sesuai versi subclass yang sebenarnya (Akademik/Non-Akademik).
Ini disebut runtime polymorphism (overriding method).

4. Abstraction (Abstraksi)

Penjelasan:
Abstraction berarti menyembunyikan detail implementasi dan hanya menampilkan fungsi penting. Misalnya, kita tidak perlu tahu bagaimana bentrok jadwal dicek, cukup pakai method `bentrok()`.

Bukti kode:
```
public boolean bentrok(Kegiatan lain) {
    return !(getJamSelesai() <= lain.getJamMulai() || getJamMulai() >= lain.getJamSelesai());
}
```
Yang terjadi:

Pengguna kelas cukup memanggil `k1.bentrok(k2)` tanpa tahu logika perhitungan jam di dalamnya.
Abstraction memudahkan penggunaan kelas tanpa harus mengerti implementasinya.

#### Keunikan Sistem Manajemen Waktu Mahasiswa

# Keunikan Sistem Manajemen Waktu Mahasiswa

Program ini memiliki beberapa keunikan yang membedakannya dari cara individu lain mengatur waktu secara manual:

1. **Deteksi Jadwal Bentrok**  
   Program otomatis mendeteksi jika ada jadwal yang bertabrakan sehingga mahasiswa dapat segera menyesuaikan prioritas.

2. **Prioritas Berdasarkan Kepentingan dan Deadline**  
   Setiap kegiatan memiliki atribut prioritas, dan program memberikan rekomendasi kegiatan yang harus dilakukan terlebih dahulu.

3. **Perhitungan Total Jam Aktivitas**  
   Program menghitung total jam kegiatan harian secara otomatis, membantu mahasiswa memahami beban waktu mereka.

4. **OOP Lengkap dan Terstruktur**  
   Menggunakan prinsip Encapsulation, Abstraction, Inheritance, dan Polymorphism sehingga kode lebih rapi, mudah dikembangkan, dan fleksibel dibandingkan pencatatan manual.
