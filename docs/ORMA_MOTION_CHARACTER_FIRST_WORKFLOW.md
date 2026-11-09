# ORMA MOTION — Character-first & asset-first layered animation

**Status:** standar **perencanaan dan produksi** yang diminta Owner, 10 November 2026. Berlaku sebagai pedoman kerja lintas proyek di repository Orma Motion; **bukan klaim fitur auto-generator yang sudah terimplementasi**. Gunakan bersama `SKILL.md`, `references/anti-ppt.md`, `references/architecture.md`, dan, bila ada karakter ber-rig, `references/kartun-panggung.md`.

## 1. Masalah yang harus dihindari

Kegagalan nyata pada VISIBEL: dari satu foto/storyboard komposit dibuat mask karakter/latar/properti, lalu hasil potongannya digerakkan dengan zoom, pan, dan bubble di atas VO. Secara teknis bisa menghasilkan MP4, **tetapi itu bukan karakter animasi yang dirancang**; Owner menolaknya. Hasil yang punya parallax saja belum tentu mengandung akting/gerak yang bermakna.

**Aturan keras untuk produksi berbasis karakter:**
- **DILARANG** memakai satu frame hasil storyboard/poster/foto komposit sebagai sumber utama lalu memotong seluruh karakter dan properti dari frame itu demi mengklaim `2.5D layered animation`.
- **DILARANG** satu karakter = satu gambar utuh dengan hanya translate/scale/rotate lalu foto berganti; ganti pose/ekspresi atau gunakan rig yang memang memungkinkan aksi yang ditulis.
- **DILARANG** memulai uji video 8–12 detik saat pemeran, set, props, variasi sprite, dan action-state yang dibutuhkan oleh **seluruh** VO masih belum dipetakan.
- **DILARANG** menganggap storyboard yang indah, poster, contact sheet, atau snapshot UI sebagai bukti animasi berjalan.
- **DILARANG** mengarang kemampuan engine, menyebut karakter bisa melakukan gerakan natural tanpa pose/rig/footage pendukung, atau mengklaim video final dari rencana.

Pengecualian berbasis brief: foto/footage asli yang berizin boleh menjadi elemen dokumenter, kolase, UGC, atau hybrid iklan produk. Namun penggunaannya harus **disengaja**, bukan menggantikan character asset system saat Owner memilih animasi karakter.

## 2. Istilah dan sasaran

**Layered cutout animation:** karakter dan benda dibangun sebagai aset mandiri; dapat memakai rig sendi atau pergantian pose/sprite. **Multiplane/2.5D:** panggung punya bidang kedalaman terpisah (BG/far, middle, character, foreground, UI overlay) dengan perbedaan transform dan perspektif semu. **Sprite sheet / pose atlas:** kumpulan pose, arah dan ekspresi karakter yang sama yang dapat dipanggil ulang pada berbagai shot. Rig sendi dan sprite swap dapat digabung; keduanya tidak sama dengan crop dari satu foto final.

Visual dapat realistis, semi-realistis, ilustratif atau kartun sesuai produk. **2.5D realistis adalah kandidat utama untuk diuji pada iklan produk digital; bukan kewajiban pada semua proyek.** Produk fisik mungkin lebih tepat berupa footage produk + motion/UI hybrid. Motion dan styling adalah keputusan terpisah.

## 3. Urutan wajib — pikirkan seluruh film sebelum menciptakan aset

1. **Brief + verifikasi materi.** Baca VO yang disediakan, semua HTML/produk asli dan constraint iklan; ukur audio asli. Jangan mengganti isi VO. Uraikan seluruh durasi (bukan 12 detik pertama saja), alur sebab-akibat dan CTA.
2. **Full-video motion blueprint.** Pecah seluruh naskah menjadi beat yang punya tindakan. Untuk SETIAP beat, tentukan: siapa/apa yang muncul, lokasi, perubahan keadaan, interaksi, kamera, transisi, waktu, dan teknik (sprite swap, joint rig, UI animation, prop animation, footage, dll.). Kalimat VO **tidak harus** setara satu scene; sebuah panggung bisa memuat beberapa beat.
3. **CAST BIBLE seluruh film.** Daftarkan semua pemeran utama dan pendukung yang benar-benar diperlukan, karakter-ID konsisten, visual identitas, wardrobe, postur, prop yang dipegang, perspektif, arah tubuh (front / 3/4 left / 3/4 right / side bila relevan), dan perubahan emosi/aksi sepanjang film. Rencanakan **pose/action/expression matrix** dari seluruh beat sebelum asset generation pertama.
4. **SET & PROP BIBLE seluruh film.** Daftar semua background tiap lokasi **tanpa karakter tertanam**, objek midground/foreground, properti interaktif, dan state (laptop terbuka/tertutup, surat dibuka, dokumen menumpuk, UI berpindah halaman). Tentukan skala, titik jangkar dan occlusion.
5. **ASSET MANIFEST dan dependency graph.** Satu ID untuk tiap aset/revisi. Petakan asset -> beat/scene; mana dipakai ulang, mana perlu versi pose/angle, dan apa yang boleh dibangun dari SVG. **Perencanaan kebutuhan untuk 100% video harus lengkap sebelum menguji gerak.**
6. **Buat aset aslinya secara terpisah.** Buat master karakter/sprite/rig, termasuk pose dan ekspresi yang diperlukan; buat background, props, pemeran lain, UI/source captures secara mandiri. Atlas PNG alpha atau SVG rig bukan keharusan mutlak: format dipilih dari jenis aksi. Jangan menghasilkan satu poster lalu mengirisnya. Periksa identitas antarpose, alpha, anatomi, pertemuan tangan-prop, pivot, arah cahaya dan perspektif.
7. **Bangun panggung dan satu master timeline** di engine Orma Motion (HTML/CSS/SVG/GSAP, Three.js hanya bila perlu). Sambungkan layer asli, pergerakan pose/rig dan props, kamera, UI, VO, SFX. Kamera jangan menjadi satu-satunya yang bergerak.
8. **Motion proof sebelum full render.** Uji shot yang representatif **setelah cast/asset plan seluruh film tersedia dan aset kunci siap**; periksa aksi karakter (bukan crop zoom), hubungan objek, transisi, continuity dan sync. Jika gagal, betulkan pada pose/rig atau blocking, bukan tambal lagi dengan poster.
9. **Produksi dan QA MP4** hanya dengan izin produksi yang berlaku. Render frame deterministik dan uji per beat/scene; cek rasio/resolusi, frame, audio, decode, lisensi, dan relevansi visual; bedakan QA teknis dari penerimaan kreatif Owner.

