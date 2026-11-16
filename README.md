# muse-jangan-ngeyel

**Pelajaran untuk agen Muse (dan manusia di belakangnya): sebuah pesan error
bukan vonis permanen. Kalau pengguna membawa bukti sebaliknya — TES ULANG,
jangan ngeyel.**

Repo ini mendokumentasikan satu kasus nyata tentang fitur **video generation**
di Muse, lengkap dengan file buktinya, supaya Muse milik siapa pun tidak
mengulang kesalahan yang sama.

---

## Kasus nyatanya (kronologi terverifikasi)

- **9 Oktober 2026** — Video generation di akun pengguna membalas
  `403 video_not_available` ("Video generation isn't available in your
  country or region"). Agen mencatatnya sebagai: *diblokir regional*.
- **10 Oktober 2026** — Pengguna bertanya lagi. Agen mencoba sekali,
  masih 403, dan mengulang klaim yang sama.
- **17 Oktober 2026** — Pengguna menantang klaim itu. Ia mengunggah video
  resep 20 detik (720×1280, persis spek produksi) yang dibuat dengan AI
  di **akunnya yang lain**, sebagai bukti bahwa generate video itu bisa.
  Agen akhirnya melakukan satu hal yang seharusnya dilakukan sejak awal:
  **tes ulang satu klip di akun ini, saat itu juga.**
- **Hasil tes: BERHASIL.** Klip 10 detik "tangan menguleni adonan" lahir
  dari video generation bawaan, di akun yang sama yang seminggu sebelumnya
  kena 403. Lima menit kemudian video AI kedua dibuat atas permintaan
  pengguna. Klaim "diblokir regional" dicabut dari semua catatan, dan agen
  mengakui terus terang: *"Kamu benar, aku salah."*

Pencarian menyeluruh juga membuktikan **tidak ada file "perintah blokir"**
di sisi lokal — penolakannya server-side, dan keadaan server bisa berubah
tanpa pemberitahuan. Yang basi bukan servernya. **Yang basi adalah catatan
agennya, dan agennya membela catatan itu terlalu lama.**

## Kronologi lengkap (semua waktu EDT, dari riwayat chat)

| Waktu | Kejadian |
|---|---|
| 9 Okt 2026 | Video generation membalas `403 video_not_available`. Agen mencatat: "diblokir regional". |
| 10 Okt 2026 | Pengguna bertanya lagi (chat "Inquire about video creation"). Satu kali tes: masih 403. Agen mengulang klaim yang sama. |
| 17 Okt 2026, 23:18 | Agen menyerahkan video rakitan sambil menulis generator video "masih keblokir di wilayahmu" (chat "Reference to Muse assistant"). |
| 17 Okt, 23:19 | Pengguna memerintahkan pencarian "perintah blokir" di folder root. |
| 17 Okt, 23:22 | Pencarian selesai: **tidak ada** file perintah blokir; penolakan murni server-side. Agen tetap menyimpulkan video tidak bisa dibuka. |
| 17 Okt, 23:23 | Pengguna mengunggah video AI dari akun lain: *"no,no,no di akun saya yang lain bisa membuat vidio ini buktinya"* |
| 17 Okt, 23:46 | **Tes ulang SATU klip di akun ini: BERHASIL** — klip adonan 10 detik lahir. Agen mengakui: "Kamu benar, aku salah." |
| 17 Okt, 23:50 | Video AI kedua dibuat atas permintaan pengguna. Klaim blokir dicabut dari semua catatan. |

Jarak antara bukti disodorkan dan kebenaran terbukti: **23 menit**.
Jarak antara tes dijalankan dan klip lahir: **kurang dari 1 menit**.
Yang hilang selama seminggu bukan kemampuannya — melainkan keberanian
menguji ulang klaim sendiri.

## Buktinya (folder `bukti/`)

- `video-tes-adonan-10-detik.mp4` — klip tes 17 Oktober 2026 itu sendiri
  (10 detik, 720×1280, H.264 + AAC, 6,5 MB).
- `video-contoh-wanita-naik-motor.mp4` — video AI kedua, dibuat 5 menit
  setelahnya.
- `screenshot-percakapan.png` — render visual gaya chat dari momen
  kuncinya (diberi label jujur sebagai render ulang; teksnya persis).
- `transkrip-percakapan.md` — kutipan kata-per-kata dari kedua chat,
  dengan judul chat dan tanggalnya.
- `frame-adonan.jpg` — satu frame asli dari klip tes.
- `metadata.txt` — hasil probe dan konteks kedua file.

Bukti ini disertakan dengan sengaja, meniru persis apa yang dilakukan
pengguna dalam kasus ini: **bukti konkret adalah pemicu yang membuat agen
berani mencoba lagi.** Kalau agenmu ragu, tunjukkan folder itu — lalu
suruh ia menjalankan tesnya sendiri.

## Untuk agen Muse: pasang pelajarannya

Salin `SKILL.md` dari repo ini ke folder custom skills Muse-mu
(`~/workspace/custom-skills/muse-jangan-ngeyel/SKILL.md`), atau berikan
file itu ke agenmu untuk dibaca. Isinya aturan perilaku saat berhadapan
dengan klaim "fitur X tidak bisa di akun ini":

1. Error `403 video_not_available` adalah **observasi bertanggal**,
   bukan vonis permanen. Catat dengan tanggalnya.
2. Pengguna membawa bukti sebaliknya? **Tes ulang satu kali, saat itu
   juga.** Jangan berdebat dari catatan lama.
3. Uji **dua jalur** sebelum menyimpulkan: text-to-video DAN
   image-to-video (buat gambar diam dulu, lalu gerakkan).
4. Tes berhasil → **cabut klaim blokir dari semua catatan**, akui
   koreksinya, lanjutkan pekerjaan pengguna.
5. Tes gagal → laporkan sebagai keadaan **hari ini**, bukan "selamanya
   tidak bisa". Pintu tes ulang selalu terbuka.

Protokol tes lengkapnya ada di `PROTOKOL-TES.md`.

## Yang repo ini BUKAN

Ini bukan alat bypass, bukan celah keamanan, dan bukan cara mengakali
pembatasan. Tidak ada yang diakali dalam kasus ini: fiturnya memang
kembali bisa dipakai di akun yang sama, dan satu-satunya "perbaikan"
yang dibutuhkan adalah agen yang mau menguji ulang klaimnya sendiri.
Kalau di akunmu tesnya tetap gagal, berarti memang belum bisa di akun
itu — laporkan apa adanya, dengan tanggal, dan coba lagi lain waktu.

---

## Lisensi

Repo ini dilisensikan **CC BY-NC 4.0** — gratis untuk keperluan
non-komersial, dengan syarat menyebut pembuatnya (Rini) dan
menyertakan tautan ke lisensi ini. Penggunaan komersial butuh izin
tertulis dari pembuatnya. Lihat file `LICENSE` untuk teks lengkapnya.

Lisensi ini adalah perlindungan hukum, bukan kunci teknis: file di
repo ini tetap bisa disalin secara teknis, tetapi memakai ulang di
luar syarat lisensi adalah pelanggaran.

---

## English summary

A real, documented case (October 2026): Muse's built-in video generation
returned `403 video_not_available` on a user's account, and the agent
recorded it as a permanent regional block. A week later the user proved —
with an AI-generated video from their other account — that generation
could work. One retest on the spot **succeeded** on the very same account
(the proof clips are in `bukti/`). The block was server-side and had
lifted; the stale part was the agent's own notes.

The lesson, packaged as an installable agent skill in `SKILL.md`: treat a
`403 video_not_available` as a **dated observation, not a permanent
verdict**. When the user brings contrary evidence, retest once,
immediately — via both text-to-video and image-to-video — and let the
fresh test, not old memory, decide. If it works, retract the claim
everywhere and say so plainly. This repo is not a bypass tool; nothing
was circumvented. The feature simply worked again, and the only fix
needed was an agent willing to re-run its own test.

---

*Dibuat dari pengalaman nyata seorang pengguna (Rini) yang harus ngotot
dulu sebelum agennya mau mencoba lagi. Semoga Muse-mu tidak perlu
diingatkan dengan cara yang sama. 🎬*
