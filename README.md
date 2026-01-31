# Access control failure analysis on financial transaction incident

1. [Backkground](#background)
2. [Scenario overview](#scenario)
3. [Incident evidence](#incident)
4. [Access control worksheet](#worksheet)
5. [Conclusion](#conclusion)

---

## 🧠 Background <a name="background">

Studi kasus ini saya kerjakan sebagai latihan cybersecurity yang membahas kontrol akses dan kejadian finansial di sistem bisnis. Skenario ini menggambarkan perusahaan yang lagi berkembang dan mulai banyak mengandalkan sistem digital untuk mengurus transaksi penting, termasuk urusan keuangan. Kondisi ini bikin saya sadar kalau satu aktivitas kecil bisa punya dampak besar saat akses pengguna tidak dijaga dengan baik.

Latihan ini mengacu ke materi Google Cybersecurity Professional Certificate, terutama course Assets, Threats, and Vulnerabilities. Pembahasan saya mulai dengan melihat aset apa yang paling penting di kasus ini, lalu menelusuri ancaman dan celah yang muncul lewat penggunaan akun. Proses ini memberi pemahaman kalau risiko tidak selalu muncul karena serangan teknis, tapi sering muncul karena kontrol akses yang terlalu longgar dan kurang dipantau.

---

## 🧩 Scenario overview <a name="scenario">

Skenario ini menggambarkan bisnis yang lagi berkembang dan baru punya divisi khusus di bidang cyber security. Posisi saya di sini sebagai orang pertama yang ngurus soal keamanan sistem. Masalah mulai kelihatan saat ada setoran uang ke rekening bank yang tidak dikenal. Tim keuangan merasa tidak pernah melakukan transaksi itu dan pembayaran berhasil dihentikan sebelum muncul kerugian.

Tugas saya di skenario ini lebih ke mencari tahu apa yang sebenarnya terjadi. Prosesnya saya mulai dengan melihat log akses yang berkaitan dengan kejadian tersebut. Log ini membantu melihat aktivitas akun, waktu akses, dan kemungkinan penyalahgunaan akun. Catatan kecil saya kumpulkan untuk menebak siapa yang terlibat dan bagaimana akses itu bisa terjadi.

Langkah selanjutnya saya melihat kontrol akses yang dipakai di sistem. Bagian ini bikin saya paham celah yang dimanfaatkan, seperti hak akses yang terlalu luas atau akun yang seharusnya sudah tidak aktif. Skenario ini saya tutup dengan menyusun rekomendasi sederhana berdasarkan temuan tadi supaya kontrol akses lebih tertata dan kejadian serupa tidak mudah terulang.

---

## 📄 Incident evidence <a name="incident">

### Event log summary

Bagian ini saya cek untuk memahami aktivitas di sistem saat insiden terjadi. Event log memperlihatkan perubahan penting yang berkaitan dengan payroll dan rekening bank, lalu jadi petunjuk awal soal akun yang dipakai dan kapan kejadiannya.

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

Bagian ini saya gunakan untuk mencocokkan IP address dengan akun yang muncul di log. Fokus ke siapa saja yang masih pegang akses admin dan status akunnya sekarang. Beberapa akun terlihat sudah tidak aktif secara kontrak, tapi masih tercatat punya akses penuh.

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

## 🔐 Access control worksheet <a name="worksheet">

Bagian ini berisi ringkasan hasil pengamatan soal kontrol akses di insiden ini. Fokus ke siapa yang melakukan aktivitas, jenis akses yang dipakai, dan celah yang terlihat saat data log dibandingkan dengan direktori karyawan. Tabel ini bantu saya melihat masalah secara sederhana tanpa ribet, jadi alurnya tetap masuk akal walau cuma pakai log dan data dasar.

| Area Kontrol           | Catatan                                                                                                                                                                                                                   | Masalah                                                                                                                                                                                                                 | Rekomendasi                                                                                                                                                                                      |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Otorisasi / otentikasi | Insiden tercatat 10/03/2023 pagi. Aktivitas pakai akun Legal\Administrator. Perangkat tercatat sebagai komputer Up2-NoGud dengan IP 152.207.255.255. Data ini nyambung ke akun Robert Taylor Jr dengan status kontraktor. | Akun kontraktor masih pegang akses admin penuh. Akun tetap aktif walau masa kontrak sudah lama selesai. Hak akses tidak sejalan dengan peran kerja. Aktivitas sensitif seperti payroll tidak punya pembatasan tambahan. | Akses admin dibatasi ke peran tertentu saja. Akun kontraktor dinonaktifkan saat masa kerja selesai. Review akses dilakukan rutin. Aktivitas sensitif seperti payroll ditambah approval atau MFA. |

Secara keseluruhan, tabel ini menunjukan kalau masalah utamanya bukan karena sistem bermasalah. Pengelolaan akses pengguna jadi titik lemah terbesar. Akun yang seharusnya sudah tidak aktif masih bisa jalan dan melakukan aksi penting. Autentikasi dan otorisasi sebenarnya ada, tapi manajemen akun kurang terjaga. Kondisi seperti ini bikin sistem rawan disalahgunakan tanpa teknik serangan yang ribet.

---

## 🏁 Conclusion <a name="conclusion">

Kesimpulan yang saya tarik dari kasus ini cukup jelas dan sederhana. Masalah utamanya bukan serangan teknis yang rumit. Akar masalahnya ada di kontrol akses yang longgar dan tidak terpantau dengan baik. Akun yang status kerjanya sudah selesai masih punya akses admin dan bisa melakukan perubahan sensitif.

Kasus ini bikin saya sadar kalau sistem yang kelihatan aman tetap bisa bermasalah kalau manajemen akun tidak rapi. Event log sebenarnya sudah memberi petunjuk jelas, tapi tanpa review rutin, risiko seperti ini gampang terlewat. Kontrol akses bukan cuma soal login berhasil atau tidak, tapi juga soal siapa yang pantas pegang akses dan sampai kapan.

Latihan ini membantu saya memahami bahwa keamanan sistem sangat bergantung pada disiplin pengelolaan user. Tanpa itu, satu akun saja sudah cukup untuk bikin dampak besar ke bisnis, apalagi yang menyangkut keuangan.