**Gerbang:** jangan langsung membuat aset atau animasi hanya karena menerima brief/VO, kecuali Owner telah mengizinkan tahap itu. Saat Owner meminta pembahasan/standar saja, berhenti pada dokumentasi; tidak ada gambar/video baru.

## 4. Spesifikasi aset wajib untuk karakter yang benar-benar beraksi

Untuk tiap `character_id` simpan:

| Field | Fungsi |
|---|---|
| `identity` | Wajah, siluet, umur visual, baju, proporsi, warna, pencahayaan tetap |
| `views` | Arah yang dibutuhkan story: front / 3/4 / profile / belakang jika memang digunakan |
| `expressions` | Neutral, kecewa, cemas, berpikir, puas, atau kategori lain yang dipakai di seluruh film |
| `poses_and_actions` | Duduk, menunjuk, mengetik, mengambil berkas, menoleh, memberi gestur, dll., sesuai aksi nyata di script |
| `sprite_states` | Per kombinasi `view+expression+pose`, termasuk blink/mouth shape hanya jika benar-benar akan dianimasikan |
| `rig_segments` | Jika memakai rig: kepala, torso, lengan atas/bawah, tangan, paha/betis, sendi, hierarki parent-child, pivot lokal |
| `anchors` | Foot contact, seat point, hand/grip point, look target, z/depth group |
| `file_and_license` | Referensi berkas asli, revision/hash bila ada, hak penggunaan, transparansi/ukuran |

**Contoh struktur, bukan file yang sudah dibuat:**

```text
assets/
  characters/
    hero01/
      identity-sheet.png
      sprites/
        front-neutral-standing.png
        3q-left-disappointed-seated.png
        3q-left-working-typing.png
        3q-right-thinking.png
      rig/                 # opsional: kepala, torso, upper/lower arms, etc.
    manager01/
    colleague01/
  sets/
    office-desk/BG.png
    office-desk/foreground-desk.png
    meeting-room/BG.png
  props/
    laptop-open.png
    promotion-notice.png
    document-stack.png
  ui/
    product-home-capture.png
    playbook-capture.png
    action-map-capture.png
  production/
    full-video-beats.md
    asset-manifest.json
    motion-cues.json
```

Untuk foto-realistis, sprite swap perlu dibuat dengan identitas, pakaian, sudut, ukuran/perspektif yang konsisten; key poses dapat berupa cutout PNG alpha yang **dibuat khusus tanpa background**, bukan dari komposit storyboard. Untuk visual bergaya SVG, sendi bisa di-rig. Penggunaan rig tidak otomatis menyelesaikan akting; aksi harus disusun pada timeline dengan pose/pergerakan yang tepat. Jangan menyatakan sprite swap adalah motion tubuh penuh.

## 5. Template full-video breakdown (isi semuanya sebelum mulai generate)

| Beat/VO & time | Panggung BG / middle / foreground | Character ID + state | Props + state | **Aksi aktual** | Kamera + transisi | Asset IDs / method |
|---|---|---|---|---|---|---|
| 00:00–xx | lokasi A | hero01 expression01/pose02, colleague01 pose03 | announcement, chair | Pengumuman berubah → rekan ditunjuk → hero menoleh / bereaksi | dolly mengikuti subjek, cut reaksi | hero01/sprite02, ... |
| xx–xx | lokasi A tetap | hero01 pose04 | laptop, document | tangan ke keyboard → dokumen terkumpul → ceklis tercentang | kamera mengikuti prop | rig/pose, SVG |
| ... | ... | ... | ... | ... | ... | ... |

