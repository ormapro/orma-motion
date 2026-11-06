# ORMA MOTION — Technical Development Handoff & Reference Register

**Tanggal:** 06 November 2026 WIB
**Status:** Tahap A audit statis selesai; Tahap B visual research / arsitektur konsep AKTIF, BELUM DI-ACC final; Tahap C implementasi BELUM DIMULAI.
**Repository source:** https://github.com/ormapro/orma-motion (main)
**Koordinasi utama:** https://github.com/omar-mcht/orma-member-area — docs/motion/ORMA_MOTION_COORDINATION_HANDOFF_2026-11-06.md
**Nama proyek:** Orma Motion. Nama calon produk Arpa Motion masih sementara.

## 1. Scope dan batas repo

Orma Motion adalah proyek terpisah untuk AI-assisted motion graphics dan video ads. ChatGPT Project OrmaPro Member Area dipakai untuk koordinasi, decisions, pending work, dan continuity. Jangan mengubah kode Member Area, Supabase, atau Vercel hanya karena motion dibahas dalam project chat. Tidak ada keputusan mengintegrasikan Orma Motion sebagai produk di portal.

Repository ini adalah sumber teknis untuk engine, skill, references, visual standards, script, dan kelak tes/video proof. Source Bang Motion v1.19.0 telah diimpor beserta riwayat Git aslinya; pada pemeriksaan 06 Nov 2026 HEAD main c1aa65e921c970d858705fcb4a53a8294d1a4131 sama dengan upstream bangtutorial/bang-motion. LICENSE MIT dengan Copyright (c) 2026 Bang Tutorial harus dipertahankan. Semua dependency, contoh, media, dan asset pihak ketiga perlu audit lisensi sendiri. Repository public; tidak boleh menyimpan secrets/API key.

**Perubahan dokumen handoff ini bukan perubahan engine.** Jangan edit SKILL.md/README.md/CHANGELOG.md upstream dan jangan menjalankan kode atau deploy sebelum rencana implementasi disetujui.

## 2. Visi sistem dan ruang lingkup (arah disepakati, belum terimplementasi)

Target jangka panjang: prompt sederhana -> pemahaman tujuan -> script/storyboard -> pemilihan visual -> asset/voice opsional -> timeline -> sound effect -> render MP4 -> QA/revisi. Dibutuhkan video edukasi, dokumenter/sejarah, YouTube/creator, iklan produk digital, serta iklan hybrid dari footage asli; tidak terbatas pada satu genre atau platform.

**Tidak ada spesifikasi universal 30 detik/9:16/1080p/30fps.** Format, resolusi, durasi, rasio, subtitle, dan sumber VO mengikuti brief atau rekomendasi AI berdasarkan tujuan. 9:16 dan 30 detik umum untuk kebutuhan pribadi tetapi hanya contoh benchmark, bukan batas engine atau standar kualitas.

Voiceover pilihan: rekaman pengguna, ElevenLabs/voice AI lain, atau tanpa narasi. Audio nyata bila ada menjadi acuan timing visual; jangan mengasumsikan durasi dari jumlah kata saja. Integrasi ElevenLabs bukan dependency wajib dan belum diuji secara end-to-end. Personal mode dan calon commercial mode menggunakan engine sama, mungkin berbeda alur interaksi; bentuk produk, harga, distribusi, dan UI komersial belum diputuskan.

## 3. Audit statis Bang Motion (terverifikasi hanya di source)

