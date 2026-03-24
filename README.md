# Manajemen-Waktu-Mahasiswa
 ---
 ###  Nama : Maitasya Rohmatul Ula
 ###  NRP  : 5027251026
 ### Tugas : Class Diagram Strukdat
 ---
 ### Case: Sistem Prioritas Kegiatan Mahasiswa
 ####  Deskripsi Kasus 
 Sebagai mahasiswa, aku sering merasa  24 jam kurang deh karena banyaknya kegiatan yang harus dijalani. Dalam satu hari saja, aku bisa memiliki jadwal kuliah pagi sampai sore, atau kadang pagi kuliah dilanjutkan praktikum siang, lalu asistensi sore, dan malamnya masih harus join rapat organisasi atau UKM selain itu, kadang juga dikejar-kejar hantu perkuliahan. Ha?? Hantu perkuliahan? ets makausdnya deadline tugas. Belum lagi kalua ada demo project atau demo praktikum, pelatihan,seminar, atau acara departemen yang tiba-tiba muncul dan membuat jadwal semakin ambrul-adul dan padat.

Awalnya tidakmasalah sih tapi lambat laut masalah mulai terasa ketika beberapa kegiatan memiliki waktu yang bertabrakan, misalnya jadwal praktikum yang bentrok dengan deadline tugas yang berdekatan dengan jadwal demo project. Aku sering kebingungan menentukan kegiatan mana yang harus diprioritaskan terlebih dahulu, terutama ketika semua kegiatan terasa sama pentingnya. Akibatnya, ada tugas yang terlambat dikerjakan atau kegiatan yang terlewat karena tidak tercatat dengan baik.

Selain itu, prioritas kegiatan juga bisa berubah secara mendadak. Terkadang dosen memberikan tugas baru dengan deadline singkat, atau organisasi mengadakan rapat penting secara tiba-tiba. Tanpa sistem pengelolaan waktu yang baik, aku harus mengecek catatan secara manual dan menyesuaikan jadwal satu per satu, yang justru membuat waktu semakin tidak efisien.

Berdasarkan permasalahan tersebut, dibuatlah program Manajemen Waktu Mahasiswa Multi-Kegiatan Adaptif menggunakan paradigma OOP. Program ini membantu menyimpan seluruh daftar kegiatan seperti kuliah, praktikum, asistensi, demo project, organisasi, pelatihan, acara departemen, dan deadline tugas dalam satu sistem. Selain itu, program mampu mendeteksi jadwal yang bentrok, menghitung total jam aktivitas, serta memberikan rekomendasi kegiatan yang harus diprioritaskan berdasarkan tingkat kepentingan dan kedekatan waktu deadline.

Dengan adanya sistem ini, aku dapat melihat jadwal hariannya dengan lebih jelas, mengetahui kegiatan mana yang paling mendesak, dan menghindari konflik waktu antar aktivitas. Program ini tidak hanya berfungsi sebagai pencatat jadwal, tetapi juga membantu mahasiswa mengambil keputusan yang lebih efektif dalam mengatur waktu, sehingga aktivitas akademik dan non-akademik dapat berjalan lebih seimbang.
#### Rancangan Kelas Diagram

