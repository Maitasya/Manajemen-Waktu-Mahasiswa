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

<img width="660" height="1264" alt="mermaid-diagram" src="https://github.com/user-attachments/assets/e7a3c895-88db-4c96-836a-a39c3e376c88" />

#### Implementasi Kode
```java
import java.util.*;

class Kegiatan {
    private String namaKegiatan;
    private int prioritas;
    private int jamMulai;
    private int jamSelesai;

    public Kegiatan(String namaKegiatan, int prioritas, int jamMulai, int jamSelesai) {
        this.namaKegiatan = namaKegiatan;
        this.prioritas = prioritas;
        this.jamMulai = jamMulai;
        this.jamSelesai = jamSelesai;
    }

    public void tampilkan() {
        System.out.printf("%-30s | %-8d | %02d:00-%02d:00\n", namaKegiatan, prioritas, jamMulai, jamSelesai);
    }

    public String getNamaKegiatan() { return namaKegiatan; }
    public int getPrioritas() { return prioritas; }
    public int getJamMulai() { return jamMulai; }
    public int getJamSelesai() { return jamSelesai; }
    public boolean bentrok(Kegiatan lain) {
        return !(jamSelesai <= lain.getJamMulai() || jamMulai >= lain.getJamSelesai());
    }
    public int durasi() { return jamSelesai - jamMulai; }
}

class KegiatanOnline extends Kegiatan {
    private String linkZoom;

    public KegiatanOnline(String namaKegiatan, int prioritas, int jamMulai, int jamSelesai, String linkZoom) {
        super(namaKegiatan, prioritas, jamMulai, jamSelesai);
        this.linkZoom = linkZoom;
    }

    @Override
    public void tampilkan() {
        System.out.printf("%-30s | %-8d | %02d:00-%02d:00 | %s\n", getNamaKegiatan(), getPrioritas(),
                          getJamMulai(), getJamSelesai(), linkZoom);
    }
}

public class App {
    public static void main(String[] args) {
        String nama = "May";
        String nim = "230123456";

        Kegiatan[] daftar = {
            new Kegiatan("Kuliah Struktur Data", 2, 8, 10),
            new KegiatanOnline("Praktikum Struktur Data", 1, 10, 12, "zoom.com/praktikum"),
            new Kegiatan("Deadline Tugas Algoritma", 1, 11, 12),
            new KegiatanOnline("Asistensi Basis Data", 3, 13, 15, "zoom.com/asistensi"),
            new Kegiatan("Rapat Organisasi", 4, 19, 20),
            new Kegiatan("Demo Project", 1, 20, 21)
        };

        System.out.println("=== MANAJEMEN WAKTU MAHASISWA ===");
        System.out.println("Nama : " + nama);
        System.out.println("NIM  : " + nim);

        System.out.println("\nDaftar Kegiatan:");
        System.out.printf("%-30s | %-8s | %-11s | %s\n", "Kegiatan", "Prioritas", "Jam", "Link");
        System.out.println("--------------------------------------------------------------------------");
        for (Kegiatan k : daftar) k.tampilkan();

        System.out.println("\nDeteksi Bentrok Jadwal:");
        boolean adaBentrok = false;
        for (int i = 0; i < daftar.length; i++) {
            for (int j = i + 1; j < daftar.length; j++) {
                if (daftar[i].bentrok(daftar[j])) {
                    System.out.printf("⚠ %-30s <--> %s\n", daftar[i].getNamaKegiatan(), daftar[j].getNamaKegiatan());
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

<img width="1252" height="586" alt="image" src="https://github.com/user-attachments/assets/c5378481-828f-4574-b18e-91cc5e25c7b5" />

#### Prinsip-prinsip OOP yang diterapkan

1. Encapsulation (Enkapsulasi / menyimpan data di satu tempat)

Penjelasan:
Setiap class menyimpan data (atribut) dan fungsi (method) yang saling berkaitan. Data dibuat private agar tidak bisa diubah sembarangan, tetapi diakses melalui method tertentu.

Bukti dari kode:
Kelas Kegiatan menyimpan:
`private String namaKegiatan`
`private int prioritas`

Method dalam class:
getNamaKegiatan() → mengambil nama kegiatan
getPrioritas() → mengambil nilai prioritas
tampilkan() → menampilkan data kegiatan
Data kegiatan tidak diubah langsung, tetapi melalui constructor:
Kegiatan(String namaKegiatan, int prioritas)

2. Inheritance (Pewarisan / turun-temurun)

Penjelasan:
Inheritance memungkinkan class turunan (subclass) mewarisi atribut dan method dari class induk sehingga tidak perlu menulis ulang kode yang sama.

Bukti dari kode (konsep yang bisa diterapkan):
Kelas induk: Kegiatan
Subclass yang dapat dibuat:
Kuliah → menambahkan String mataKuliah
Praktikum → menambahkan String ruangLab
Deadline → menambahkan String tanggalDeadline

Semua subclass mewarisi:
`namaKegiatan`
`prioritas`
`method tampilkan()`

Contoh konsep:
```java
class Kuliah extends Kegiatan {
    String mataKuliah;
}
```
3. Polymorphism (Banyak bentuk / fleksibel)

Penjelasan:
Polymorphism memungkinkan satu method digunakan oleh banyak object dengan hasil yang berbeda tergantung object yang memanggilnya.

Bukti dari kode:
Method yang digunakan:
`tampilkan()`
Dipanggil oleh banyak object:
`k1.tampilkan()`
`k2.tampilkan()`
`k3.tampilkan()`
dst.

Walaupun method sama, isi yang ditampilkan berbeda karena data tiap object berbeda.
Loop juga menunjukkan polymorphism:
```java
for(int i=0; i<daftar.length; i++){
    daftar[i].tampilkan();
}
```
4. Abstraction (Abstraksi / fokus ke yang penting)

Penjelasan:
Abstraction menyederhanakan penggunaan program sehingga user hanya melihat fungsi utama tanpa perlu mengetahui proses detail di dalam program.

Bukti dari kode:
User cukup menjalankan program untuk melihat:
`daftar kegiatan`
`urutan prioritas`
`kegiatan paling penting`

Detail proses seperti sorting tidak terlihat oleh user:
```java
for(int i=0;i<daftar.length-1;i++){
    for(int j=0;j<daftar.length-1-i;j++){
        if(daftar[j].getPrioritas() >
           daftar[j+1].getPrioritas()){
           
           Kegiatan temp = daftar[j];
           daftar[j] = daftar[j+1];
           daftar[j+1] = temp;
        }
    }
}
```
User hanya melihat hasil akhir tanpa perlu memahami algoritma sorting.
 
#### Keunikan Sistem Manajemen Waktu Mahasiswa

1. Prioritas otomatis → setiap kegiatan memiliki tingkat prioritas sehingga mudah menentukan mana yang paling penting.
2. Pengurutan kegiatan → jadwal dapat diurutkan otomatis berdasarkan prioritas.
3. Fokus kebutuhan mahasiswa → mencakup kuliah, praktikum, deadline tugas, organisasi, dan seminar.
4. Mengurangi lupa deadline → semua kegiatan tercatat dalam satu sistem.
5. Berbasis OOP → data tersusun rapi dalam bentuk class dan object sehingga mudah dikembangkan.
6. Mudah dikembangkan → bisa ditambah fitur notifikasi, pengingat, dan cek bentrok jadwal.
