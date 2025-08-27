# Prompt Templates — Koleksi Template Prompt JSON

##Deskripsi singkat
-----------------
Repositori ini berisi kumpulan template prompt berbasis JSON yang dirancang untuk menghasilkan keluaran AI terstruktur (hanya JSON). Template ditujukan untuk memudahkan integrasi dengan pipeline otomatis, validasi JSON Schema, dan pengujian A/B. Template cocok dipakai untuk ekstraksi data, ringkasan, QA dengan bukti, generasi kode proyek, percakapan santai, dan contoh payload API.

##Isi utama
---------
- extractor_template.json — ekstraksi kontak / form
- compute_template.json — perintah komputasi sederhana
- summary_template.json — ringkasan artikel menjadi 5 poin terstruktur
- qa_template.json — tanya-jawab dengan array bukti (evidence)
- codegen_template.json — buat beberapa file proyek (struktur JSON)
- casual_chat_template.json — percakapan santai; reply terstruktur
- api_payload_example.json — contoh payload messages untuk dipakai langsung ke endpoint chat
- contact_schema.json, summary_schema.json, qa_schema.json, codegen_schema.json, casual_chat_schema.json — JSON Schema untuk validasi

##Tujuan penggunaan
-----------------
- Memaksa model membalas hanya dengan JSON yang valid sesuai skema.
- Mempermudah parsing dan integrasi hasil AI ke sistem backend.
- Menyediakan contoh payload siap pakai untuk API Chat (sesuaikan model & setting).

##Panduan singkat (Quick start)
-----------------------------
1. Pilih template yang sesuai (mis. extractor_template.json).
2. Sesuaikan nilai placeholder di field `user` seperti <TEKS_INPUT> atau <DESKRIPSI_PROYEK>.
3. Kirimkan payload `messages` ke endpoint chat dengan:
   - system message yang tegas: "RESPOND ONLY WITH JSON. NOTHING ELSE." (atau versi bahasa Indonesia).
   - temperature: 0.0–0.2 untuk keluaran deterministik.
   - max_tokens disesuaikan dengan ukuran output yang diharapkan.
4. Validasi response dengan JSON Schema yang sesuai (ajv untuk Node.js, jsonschema untuk Python, dsb).
5. Jika model menyertakan teks non-JSON, tambahkan contoh output valid (few-shot) di user message atau perketat system message.

Contoh panggilan API (sesuaikan model & endpoint)
```json
{
  "model": "gpt-5-mini",
  "temperature": 0.0,
  "max_tokens": 300,
  "messages": [
    {
      "role": "system",
      "content": "You are an assistant that MUST ONLY RESPOND with valid JSON matching the schema given. If unsure, set values to null. Do not output any extra text."
    },
    {
      "role": "user",
      "content": "Skema: {\"name\":\"string|null\",\"email\":\"string|null\",\"phone\":\"string|null\",\"company\":\"string|null\",\"notes\":\"string|null\"}\nTeks: \"Halo, saya Andi dari PT Contoh. Email: andi@contoh.com\"\nKeluarkan hanya JSON sesuai skema."
    }
  ]
}
```

Contoh minimal (extractor)
```json
Input text:
"Halo, saya Rina dari PT Alfa. Email: rina@alfa.co, Telepon: +628123456."

Expected JSON:
{
  "name": "Rina",
  "email": "rina@alfa.co",
  "phone": "+628123456",
  "company": "PT Alfa",
  "notes": null
}
```

##Validasi & testing
------------------
- Gunakan validator JSON Schema di sisi client (ajv, jsonschema, dsf.).
- Jalankan batch test (50–200 sampel) untuk mengukur:
  - Persentase response yang valid JSON.
  - Ketepatan entitas (precision/recall) terhadap dataset ground truth.
- Jika hasil sering mengandung teks tambahan, tambahkan few-shot examples atau perketat system message.

##Tips praktis
-----------
- Gunakan temperature = 0.0 untuk determinisme; naikkan sedikit (0.2–0.4) untuk nada santai di casual_chat.
- Minta model untuk mengisi nilai yang tidak diketahui dengan `null`.
- Sertakan `max_tokens` cukup besar untuk output besar (mis. codegen).
- Simpan schema dan contoh expected output bersama template agar tim QA dapat menjalankan validasi otomatis.

##Kontribusi
----------
Silakan buat PR yang menambahkan template baru, contoh input/expected output, atau suite test. Beri nama file yang jelas dan sertakan JSON Schema bila relevan.

##Lisensi
-------
MIT — bebas dipakai dan dimodifikasi.

Kontak
------
Jika perlu penyesuaian template (mis. invoice parsing, resume parsing, review produk), buat issue atau kirim PR dengan contoh input dan skema target.
