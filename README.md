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

public class ManajemenWaktuMahasiswa {

    public static void main(String[] args) {

        // Data mahasiswa (langsung diisi, tanpa input)
        String nama = "May";
        String nim = "230123456";

        // Jadwal kegiatan (contoh kasus bentrok & deadline)
        String[] kegiatan = {
            "Kuliah Struktur Data (08.00 - 10.00)",
            "Praktikum Struktur Data (10.00 - 12.00)",
            "Deadline Tugas Algoritma (12.00)",
            "Asistensi Basis Data (13.00 - 15.00)",
            "Rapat Organisasi (19.00 - 20.00)",
            "Demo Project (20.00)"
        };

        // Prioritas (1 = sangat penting)
        int[] prioritas = {1, 1, 1, 2, 3, 1};

        System.out.println("=== Tracker Manajemen Waktu Mahasiswa ===");
        System.out.println("Nama : " + nama);
        System.out.println("NIM  : " + nim);

        System.out.println("\nDaftar Kegiatan Hari Ini:");
        
        for (int i = 0; i < kegiatan.length; i++) {
            System.out.println((i+1) + ". " + kegiatan[i] + 
                               " | Prioritas: " + prioritas[i]);
        }

        // mencari prioritas tertinggi
        int prioritasTertinggi = prioritas[0];
        int index = 0;

        for (int i = 1; i < prioritas.length; i++) {
            if (prioritas[i] < prioritasTertinggi) {
                prioritasTertinggi = prioritas[i];
                index = i;
            }
        }

        System.out.println("\nKegiatan yang harus diprioritaskan:");
        System.out.println(kegiatan[index]);
    }
}
#### Screenshot output

##### Input masukan awal jadwal kelas harian

<img width="1348" height="821" alt="Screenshot 2026-03-24 142657" src="https://github.com/user-attachments/assets/b700efdc-5f47-4f3b-9ee9-201ba28e7784" />

##### Input jadwal kegitaan praktikum

<img width="1355" height="818" alt="Screenshot 2026-03-24 142712" src="https://github.com/user-attachments/assets/855c4d60-fa96-49ee-bc95-c1c060a75b6e" />

##### Input jadwal kegitaan deadline tugas

<img width="1367" height="477" alt="Screenshot 2026-03-24 142736" src="https://github.com/user-attachments/assets/5719a3ea-579e-4a39-b35d-85e1db6958e5" />

##### Input jadwal kegitaan pengembangan diri

<img width="1372" height="822" alt="Screenshot 2026-03-24 142751" src="https://github.com/user-attachments/assets/febcfba4-bb97-42c1-82cc-b51c137bb8f0" />

##### Informasi keseluruhan jadwal

<img width="1318" height="763" alt="Screenshot 2026-03-24 142809" src="https://github.com/user-attachments/assets/0c8f621c-8a4c-491f-9fff-94c3d9f16efe" />

#### Prinsip-prinsip OOP yang diterapkan

1. Encapsulation (Enkapsulasi / menyimpan data di satu tempat)
- Penjelasan: Setiap kelas menyimpan data dan fungsi yang saling berkaitan sehingga manipulasi data bisa melalui method tertentu.
- Bukti dari kode:
  - Kelas `Mahasiswa` menyimpan:
    - `String nama`
    - `String nim`
    - `Kegiatan[] daftarKegiatan`
    - `int jumlahKegiatan`
    - Method: `tambahKegiatan()`, `lihatSemuaKegiatanUrut()`
  - Kelas `Kegiatan` menyimpan:
    - `String namaKegiatan`, `String kategori`, `String hari`, `String tanggal`
    - `int jamMulai`, `int jamSelesai`, `int prioritas`
    - Method: `getInfo()`, `getDurasi()`, `setPrioritas()`

2. Inheritance (Pewarisan / turun-temurun)
- Penjelasan: Kelas induk mewariskan atribut dan method ke subclass, sehingga subclass bisa menggunakan dan menambahkan fungsi baru.
- Bukti dari kode:
  - Kelas induk: `Kegiatan`
  - Subclass:
    - `Kuliah` → menambahkan `String mataKuliah` + override `getInfo()`
    - `Praktikum` → menambahkan method `tambahPraktikumLengkap()` + override `getInfo()`
    - `DeadlineTugas` → menambahkan `String deadlineHari` + override `getInfo()`
    - `PengembanganDiri` → menambahkan `String jenisKegiatan` + override `getInfo()`

