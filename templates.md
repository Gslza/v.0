# Template Prompt JSON untuk Output Terstruktur (Contoh)

Dokumentasi singkat berisi template siap pakai untuk meminta AI mengeluarkan hanya JSON yang valid sesuai skema. Gunakan temperature 0.0–0.2 untuk determinisme. Selalu validasi hasil dengan JSON Schema di sisi client.

Cara pakai singkat:
1. Kirim system message yang memaksa format:
   - "RESPOND ONLY WITH JSON. NOTHING ELSE." (atau versi Bahasa)
2. Sertakan skema JSON eksplisit (atau JSON Schema) dalam user message.
3. Sertakan contoh (optional) untuk few-shot.
4. Gunakan temperature = 0.0 dan max_tokens sesuai kebutuhan.
5. Validasi response dengan validator (ajv, jsonschema, dsb).

Template yang tersedia di paket ini:
- extractor_template.json       : ekstraksi kontak / form
- compute_template.json         : perintah komputasi sederhana
- summary_template.json         : ringkasan artikel -> 5 poin terstruktur
- qa_template.json              : jawaban + bukti / evidence
- codegen_template.json         : generasi beberapa file proyek (format JSON)
- api_payload_example.json      : contoh payload chat API (messages array)
- contact_schema.json           : JSON Schema untuk ekstraksi kontak
- summary_schema.json           : JSON Schema untuk ringkasan
- qa_schema.json                : JSON Schema untuk QA + evidence
- codegen_schema.json           : JSON Schema untuk codegen

Contoh alur singkat:
- Kirim payload seperti di api_payload_example.json.
- Terima response (hanya JSON).
- Jalankan validator dan post-process (simpan file, jalankan build, dsb).

Catatan: Jika model masih menyisipkan teks selain JSON, ulangi system message dengan sangat tegas dan tambahkan contoh output yang valid.