```memaid.ai
classDiagram

class Mahasiswa{
    - String nama
    - String nim
    - Kegiatan[] daftarKegiatan
    - int jumlahKegiatan
    + tambahKegiatan(Kegiatan k)
    + lihatSemuaKegiatan()
    + getDaftarKegiatan()
    + getJumlahKegiatan()
}

class Kegiatan{
    - String namaKegiatan
    - String jenisKegiatan
    - String hari
    - String tanggal
    - int jamMulai
    - int jamSelesai
    - int prioritas
    + getDurasi()
    + setPrioritas(int prioritas)
    + getInfo()
}

class Kuliah{
    - String mataKuliah
    + getInfo()
}

class Praktikum{
    - boolean adaAsistensi
    - boolean adaDemo
    + getInfo()
}

class DeadlineTugas{
    - String deadlineHari
    + getInfo()
}

class PengembanganDiri{
    - String jenisKegiatan
    + getInfo()
}

class PrioritasManager{
    + hitungPrioritas(Kegiatan k)
    + updateSemuaPrioritas(Mahasiswa mhs)
}

class JadwalManager{
    + cekBentrok(Mahasiswa mhs)
    + hitungTotalJam(Mahasiswa mhs)
    + tampilPrioritasUtama(Mahasiswa mhs)
}

Mahasiswa "1" --> "*" Kegiatan : "memiliki"
Kuliah --|> Kegiatan : "inheritance"
Praktikum --|> Kegiatan : "inheritance"
DeadlineTugas --|> Kegiatan : "inheritance"
PengembanganDiri --|> Kegiatan : "inheritance"

Mahasiswa "1" --> "1" PrioritasManager : "menggunakan"
Mahasiswa "1" --> "1" JadwalManager : "menggunakan"
```
#### diagram hasil di mermaid.ai
<img width="1022" height="407" alt="image" src="https://github.com/user-attachments/assets/6aa87adc-d0b4-4f21-975b-6da9560da391" />

Class diagram ini menggambarkan sistem manajemen waktu mahasiswa.
- Mahasiswa menyimpan data dasar seperti nama, NIM, dan daftar kegiatan. Mahasiswa bisa menambah kegiatan, melihat semua kegiatan, dan mengetahui jumlah kegiatan yang dimiliki.
- Kegiatan adalah class induk untuk semua aktivitas mahasiswa, menyimpan nama, jenis, hari, tanggal, jam mulai & selesai, serta prioritas. Kegiatan punya method untuk menghitung durasi, mengatur prioritas, dan menampilkan informasi.
- Terdapat empat jenis kegiatan yang mewarisi Kegiatan:
    1. Kuliah – menyimpan mata kuliah.
    2. Praktikum – menyimpan informasi asistensi dan demo.
    3. DeadlineTugas – menyimpan hari deadline tugas.
    4. PengembanganDiri – menyimpan jenis kegiatan pengembangan diri.
- PrioritasManager menghitung dan memperbarui prioritas kegiatan mahasiswa.
- JadwalManager mengecek bentrok jadwal, menghitung total jam kegiatan, dan menampilkan prioritas utama.
- Relasinya: Mahasiswa memiliki banyak kegiatan dan menggunakan PrioritasManager serta JadwalManager untuk mengatur jadwal dan prioritas.

#### Implementasi Kode

