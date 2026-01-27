# Access control failure analysis on financial transaction incident

1. [Backkground](#background)
2. [Scenario overview](#scenario)
3. [Incident evidence](#incident)
4. [Access control worksheet](#worksheet)
5. [Key takeaways and insights](#insight)
6. [Conclusion](#conclusion)

---

## 🧠 Background <a name="background">

Studi kasus ini saya buat sebagai latihan cybersecurity dengan fokus pada penilaian kontrol akses di lingkungan bisnis yang sedang berkembang. Skenario menggambarkan kondisi ketika perusahaan menghadapi transaksi keuangan yang tidak dikenali dan tim keamanan perlu memahami bagaimana akses sistem digunakan sebelum menentukan langkah pengamanan yang tepat.

Latihan ini mengacu pada Google Cybersecurity Professional Certificate, khususnya course Assets, Threats, and Vulnerabilities serta pembahasan access control. Proses analisis dimulai dengan meninjau event log untuk melihat aktivitas pengguna, dilanjutkan dengan pencocokan data tersebut dengan direktori karyawan. Hasil peninjauan digunakan sebagai dasar untuk mengidentifikasi kelemahan authentication dan authorization, lalu menyusun rekomendasi perbaikan yang realistis sesuai konteks operasional bisnis.

---

## 🧩 Scenario overview <a name="scenario">

Skenario ini menempatkan saya sebagai profesional keamanan siber pertama di sebuah bisnis yang sedang berkembang. Masalah muncul ketika ditemukan adanya setoran ke rekening bank yang tidak dikenal. Manajer keuangan memastikan tidak pernah melakukan transaksi tersebut dan pembayaran berhasil dihentikan sebelum dana benar-benar terkirim.

Pemilik bisnis kemudian meminta dilakukan penelusuran untuk memahami apa yang sebenarnya terjadi dan mencegah kejadian serupa. Proses analisis dimulai dengan meninjau log akses sistem yang mencatat aktivitas terkait insiden. Data tersebut dipakai untuk mengidentifikasi pengguna yang terlibat dan melihat pola akses yang mencurigakan. Informasi ini kemudian dicocokkan dengan data karyawan untuk menemukan kelemahan kontrol akses yang dimanfaatkan. Hasil temuan menjadi dasar penyusunan rekomendasi mitigasi yang lebih masuk akal dan relevan dengan kondisi operasional bisnis.

---

## 📄 Incident evidence <a name="incident">

Bagian ini menyajikan data mentah yang digunakan dalam proses analisis insiden. Informasi ditampilkan langsung berdasarkan hasil pencatatan sistem dan direktori karyawan, tanpa interpretasi atau kesimpulan.

### Event log summary

Tabel berikut menunjukkan detail log kejadian yang tercatat oleh sistem saat insiden payroll terjadi:

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

Tabel berikut menampilkan data direktori karyawan yang tercatat dalam sistem pada waktu insiden terjadi:

| Name              | Role             | Email                                                   | IP Address      | Status     | Authorization | Last Access                  | Start Date | End Date   |
| ----------------- | ---------------- | ------------------------------------------------------- | --------------- | ---------- | ------------- | ---------------------------- | ---------- | ---------- |
| Lisa Lawrence     | Office manager   | [l.lawrence@erems.net](mailto:l.lawrence@erems.net)     | 118.119.20.150  | Full-time  | Admin         | 12:27:19 pm (0 minutes ago)  | 10/01/2019 | N/A        |
| Jesse Pena        | Graphic designer | [j.pena@erems.net](mailto:j.pena@erems.net)             | 186.125.232.66  | Part-time  | Admin         | 4:55:05 pm (1 day ago)       | 11/16/2020 | N/A        |
| Catherine Martin  | Sales associate  | [catherine_M@erems.net](mailto:catherine_M@erems.net)   | 247.168.184.57  | Full-time  | Admin         | 12:17:34 am (10 minutes ago) | 10/01/2019 | N/A        |
| Jyoti Patil       | Account manager  | [j.patil@erems.net](mailto:j.patil@erems.net)           | 159.250.146.63  | Full-time  | Admin         | 10:03:08 am (2 hours ago)    | 10/01/2019 | N/A        |
| Joanne Phelps     | Sales associate  | [j_phelps123@erems.net](mailto:j_phelps123@erems.net)   | 249.57.94.27    | Seasonal   | Admin         | 1:24:57 pm (2 years ago)     | 11/16/2020 | 01/31/2020 |
| Ariel Olson       | Owner            | [a.olson@erems.net](mailto:a.olson@erems.net)           | 19.7.235.151    | Full-time  | Admin         | 12:24:41 pm (4 minutes ago)  | 08/01/2019 | N/A        |
| Robert Taylor Jr. | Legal attorney   | [rt.jr@erems.net](mailto:rt.jr@erems.net)               | 152.207.255.255 | Contractor | Admin         | 8:29:57 am (5 days ago)      | 09/04/2019 | 12/27/2019 |
| Amanda Pearson    | Manufacturer     | [amandap987@erems.net](mailto:amandap987@erems.net)     | 101.225.113.171 | Contractor | Admin         | 6:24:19 pm (3 months ago)    | 08/05/2019 | N/A        |
| George Harris     | Security analyst | [georgeharris@erems.net](mailto:georgeharris@erems.net) | 70.188.129.105  | Full-time  | Admin         | 05:05:22 pm (1 day ago)      | 01/24/2022 | N/A        |
| Lei Chu           | Marketing        | [lei.chu@erems.net](mailto:lei.chu@erems.net)           | 53.49.27.117    | Part-time  | Admin         | 3:05:00 pm (2 days ago)      | 11/16/2020 | 01/31/2020 |

## 🧠 Access control worksheet <a name="worksheet">





