# Koleksi Template Prompt — Search & Task Templates

Deskripsi
--------
Repo ini berisi kumpulan template prompt berbasis JSON yang sering dipakai untuk:
- Pencarian (web / code / semantic)
- Tugas operasional (to-do, meeting notes, action items)
- Komunikasi (email, bug/feature reports)
- Pengembangan (code review, unit tests, SQL generation, codegen)
- Ekstraksi & parsing (invoice, resume, forms)
- Konten (summarization, translation, QA)
- Percakapan santai (casual chat)

Tujuan
------
Memudahkan integrasi AI ke workflow sehingga assistant menghasilkan output terstruktur (JSON) yang mudah divalidasi dan diproses otomatis.

Panduan singkat (Quick start)
----------------------------
1. Pilih template JSON yang sesuai dari folder atau daftar.
2. Ganti placeholder di field `user` seperti <INPUT_TEXT> atau <DESCRIPTION>.
3. Kirim payload `messages` ke API chat:
   - Sertakan `system` message yang memaksa format: "RESPOND ONLY WITH VALID JSON. NOTHING ELSE."
   - Atur temperature sesuai settings di template (0.0–0.2 untuk deterministik; 0.3–0.6 untuk nada santai).
4. Validasi response dengan JSON Schema yang disertakan (ajv, jsonschema, dsb).
5. Jika model menyertakan teks selain JSON, tambahkan contoh few-shot di `user` atau perketat system message.

File penting
-----------
- README.md — penjelasan & quickstart
- index_templates.json — daftar semua template
- *.json — masing-masing template dan schema

Validasi & testing
------------------
- Jalankan validator JSON Schema pada setiap response.
- Lakukan batch test (50–200 sampel) untuk mengukur valid JSON rate dan akurasi entitas.
- Untuk A/B testing, bandingkan dua model/setting pada sample prompt identik.

Kontribusi
----------
Tambahkan template baru, contoh input/output, atau suite test lewat PR. Sertakan JSON Schema jika memungkinkan.

Lisensi
-------
MIT