# PROTOKOL TES — Membuktikan Video Generation Bisa / Tidak, Dalam ±1 Menit

Dipakai saat ada klaim "video generation diblokir di akun ini" — baik
klaim itu datang dari catatan agen sendiri maupun dari error barusan.
Satu kali jalan, satu klip, keputusan dari bukti.

## Langkah

1. **Text-to-video, satu klip pendek.**
   - Durasi: 10 detik. Format: vertikal 9:16 (720×1280) atau default
     lingkunganmu.
   - Prompt harus berisi GERAKAN yang jelas dan sederhana, contoh:
     "Tangan menguleni adonan roti di meja kayu, gerakan lambat dan
     mulus, cahaya dapur hangat." (Prompt statis tidak membuktikan
     apa-apa — yang diuji adalah video beneran.)
   - Jalankan SEKALI. Jangan mengulang-ulang panggilan yang ditolak
     sistem; satu tes yang bersih cukup untuk keputusan hari ini.

2. **Kalau text-to-video ditolak DAN image-to-video tersedia:**
   - Buat satu gambar diam (mis. dari prompt yang sama).
   - Gerakkan gambar itu jadi video (image-to-video), satu kali.
   - Jalur ini kadang lolos saat jalur teks gagal — dan sebaliknya.
     Kesimpulan "diblokir" hanya sah kalau yang diuji memang jalurnya
     sudah dicoba.

3. **Verifikasi hasilnya seperti orang yang tidak percaya.**
   - File video benar-benar ada? Ukurannya masuk akal (MB, bukan KB)?
   - Probe: codec video + resolusi + durasi sesuai permintaan?
   - Ambil SATU frame (mis. detik ke-3) dan lihat: ada gambarnya?
   - Cek gerakannya: bandingkan frame awal vs frame akhir — berubah
     karena gerakan, bukan slideshow hasil rakitan sendiri.

## Keputusan

| Hasil | Kesimpulan yang SAH ditulis |
|---|---|
| Klip lahir & terverifikasi | "Video generation BISA di akun ini (terbukti <tanggal>)." Cabut semua klaim blokir lama. |
| 403 `video_not_available` | "Per <tanggal> video generation masih membalas 403 di akun ini." — titik. Bukan "selamanya", bukan "regional permanen". |
| Error lain | Catat error persisnya + tanggal. Jangan diterjemahkan jadi "diblokir". |

## Contoh nyata

Protokol ini persis yang mengakhiri kasus di README repo ini:
9 Okt 2026 → 403. 17 Okt 2026 → satu tes seperti di atas → klip adonan
10 detik lahir (lihat `bukti/`). Klaim basi berumur seminggu gugur oleh
satu tes berumur satu menit.

---

## English version (short)

1. Generate ONE short clip (10s) via text-to-video with a clear, simple
   motion prompt. Once — do not hammer a denied call.
2. If text-to-video is denied and image-to-video exists, generate a
   still and animate it, once.
3. Verify like a skeptic: file exists, sane size, probe shows expected
   codec/resolution/duration, extract a frame, confirm real motion.
4. Decide from the fresh result only: success = the feature works,
   retract older block claims everywhere; a 403 = "as of <date>, still
   403 on this account" — never "permanently unavailable".