3. Polymorphism (Banyak bentuk / fleksibel)
- Penjelasan: Subclass bisa mengubah atau menyesuaikan perilaku method dari kelas induk, sehingga satu method bisa menampilkan bentuk berbeda sesuai tipe subclass.
- Bukti dari kode:
  - Semua subclass `Kegiatan` memiliki method `getInfo()`, tapi hasilnya berbeda:
    - `Kuliah.getInfo()` → menambahkan info `mataKuliah`
    - `Praktikum.getInfo()` → tetap menampilkan info dasar kegiatan
    - `DeadlineTugas.getInfo()` → menambahkan info `deadlineHari`
    - `PengembanganDiri.getInfo()` → menambahkan info `jenisKegiatan`

4. Abstraction (Abstraksi / fokus ke yang penting)
- Penjelasan: Pengguna cukup fokus ke fungsi utama, tanpa perlu tahu detail implementasi di dalamnya.
- Bukti dari kode:
  - Mahasiswa cukup memanggil:
    - `lihatSemuaKegiatanUrut()` → menampilkan jadwal urut tanpa perlu tahu algoritma pengurutan tanggal
    - `tampilPrioritasUtama()` → menampilkan kegiatan paling penting tanpa tahu cara perhitungan prioritas
  - `PrioritasManager` dan `JadwalManager` menangani semua perhitungan prioritas, cek bentrok, dan total jam

5. Modularitas (Pisah-pisah fungsi supaya rapi)
- Penjelasan: Fungsi dikelompokkan sesuai tanggung jawab agar kode rapi dan mudah dikembangkan.
- Bukti dari kode:
  - `PrioritasManager` → khusus untuk:
    - `hitungPrioritas(Kegiatan k)`
    - `updateSemuaPrioritas(Mahasiswa mhs)`
  - `JadwalManager` → khusus untuk:
    - `cekBentrok(Mahasiswa mhs)`
    - `hitungTotalJam(Mahasiswa mhs)`
    - `tampilPrioritasUtama(Mahasiswa mhs)`
  - Dengan pemisahan ini, jika mau menambahkan fitur baru seperti notifikasi atau pengingat, cukup buat class baru tanpa mengubah kelas lain.
 
#### Keunikan Sistem Manajemen Waktu Mahasiswa

Sistem ini punya beberapa keunikan yang membedakan dari metode atau catatan individu lain:

1. Multi-kegiatan & Adaptif

Program ini mampu menangani berbagai jenis kegiatan sekaligus, mulai dari kuliah, praktikum, asistensi, demo, deadline tugas, organisasi, seminar, hingga pelatihan. Banyak mahasiswa biasanya hanya mencatat satu jenis kegiatan saja, misalnya hanya kuliah, sehingga jadwal lain sering terlewat. Dengan sistem ini, seluruh kegiatan bisa tersimpan dan teratur di satu tempat.

2. Deteksi Bentrok Otomatis

Sistem dapat mendeteksi jadwal yang saling bertabrakan secara otomatis tanpa perlu dicek manual. Hal ini membantu mahasiswa mengatur prioritas dan memutuskan mana yang harus dikerjakan terlebih dahulu, yang jarang ditemukan di metode catatan konvensional.

3. Prioritas Dinamis

Prioritas setiap kegiatan dihitung berdasarkan kategori, sehingga mahasiswa tahu kegiatan mana yang paling penting setiap hari. Contohnya, `Deadline Tugas` otomatis menjadi prioritas 1, sedangkan kegiatan pengembangan diri seperti seminar atau pelatihan masuk prioritas 3. Dengan cara ini, keputusan terkait waktu bisa lebih cepat dan efisien.

4. User-friendly & Interaktif

Input data dilakukan langsung melalui terminal dengan menu yang interaktif, sehingga mahasiswa bisa menambah kegiatan baru dengan mudah. Output menampilkan jadwal lengkap, total jam kegiatan, serta prioritas utama, sehingga mahasiswa bisa memvisualisasikan aktivitas hariannya dengan jelas.

#### Kekurangan Program

Meskipun sistem Manajemen Waktu Mahasiswa ini sudah cukup membantu, ada beberapa keterbatasan, salah satunya adalah data belum bisa disimpan secara permanen.  

- Saat program ditutup, semua data yang dimasukkan akan hilang karena hanya tersimpan di memori sementara (RAM).  
- Mahasiswa harus memasukkan ulang semua jadwal setiap kali program dijalankan kembali.  
- Kekurangan ini membuat sistem kurang efisien jika ingin digunakan untuk semester penuh atau kegiatan jangka panjang.  

> Catatan: Untuk mengatasi ini, program bisa dikembangkan dengan fitur `penyimpanan file` (misal CSV, TXT, atau database sederhana) sehingga data jadwal bisa tersimpan dan dibuka kembali kapan saja.
  