- SKILL.md dan references/{architecture,anti-ppt,explainer,kartun-panggung,opener-konsep,techniques,roadmap}.md memuat aturan anti-slide, kamera, GSAP timeline deterministik, style brief, enam gaya explainer, dan visual QA.
- assets/starter-opener.html dan starter-explainer*.html menyediakan starter opener, kolase, kartun panggung, jurnalisme, katalog, sketsa, dan continuous motion.
- scripts/snap.mjs untuk screenshot detik kunci, scripts/vo-pauses.html untuk analisis jeda VO, scripts/export-frames.mjs untuk render PNG via Puppeteer. MP4 final perlu FFmpeg.
- Bang Motion v1.18+ punya clip() untuk video footage sebagai layer yang mengikuti waktu timeline.
- Gap: belum ada orchestration input prompt -> MP4 dengan VO/SFX lengkap; belum ada sistem AI Visual Director yang diuji, voice provider adapter, QA otomatis end-to-end, 3D pipeline matang, atau flexible render resolution/audio mux integration. export-frames.mjs pada baseline memakai viewport/screenshot 1920x1080 tetap dan contoh output silent. Ini temuan source, bukan bukti uji runtime.
- Pengujian awal owner (kualitatif, belum apple-to-apple): ChatGPT Free kurang bagus, GPT-6 High chat biasa kurang bagus, Work Astra Medium sedang/ElevenLabs berfungsi, Codex Astra High visual lebih bagus tetapi ElevenLabs error. Perbandingan environment/effort setara belum dilakukan. Jangan menyimpulkan platform terbaik.

## 4. Visual Director & Style Book — rancangan tahap B, belum ACC final

Istilah kerja: **Orma Visual Director** (memilih cerita, adegan, teknik, aset dan kamera) dan **Orma Style Book** (catalog referensi dan prinsip lintas proyek). **Style Bible** adalah konsistensi spesifik setiap produksi; semua nama masih bisa berubah.

Pisahkan konsep: visual style (appearance), motion style (gerak objek/kamera), storytelling style (cara menjelaskan), art direction (konsistensi). Topik sejarah/sains/ekonomi bukan template tetap. Satu video boleh menggunakan karakter sederhana, 2D puppet, foto arsip, peta, diagram, footage, 3D simulation, kinetic typography dan UI. AI memilih teknik untuk tiap adegan serta menjaga keseluruhan tetap koheren. Pengguna kelak boleh memakai Auto Director (AI memilih), Guided (preferensi), Custom (prompt per adegan). Ini konsep, bukan fitur yang sudah dibuat.

Rencana library menyimpan: nama pendekatan, cocok untuk, teknik visual/gerak, kapan dipilih, sumber contoh & timestamp, teknologi, hak lisensi, QA outcomes dan status diuji/belum.

Prioritas riset visual:
1. Character-led 2D/2.5D/3D explainer (karakter sederhana benar-benar beraksi di dunia bercerita).
2. 2D mechanism/diagram/map/data animation, bukan PPT.
3. Historical/documentary editorial collage + footage autentik berlisensi.
4. Hybrid product and digital ads, sumber referensinya masih kurang.
5. Konsistensi aset/karakter dan scene-level revision melalui prompt.

Level teknologi yang akan dievaluasi, bukan otomatis diadopsi: Bang Motion HTML/CSS/SVG/GSAP; Three.js untuk ruang 3D ringan; Blender/Python untuk adegan 3D kompleks; FFmpeg untuk audio mux/cuts; sumber video/foto/AI sesuai kebutuhan dan lisensi.

## 5. Benchmark — rancangan revisi, bukan gate final

Penilaian utama: storytelling/kejelasan pesan, kualitas motion yang bermakna, komposisi & konsistensi visual, kepatuhan instruksi pengguna, kualitas audio bila relevan, serta finishing. Pemeriksaan teknis terpisah: output benar-benar sesuai rasio/durasi/resolusi yang diminta, tidak blank/freeze, audio utuh/sinkron, font/aset ada. Video yang lebih pendek/panjang atau berbeda orientasi tidak dihukum semata-mata karena format.

Perbandingan Work vs Codex harus memakai prompt, source commit, audio/aset dan spec uji yang sama. Catat waktu, jumlah iterasi, pengeluaran API, error, dan skor visual. Bobot dan passing threshold sebelumnya diusulkan, BELUM disetujui sebagai standar final. Uji render frame-by-frame dan QA owner belum dilaksanakan pada engine Orma.

