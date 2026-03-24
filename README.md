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