```java
import java.util.Scanner;

public class ManajemenWaktuMahasiswa {

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        System.out.println("=== Tracker Manajemen Waktu Mahasiswa ===");

        System.out.print("Masukkan Nama: ");
        String nama = input.nextLine();

        System.out.print("Masukkan NIM: ");
        String nim = input.nextLine();

        Mahasiswa mhs = new Mahasiswa(nama, nim);
        PrioritasManager pm = new PrioritasManager();
        JadwalManager jm = new JadwalManager();

// Input jadwal kuliah 1 semester
        System.out.println("\nInput Jadwal Kuliah 1 Semester");
        System.out.print("Berapa jumlah mata kuliah? ");
        int jumlahMK = input.nextInt();
        input.nextLine();

        for (int i = 0; i < jumlahMK; i++) {
            System.out.println("\nMata kuliah ke-" + (i + 1));
            System.out.print("Nama matkul: ");
            String matkul = input.nextLine();
            System.out.print("Hari: ");
            String hari = input.nextLine();
            System.out.print("Tanggal mulai semester: ");
            String tanggal = input.nextLine();
            System.out.print("Jam mulai: ");
            int mulai = input.nextInt();
            System.out.print("Jam selesai: ");
            int selesai = input.nextInt();
            input.nextLine();

            mhs.tambahKegiatan(new Kuliah(matkul, hari, tanggal, mulai, selesai, matkul));
        }

// Input kegiatan lain
    int pilih = 1;
    while (pilih == 1) {
        System.out.println("\nTambah kegiatan lain?");
        System.out.println("1. ya");
        System.out.println("0. tidak");
        System.out.print("Pilihan: ");
        pilih = input.nextInt();
        input.nextLine();
    
    if (pilih == 1) {
            System.out.println("\nJenis kegiatan:");
            System.out.println("1. Praktikum (praktikum/asistensi/demo)");
            System.out.println("2. Deadline Tugas");
            System.out.println("3. Pengembangan Diri (Organisasi, Pelatihan, Acara, Seminar)");      
            System.out.print("Pilihan: ");
            int jenis = input.nextInt();
            input.nextLine();

        if (jenis == 1) {
            Praktikum.tambahPraktikumLengkap(mhs, input);
        } else if (jenis == 2) {
            System.out.print("Nama kegiatan: ");
             String namaKegiatan = input.nextLine();

            System.out.print("Deadline hari apa: ");
            String deadlineHari = input.nextLine();

            System.out.print("Tanggal Deadline: ");
            String tanggalDeadline = input.nextLine();

            System.out.print("Jam terakhir pengumpulan: ");
            int jamSelesai = input.nextInt();
            input.nextLine();

            int jamMulai = jamSelesai - 2; // durasi contoh 2 jam
             mhs.tambahKegiatan(new DeadlineTugas(namaKegiatan, deadlineHari, tanggalDeadline, jamMulai, jamSelesai, deadlineHari));

        } else if (jenis == 3) {
            System.out.print("Nama kegiatan: ");
            String namaKegiatan = input.nextLine();
            System.out.print("Hari: ");
            String hariK = input.nextLine();
            System.out.print("Tanggal: ");
            String tanggalK = input.nextLine();
            System.out.print("Jam mulai: ");
            int mulai = input.nextInt();
            System.out.print("Jam selesai: ");
            int selesai = input.nextInt();
            input.nextLine();
            System.out.print("Jenis kegiatan (Organisasi/Pelatihan/Acara/Seminar): ");
            String jenisK = input.nextLine();

            mhs.tambahKegiatan(new PengembanganDiri(namaKegiatan, hariK, tanggalK, mulai, selesai, jenisK));
                }
            }
        }
// Proses sistem
        pm.updateSemuaPrioritas(mhs);
        mhs.lihatSemuaKegiatanUrut(); 
        jm.cekBentrok(mhs);

        int total = jm.hitungTotalJam(mhs);
        System.out.println("\nTotal jam kegiatan: " + total);

        jm.tampilPrioritasUtama(mhs);

        System.out.println("\nProgram selesai");
    }
}
// KELAS MAHASISWA
class Mahasiswa {
    String nama;
    String nim;
    Kegiatan[] daftarKegiatan = new Kegiatan[100];
    int jumlahKegiatan = 0;

    Mahasiswa(String nama, String nim) {
        this.nama = nama;
        this.nim = nim;
    }

    void tambahKegiatan(Kegiatan k) {
        daftarKegiatan[jumlahKegiatan] = k;
        jumlahKegiatan++;
    }
    void lihatSemuaKegiatanUrut() {
        for (int i = 0; i < jumlahKegiatan - 1; i++) {
            for (int j = 0; j < jumlahKegiatan - i - 1; j++) {
                if (daftarKegiatan[j].tanggal.compareTo(daftarKegiatan[j + 1].tanggal) > 0) {
                    Kegiatan temp = daftarKegiatan[j];
                    daftarKegiatan[j] = daftarKegiatan[j + 1];
                    daftarKegiatan[j + 1] = temp;
                }
            }
        }

        System.out.println("\nDaftar Kegiatan " + nama + ":");
        for (int i = 0; i < jumlahKegiatan; i++) {
            System.out.println((i + 1) + ". " + daftarKegiatan[i].getInfo());
        }
    }

    Kegiatan[] getDaftarKegiatan() { return daftarKegiatan; }
    int getJumlahKegiatan() { return jumlahKegiatan; }
}
// KELAS KEGIATAN
class Kegiatan {
    String namaKegiatan;
    String kategori;
    String hari;
    String tanggal;
    int jamMulai;
    int jamSelesai;
    int prioritas;

    Kegiatan(String nama, String kategori, String hari, String tanggal, int mulai, int selesai) {
        this.namaKegiatan = nama;
        this.kategori = kategori;
        this.hari = hari;
        this.tanggal = tanggal;
        this.jamMulai = mulai;
        this.jamSelesai = selesai;
        this.prioritas = 0;
    }
    int getDurasi() { return jamSelesai - jamMulai; }
    void setPrioritas(int p) { prioritas = p; }

    String getInfo() {
        return String.format("%-20s | %-17s | %-7s | %-10s | %02d-%02d | prioritas: %d",
                namaKegiatan, kategori, hari, tanggal, jamMulai, jamSelesai, prioritas);
    }
}
// SUBCLASS KEGIATAN
class Kuliah extends Kegiatan {
    String mataKuliah;
    Kuliah(String nama, String hari, String tanggal, int mulai, int selesai, String mataKuliah) {
        super(nama, "Kuliah Kelas", hari, tanggal, mulai, selesai);
        this.mataKuliah = mataKuliah;
    }
    @Override
    String getInfo() {
        return super.getInfo() + " | matkul: " + mataKuliah;
    }
}

class Praktikum extends Kegiatan {
    Praktikum(String nama, String hari, String tanggal, int mulai, int selesai) {
        super(nama, "Praktikum", hari, tanggal, mulai, selesai);
    }
    @Override
    String getInfo() { return super.getInfo(); }

    static void tambahPraktikumLengkap(Mahasiswa mhs, Scanner input) {
        System.out.println("\nPRAKTIKUM BARU");
        System.out.print("Nama Praktikum: ");
        String namaPraktikum = input.nextLine();

// Asistensi
        System.out.println("\nASISTENSI");
        System.out.print("Hari Asistensi (kosong jika tidak ada): ");
        String hariA = input.nextLine();
        if (!hariA.isEmpty()) {
            System.out.print("Tanggal: ");
            String tanggalA = input.nextLine();
            System.out.print("Jam mulai: ");
            int mulaiA = input.nextInt();
            System.out.print("Jam selesai: ");
            int selesaiA = input.nextInt();
            input.nextLine();
            mhs.tambahKegiatan(new Praktikum("Asistensi " + namaPraktikum, hariA, tanggalA, mulaiA, selesaiA));
        }

// Praktikum utama
        System.out.println("\nPRAKTIKUM UTAMA");
        System.out.print("Hari Praktikum utama: ");
        String hariP = input.nextLine();
        System.out.print("Tanggal: ");
        String tanggalP = input.nextLine();
        System.out.print("Jam mulai: ");
        int mulaiP = input.nextInt();
        System.out.print("Jam selesai: ");
        int selesaiP = input.nextInt();
        input.nextLine();
        mhs.tambahKegiatan(new Praktikum(namaPraktikum, hariP, tanggalP, mulaiP, selesaiP));

// Demo
        System.out.println("\nDEMO");
        System.out.print("Hari Demo (kosong jika tidak ada): ");
        String hariD = input.nextLine();
        if (!hariD.isEmpty()) {
            System.out.print("Tanggal: ");
            String tanggalD = input.nextLine();
            System.out.print("Jam mulai: ");
            int mulaiD = input.nextInt();
            System.out.print("Jam selesai: ");
            int selesaiD = input.nextInt();
            input.nextLine();
            mhs.tambahKegiatan(new Praktikum("Demo " + namaPraktikum, hariD, tanggalD, mulaiD, selesaiD));
        }
    }
}

class DeadlineTugas extends Kegiatan {
    String deadlineHari;
    DeadlineTugas(String nama, String hari, String tanggal, int mulai, int selesai, String deadlineHari) {
        super(nama, "Deadline Tugas", hari, tanggal, mulai, selesai);
        this.deadlineHari = deadlineHari; // diperbaiki
    }
    @Override
    String getInfo() {
        return super.getInfo() + " | deadline: " + deadlineHari;
    }
}

class PengembanganDiri extends Kegiatan {
    String jenisKegiatan;
    PengembanganDiri(String nama, String hari, String tanggal, int mulai, int selesai, String jenisKegiatan) {
        super(nama, "Pengembangan Diri", hari, tanggal, mulai, selesai);
        this.jenisKegiatan = jenisKegiatan;
    }
    @Override
    String getInfo() {
        return super.getInfo() + " | jenis: " + jenisKegiatan;
    }
}
// PRIORITAS MANAGER
class PrioritasManager {
    void hitungPrioritas(Kegiatan k) {
        switch (k.kategori) {
            case "Deadline Tugas": k.setPrioritas(1); break;
            case "Kuliah Kelas":
            case "Praktikum": k.setPrioritas(2); break;
            case "Pengembangan Diri": k.setPrioritas(3); break;
            default: k.setPrioritas(4);
        }
    }
    void updateSemuaPrioritas(Mahasiswa mhs) {
        for (int i = 0; i < mhs.getJumlahKegiatan(); i++)
            hitungPrioritas(mhs.getDaftarKegiatan()[i]);
    }
}
// JADWAL MANAGER
class JadwalManager {
    void cekBentrok(Mahasiswa mhs) {
        System.out.println("\nCek Bentrok Jadwal:");
        for (int i = 0; i < mhs.getJumlahKegiatan(); i++) {
            for (int j = i + 1; j < mhs.getJumlahKegiatan(); j++) {
                Kegiatan a = mhs.getDaftarKegiatan()[i];
                Kegiatan b = mhs.getDaftarKegiatan()[j];
                if (a.hari.equals(b.hari)) {
                    boolean bentrok = a.jamMulai < b.jamSelesai && b.jamMulai < a.jamSelesai;
                    if (bentrok)
                        System.out.println("Bentrok: " + a.namaKegiatan + " dengan " + b.namaKegiatan);
                }
            }
        }
    }
    int hitungTotalJam(Mahasiswa mhs) {
        int total = 0;
        for (int i = 0; i < mhs.getJumlahKegiatan(); i++)
            total += mhs.getDaftarKegiatan()[i].getDurasi();
        return total;
    }
    void tampilPrioritasUtama(Mahasiswa mhs) {
        if (mhs.getJumlahKegiatan() == 0) return;
        Kegiatan utama = mhs.getDaftarKegiatan()[0];
        for (int i = 1; i < mhs.getJumlahKegiatan(); i++)
            if (mhs.getDaftarKegiatan()[i].prioritas < utama.prioritas)
                utama = mhs.getDaftarKegiatan()[i];
        System.out.println("\nYang paling penting dikerjakan:");
        System.out.println(utama.getInfo());
    }
}
```
#### Screenshot output
 Input masukan awal jadwal kelas harian
<img width="1348" height="821" alt="Screenshot 2026-03-24 142657" src="https://github.com/user-attachments/assets/b700efdc-5f47-4f3b-9ee9-201ba28e7784" />

Input jadwal kegitaan praktikum
<img width="1355" height="818" alt="Screenshot 2026-03-24 142712" src="https://github.com/user-attachments/assets/855c4d60-fa96-49ee-bc95-c1c060a75b6e" />

Input jadwal kegitaan deadline tugas
<img width="1367" height="477" alt="Screenshot 2026-03-24 142736" src="https://github.com/user-attachments/assets/5719a3ea-579e-4a39-b35d-85e1db6958e5" />

Input jadwal kegitaan pengembangan diri
<img width="1372" height="822" alt="Screenshot 2026-03-24 142751" src="https://github.com/user-attachments/assets/febcfba4-bb97-42c1-82cc-b51c137bb8f0" />

Informasi keseluruhan jadwal
<img width="1318" height="763" alt="Screenshot 2026-03-24 142809" src="https://github.com/user-attachments/assets/0c8f621c-8a4c-491f-9fff-94c3d9f16efe" />