## 6. Register referensi yang diketahui (source & proof)

### 6a. Sepuluh video edukasi yang dikirim sebagai upload chat, ditinjau secara sampling visual

- Malin Kundang: Langit pun Murka — https://www.youtube.com/watch?v=8WSVVnLQfwg (cerita ilustratif)
- Titanic 1912 — https://www.youtube.com/watch?v=tYvChCgMDak (mekanisme & sejarah)
- Tembok Besar China — https://www.youtube.com/watch?v=niIJPCDloo8 (sejarah/mitos)
- Baterai HP Saat Dicas — https://www.youtube.com/watch?v=sU0oqmmFtZ4 (mechanism)
- Komodo Betina — https://www.youtube.com/watch?v=9qhtz25jIMs (sains)
- Gerhana Matahari Total — https://www.youtube.com/watch?v=22Yvkt_CXGA (minimalist science)
- Why Perfect Railroads Don't Work — https://www.youtube.com/watch?v=7xS87iActkU (character-led 3D)
- This Shape Saved Roller Coasters — https://www.youtube.com/watch?v=QlDPMzGmYac (character-led 3D)
- Krakatau 1883 — https://www.youtube.com/watch?v=a_jKcbZnWPc (edukasi berdurasi panjang)
- Bulan Mengikuti Mobil — https://www.youtube.com/watch?v=wh1EkBVTyek (visual penjelasan 2D)

**Catatan:** file MP4 berada pada attachment ChatGPT; belum di-commit ke GitHub dan tidak bisa diasumsikan tetap tersedia lewat GitHub. URL eksternal juga tidak menjamin akses permanen atau izin redistribusi.

### 6b. Tutorial yang dikirim sebagai upload chat

- I Tried Making a Viral Video Using ONLY Claude AI — https://www.youtube.com/watch?v=kDcxEIDC5NA (skill/story -> script -> VO -> animasi).
- How I made Zach D Film Style video for $0 Using Claude — https://www.youtube.com/watch?v=uIqegmTmRUw (Blender/Python dan style-analysis/revision).
- Belum Banyak yang Tahu! Bongkar Rahasia Bikin Animasi Berbicara & Animasi 3D Pakai Claude Gratis! — https://www.youtube.com/watch?v=LWR3q8FyflI (contoh animasi berbicara/3D; belum membuktikan satu pipeline otomatis).

### 6c. File sumber referensi dari Google Drive — metadata & audit statis terpisah

- Cartoon audio short SKILL.md: https://drive.google.com/open?id=1VV9w5JKzV2i8Mzoh_zEfkXyX3lhzBYCJ — panduan kartun bean-head 2D pada dunia 3D; suara owner tidak diubah; audio dan timing. Konten Markdown terbaca di sesi.
- cartoon-short-kit.zip: https://drive.google.com/open?id=1VNvNonHXP_eDOaM87eb3qJkNbVDyp8tL — ZIP 19 entry termasuk engine/main.js, roman.js, motion.js, paint.js, story sample, scripts/timing/render/finish; tidak boleh dijalankan tanpa dependency/security/license review. Tidak terlihat mix.py di ZIP walau dirujuk skill.
- motion-graphics-by-nalarka.skill: https://drive.google.com/open?id=16s6JVw0hRuw8b_1EVj5XEjHBELHtt-Tw — ZIP kecil tiga file: SKILL.md, references/panduan-visual.md, references/render-dan-verifikasi.md; resep/prosedur, bukan bukti engine siap pakai.

Referensi dari luar dan alat AI belum di-approve untuk disalin, diinstal, dijual, atau diklaim hasil produksi Orma. Simpan hanya tautan dan pelajaran umum sampai lisensi jelas.

## 7. Roadmap Orma Motion (berbeda dari 7 tahap roadmap portal Member Area)

