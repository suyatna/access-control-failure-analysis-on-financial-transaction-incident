# Access control failure analysis on financial transaction incident

1. [Backkground](#background)
2. [Scenario overview](#scenario)
3. [Incident evidence](#incident)
4. [Access control worksheet](#worksheet)
5. [Key takeaways and insights](#insight)
6. [Conclusion](#conclusion)

---

## 🧠 Background <a name="background">

Studi kasus ini saya buat sebagai latihan kuliah cybersecurity dengan fokus ke kontrol akses dan kejadian finansial yang terjadi di dalam sistem bisnis. Skenario menggambarkan kondisi perusahaan yang sedang berkembang dan mulai bergantung pada sistem digital untuk mengelola transaksi penting, termasuk keuangan. Situasi ini menunjukkan bagaimana satu aktivitas yang terlihat kecil bisa berdampak besar kalau akses pengguna tidak dikontrol dengan baik.

Latihan ini mengacu ke materi Google Cybersecurity Professional Certificate, khususnya course Assets, Threats, and Vulnerabilities. Pembahasan saya mulai dengan memahami aset apa yang paling krusial di kasus ini, lalu melihat ancaman dan kelemahan yang muncul lewat penyalahgunaan akun. Proses ini membantu saya memahami bahwa risiko tidak selalu muncul karena sistem diserang, tapi juga bisa muncul karena kontrol akses yang longgar dan kurang diawasi.

---

## 🧩 Scenario overview <a name="scenario">

Skenario ini menceritakan kondisi bisnis yang lagi tumbuh dan baru pertama kali punya peran khusus di bidang cyber security. Saya diposisikan sebagai orang pertama yang pegang urusan keamanan. Masalah muncul saat ada setoran uang ke rekening bank yang tidak dikenal. Pihak keuangan merasa tidak pernah melakukan transaksi tersebut dan akhirnya pembayaran bisa dihentikan sebelum benar-benar terjadi kerugian.

Tugas saya di skenario ini fokus ke mencari tahu apa yang sebenarnya terjadi. Proses dimulai dengan melihat log akses yang terkait kejadian itu. Log ini dipakai untuk melihat aktivitas akun, waktu akses, dan kemungkinan penyalahgunaan akun. Catatan kecil mulai dikumpulkan untuk menebak siapa aktor ancamannya dan bagaimana akses bisa terjadi.

Langkah berikutnya melihat kontrol akses yang dipakai di sistem. Bagian ini membantu saya memahami celah apa yang dimanfaatkan pengguna, baik karena hak akses terlalu luas atau akun yang seharusnya sudah tidak aktif. Skenario ini ditutup dengan membuat rekomendasi sederhana berdasarkan temuan tadi, supaya kontrol akses bisa diperbaiki dan kejadian serupa tidak gampang terulang.

---

## 📄 Incident evidence <a name="incident">

### Event log summary

Bagian ini saya lihat untuk tahu aktivitas apa yang terjadi di sistem saat insiden. Data event log menunjukan ada perubahan penting terkait payroll dan rekening bank. Informasi ini jadi petunjuk awal siapa akun yang dipakai dan kapan kejadian berlangsung.

| Field          | Value                          |
| -------------- | ------------------------------ |
| Event type     | Information                    |
| Event source   | AdsmEmployeeService            |
| Event category | None                           |
| Event ID       | 1227                           |
| Date           | 10/03/2023                     |
| Time           | 8:29:57 AM                     |
| User           | Legal\Administrator            |
| Computer       | Up2-NoGud                      |
| IP address     | 152.207.255.255                |
| Description    | Payroll event added. FAUX_BANK |

### Employee directory snapshot

Bagian ini saya pakai untuk mencocokkan IP address dan akun yang muncul di log. Fokusnya ke siapa saja yang masih punya akses admin dan status akunnya. Beberapa akun terlihat sudah tidak aktif secara kontrak tapi masih tercatat punya akses penuh.

| Name              | Role             | Email                                                   | IP Address      | Status     | Authorization | Last Access                  | Start Date | End Date   |
| ----------------- | ---------------- | ------------------------------------------------------- | --------------- | ---------- | ------------- | ---------------------------- | ---------- | ---------- |
| Lisa Lawrence     | Office manager   | l.lawrence@erems.net                                    | 118.119.20.150  | Full-time  | Admin         | 12:27:19 pm (0 minutes ago)  | 10/01/2019 | N/A        |
| Jesse Pena        | Graphic designer | j.pena@erems.net                                        | 186.125.232.66  | Part-time  | Admin         | 4:55:05 pm (1 day ago)       | 11/16/2020 | N/A        |
| Catherine Martin  | Sales associate  | catherine_M@erems.net                                   | 247.168.184.57  | Full-time  | Admin         | 12:17:34 am (10 minutes ago) | 10/01/2019 | N/A        |
| Jyoti Patil       | Account manager  | j.patil@erems.net                                       | 159.250.146.63  | Full-time  | Admin         | 10:03:08 am (2 hours ago)    | 10/01/2019 | N/A        |
| Joanne Phelps     | Sales associate  | j_phelps123@erems.net                                   | 249.57.94.27    | Seasonal   | Admin         | 1:24:57 pm (2 years ago)     | 11/16/2020 | 01/31/2020 |
| Ariel Olson       | Owner            | a.olson@erems.net                                       | 19.7.235.151    | Full-time  | Admin         | 12:24:41 pm (4 minutes ago)  | 08/01/2019 | N/A        |
| Robert Taylor Jr. | Legal attorney   | rt.jr@erems.net                                         | 152.207.255.255 | Contractor | Admin         | 8:29:57 am (5 days ago)      | 09/04/2019 | 12/27/2019 |
| Amanda Pearson    | Manufacturer     | amandap987@erems.net                                    | 101.225.113.171 | Contractor | Admin         | 6:24:19 pm (3 months ago)    | 08/05/2019 | N/A        |
| George Harris     | Security analyst | georgeharris@erems.net                                  | 70.188.129.105  | Full-time  | Admin         | 05:05:22 pm (1 day ago)      | 01/24/2022 | N/A        |
| Lei Chu           | Marketing        | lei.chu@erems.net                                       | 53.49.27.117    | Part-time  | Admin         | 3:05:00 pm (2 days ago)      | 11/16/2020 | 01/31/2020 |

## 🧠 Access control worksheet <a name="worksheet">

Berikut adalah rangkuman hasil pengamatan soal kontrol akses yang terlibat di insiden ini. Fokusnya ke siapa yang melakukan aktivitas, akses apa yang dipakai, dan celah yang kelihatan jelas saat data log dan direktori karyawan dibandingkan. Tabel ini membantu saya melihat masalahnya secara sederhana tanpa ribet, jadi alurnya tetap masuk akal walau cuma berdasarkan log dan data dasar.

| Area Kontrol                   | Catatan                                                                                                                                                                                                                                       | Masalah                                                                                                                                                                                                                          | Rekomendasi                                                                                                                                                                                          |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Otorisasi / otentikasi         | Insiden tercatat tanggal 10/03/2023 pagi. Aktivitas dilakukan pakai akun Legal\Administrator. Perangkat tercatat sebagai komputer Up2-NoGud dengan IP 152.207.255.255. Data ini cocok dengan akun Robert Taylor Jr yang statusnya kontraktor. | Akun kontraktor masih punya akses admin penuh. Akun masih aktif walaupun end date sudah lewat lama. Level akses tidak sesuai dengan peran dan status kerja. Tidak ada pembatasan khusus untuk aktivitas sensitif seperti payroll. | Akses admin dibatasi hanya ke peran tertentu. Akun kontraktor dinonaktifkan setelah masa kerja selesai. Review akses dilakukan rutin. Aktivitas sensitif seperti payroll butuh approval tambahan atau MFA. |

Secara keseluruhan, tabel ini menunjukan kalau masalah utama bukan di sistem yang error, tapi di pengelolaan akses pengguna. Akun yang seharusnya sudah tidak aktif masih bisa melakukan aksi penting. Kontrol autentikasi dan otorisasi berjalan, tapi tidak dikawal dengan manajemen akun yang rapi. Kondisi ini membuat sistem gampang disalahgunakan tanpa perlu teknik serangan yang rumit.

 