Contoh di atas hanya menjelaskan **struktur**; timing, adegan, jumlah pemeran/pose dan kontinuitas final harus diturunkan dari VO/produk proyek sebenarnya, bukan disalin.

Untuk setiap beat, pertanyaan pemeriksaan:
- Apa yang benar-benar **berubah di layar** akibat narasi?
- Aksi siapa? Dari state apa ke state apa?
- Layer mana bergerak relatif terhadap layer lain?
- Pose/sprite/rig apa yang **sudah tersedia** untuk aksi itu?
- Bagaimana kamera memperlihatkan aksi, bukan menggantikannya?
- Apa sumber screenshot produk? Apakah benar-benar memakai data/fitur asli?
- Apakah transisinya berasal dari aksi/ruang, bukan fade antarposter?

## 6. Contoh kebutuhan awal untuk VISIBEL (bukan keputusan casting final)

Master VO VISIBEL sekitar **55,68 detik**. Tes sebelumnya sekitar 12 detik dengan memotong subjek dari gambar komposit telah **ditolak Owner secara kreatif**. **Jangan pakai crop tersebut sebagai aset produksi baru.**

Sebelum uji ulang, **audit keseluruhan naskah** lalu tentukan minimal kategori kebutuhan:
- karakter karyawan utama dengan konsistensi identitas dan pose/emosi sesuai promosi terlewat, bekerja, kecewa, berpikir, dan mulai menyusun langkah;
- karakter pendukung yang memang dibutuhkan (rekan yang dipilih, atasan/pengumum) dengan sprite/pose sendiri; jumlah dibuat **berdasarkan kebutuhan cerita**, jangan mengarang pemeran tambahan;
- panggung kantor yang relevan (area kerja, pengumuman/meeting bila memang adegan), tiap BG terpisah dari karakter dan props;
- laptop, kursi, meja, berkas, pengumuman, telepon, serta state props yang dipakai;
- UI VISIBEL asli (The Visibility Framework, Situational Playbook, 30-Day Action Map) sebagai sumber interaksi, **bukan dashboard yang direka**;
- overlay grafis dan CTA tanpa harga; VO asli tidak diubah.

Urutan yang disarankan: full breakdown VO -> asset/cast bible & storyboard aksi bila perlu -> bangun sprite/rig dan set mandiri -> validasi kontinuitas -> motion proof -> video penuh setelah persetujuan.

## 7. QA yang wajib dilaporkan, jangan hanya menyatakan "sudah 2.5D"

**Asset QA:** apakah semua karakter dibuat mandiri; tidak berasal dari crop storyboard? apakah pose/ekspresi berbeda dan identitas tetap sama? latar tanpa karakter embedded? props reusable, anchor dan occlusion benar? scene inventory seluruh film sudah dipetakan?

**Motion QA:** minimal ada **aksi karakter atau objek** teramati per beat; pergerakan pose/rig tepat; bubble/UI bereaksi; shot variety; bukan hanya zoom/pan/crossfade. Periksa frame key **dan klip yang dimainkan**, bukan gambar saja. Jika sebuah aksi butuh rig dan rig belum ada, laporkan blocker dan ubah desain sebelum render.

**Technical QA:** durasi/VO, audio alignment, seek deterministik, batas frame, rasio portrait bila disepakati, alpha artifacts, konsistensi gerak antarscene, file render, decoder errors dan lisensi. QA teknis tidak sama dengan hasil kreatif maupun performa iklan.

**Status pencatatan:** `PLANNED` (blueprint) -> `ASSETS_PREPARED` -> `MOTION_PROOF_TESTED` -> `VIDEO_RENDERED/QA` -> `OWNER_ACCEPTED`. Jangan lompat tahap atau menyebut contoh struktur sebagai implementasi.

## 8. Batas dan referensi engine

Ini pedoman kerja yang bisa segera diterapkan **secara manual** dengan engine Bang Motion bawaan Orma; belum ada sistem otomatis yang memaksa asset manifest / sprite library / continuity QA. Pemrograman validator, sprite pipeline, portrait renderer, dan orchestration ke depan harus menjadi pekerjaan teknis tersendiri, hanya setelah persetujuan serta pengujian.

- `SKILL.md`: anti-PPT, director/style brief, deterministic motion.
- `references/kartun-panggung.md`: prinsip rig sendi dengan proxy lokal, ekspresi via head swap, gerak body part. **Ambil teknik**, tidak harus mengadopsi gaya kartun flat.
- `assets/starter-explainer-panggung.html`: contoh rig dan panggung yang hidup (bukan template visual yang wajib ditiru).
- `references/architecture.md`: master timeline, rig kamera, scrubbing dan export.
- `references/anti-ppt.md`: uji kegagalan slideshow/ken-burns.
- `scripts/export-frames.mjs`: contoh export dengan viewport asal 1920×1080; sesuaikan dan uji sendiri untuk 9:16, **bukan berarti portrait otomatis didukung untuk semua starter**.