- **A — Audit Baseline:** pembacaan statis repo + gap awal DONE; smoke/runtime benchmark BELUM.
- **B — Visual Reference & Development Plan:** AKTIF. Finalisasi Style Book v0, taxonomy visual, pemilihan engine 2D/3D, standar QA, format prompt, dan benchmark; Owner ACC BELUM.
- **C — Implementasi terarah:** BELUM ADA IZIN. Batch kecil bisa dimulai setelah keputusan final dan batas license/security. Jangan langsung buat dashboard atau menimpa Bang Motion upstream.
- **D — Produk nyata:** Edukasi transportasi/tol Jawa, Signalof digital product ad, Elbrush hybrid footage — semua masih kandidat uji, bukan hasil.
- **E — Packaging komersial:** AI Skill / toolkit / ChatGPT Project / aplikasi mandiri BELUM diputuskan. Legal/license/commercial QA wajib.

## 7A. Cross-chat learning 06 Nov — empat level visual dan prioritas personal-first

**Rekonsiliasi diskusi pada ChatGPT Project lain:** Istilah Level 1–4 ditemukan sebagai **usulan assistant**, BUKAN taxonomy yang telah di-ACC final oleh Owner. Rincian usulannya: (1) motion 2D sederhana: tipografi, grafik/peta/ilustrasi; (2) motion 2.5D: layer, parallax, depth/camera; (3) character & scene animation: orang sederhana melakukan aksi di scene bercerita; (4) motion 3D/scientific visualization: objek 3D, simulasi mekanisme/cutaway. **Level bukan ranking kualitas dan satu video tidak dikunci pada satu level.** Shot bisa memakai berbagai level sesuai tujuan; footage live-action, stock video, user clips, AI B-roll dan overlays bisa dicampur lintas level. Semua istilah perlu diverifikasi lewat contoh, tidak boleh dipaksakan sebagai pipeline wajib.

**Teknologi yang pernah didiskusikan:** Remotion diperhitungkan sebagai kandidat modul editing/timeline/compositing dan render, *bukan* pengganti wajib Bang Motion atau jaminan visual lebih baik. GSAP/HTML/SVG/Three.js/Blender dan asset footage merupakan pilihan berdasarkan kebutuhan shot, runtime dan lisensi.

**Owner prioritization (06 Nov):** Kerjakan dulu **versi pribadi** agar bisa langsung dipakai sambil mempelajari kelemahan dan memperbaikinya. Use cases nyata: hook video iklan produk, product B-roll/hybrid footage, demo/visual produk digital, edukasi YouTube Shorts/long-form, serta motion info/YouTube channel pribadi. Keputusan calon produk jualan ditunda hingga prototipe personal benar-benar terbukti bagus dan workable. Owner menyebut waktu eksplorasi awal sekitar satu hari sebagai keinginan kerja intensif, **bukan janji delivery**.

**Style Book v0 versus “otak” terpisah:** Model inti sekarang cukup untuk memulai *proof-of-use* terarah setelah persetujuan owner terhadap batch kode. Tidak perlu membuat ChatGPT Project baru sekarang (Owner eksplisit: jangan dulu). Simpan style knowledge, prompt decisions, lessons, reference URLs dan hasil eksperimen dalam repo motion; Member Area repo menyimpan pointer/handover. Jangan mencoba menciptakan katalog lengkap sebelum produksi pertama. Style Book dan Visual Director akan disempurnakan secara iteratif setelah tiap contoh nyata, bukan mengunci engine ke sejumlah template.

**Urutan personal pilot yang diusulkan (belum implementasi):** (a) satu hook iklan pendek dari brief produk nyata, (b) satu hybrid B-roll/footage + motion graphic, (c) satu educational explainer untuk YouTube / scene karakter atau diagram; pilih format dan audio sesuai masing-masing brief. Setiap pilot mencatat tujuan, style bible per-video, daftar shot/teknik level, komponen yang dipakai, hasil MP4, revisi, visual QA, waktu dan penggunaan biaya. Jangan menghabiskan semua waktu untuk banyak scene sebelum menyelesaikan satu output end-to-end.

**Existing owner approval gate:** Tahap C code implementation, dependency installation, API berbayar dan publikasi produk tetap menunggu persetujuan spesifik. Dokumentasi saja diizinkan untuk mencegah kehilangan konteks.

## 7B. Owner memilih pilot pertama: IKLAN PRODUK DIGITAL via ChatGPT Work (06 Nov)

**Perubahan urutan terpilih:** pilot personal pertama adalah **video iklan untuk produk digital milik Owner secara utuh**, bukan hook terisolasi. Setelah video utuh terbukti usable baru eksplorasi hook tersendiri, B-roll dan YouTube. Product name/fitur/benefit/offer/CTA dan footage yang akan digunakan belum dipilih atau diserahkan dalam turn ini; jangan mengarang klaim atau aset.

**Target durasi untuk pilot ini:** kira-kira **30–40 detik**, fleksibel lebih pendek/panjang jika kebutuhan storytelling dan demonstrasi produk mengharuskan; 60 detik hanyalah alternatif yang boleh direkomendasikan dengan alasan isi/tempo, bukan default atau format wajib. Rasio, resolusi, VO dan platform mengikuti creative brief. Video iklan dirancang berisi opening hook, masalah/relevansi, pengenalan & demonstrasi manfaat produk, trust/proof hanya bila tersedia, dan CTA yang sesuai; optimalkan visual storytelling (UI demo, kinetic typography, 2D/2.5D/3D, footage/B-roll) per scene.

**Environment yang ingin diuji:** Owner berencana mulai dengan **ChatGPT Work, model GPT-6.1 Sol High** jika tersedia; tidak langsung Codex. Bandingkan Work + Astra pada effort yang sesuai, kemudian Codex hanya jika dibutuhkan; aset, brief, commit dan kriteria QA harus sama untuk evaluasi terkontrol. OpenAI menyatakan GPT-6 Astra sebagai model paling mampu untuk tugas kompleks, tetapi lebih boros allowance dan tak menjamin hasil visual lebih baik. Project instructions bekerja di ChatGPT Project untuk Work; Codex memakai instruksi repo/AGENTS.md, bukan mekanisme Project yang sama. Penggunaan Work/Codex dalam ChatGPT Project Member Area tidak mengubah status Orma Motion sebagai repo independen.

**Status:** Trial belum dijalankan dan produk digital spesifik belum disebut. Ini keputusan prioritas/creative pilot, B Stage planning tetap aktif. Jangan menambahkan Project ChatGPT baru atau menjalankan paid API/implementasi engine tanpa izin pekerjaan yang sesuai.

## 8. NEXT untuk chat pengembangan berikutnya

1. Baca dokumen ini dan canonical coordination handoff pada repo member-area, lalu periksa HEAD main terbaru dan perubahan aktual sebelum memulai.
2. Lanjutkan diskusi Tahap B, bukan langsung implementasi: inventaris referensi, kelompokkan bahasa visual, definisikan Style Book minimal dan kriteria 2D vs 3D vs footage.
3. Tentukan benchmark representatif tanpa mematok durasi/rasio/VO secara universal; hindari overpromising full automation.
4. Audit dependency & lisensi third-party sebelum mengadopsi code Cartoon Short Kit / referensi lain.
5. Minta/ikuti ACC rancangan Tahap B sebelum implementasi C, paid ElevenLabs, merge engine, atau deploy. Dokumentasikan keputusan final sesudah ACC.
6. Saat handover, update progress nyata di kedua repo masing-masing sesuai perannya; jangan sinkron otomatis tanpa tindakan eksplisit.

**Verifikasi dokumen:** dokumentasi ini menyatakan progres diskusi dan source inspection, bukan implementasi atau pengujian video end-to-end.