---
name: sprint-report
description: Generate sprint report berdasarkan data sprint yang tersedia.
---

# Sprint Report — Generator

Generate laporan sprint berdasarkan data sprint yang tersedia.

## Cara pakai

```
/sprint-report <list story, link csv, atau data sprint lainnya>
```

Atau tanpa argumen → Claude akan meminta deskripsi task.

---

## Instructions

Deteksi jenis input secara otomatis dan pilih mode yang sesuai:

---

### MODE 1 — CSV / List Task → HTML Links

Aktif jika input mengandung CSV (dengan kolom `Issue key` dan `Summary`) atau list task dengan format `[KEY] Judul`.

#### Input yang diterima
- CSV Jira (kolom minimal: `Issue key`, `Summary`)
- List task dengan format `ESO-XXXXX Judul task`
- Teks bebas yang mengandung issue key pola `[A-Z]+-\d+`

#### Output Format WAJIB

Satu baris HTML, tanpa newline, tanpa spasi antar elemen:

```
<a href=https://esb-id.atlassian.net/browse/ESO-XXXXX>[ESO-XXXXX]</a>Judul task<br/><a href=...
```

Aturan:
- Base URL: `https://esb-id.atlassian.net/browse/`
- Format per item: `<a href=https://esb-id.atlassian.net/browse/{KEY}>[{KEY}]</a>{Summary}<br/>`
- Seluruh output **1 baris**, tidak ada `\n`, tidak ada spasi ekstra
- Tidak ada wrapper, tidak ada markdown, tidak ada penjelasan — hanya HTML mentah
- Sertakan semua baris dari input (tidak filter berdasarkan status)

---

### MODE 2 — Story Point Estimator

Aktif jika input adalah deskripsi task, PRD, user story, atau feature request (bukan CSV/list issue key).

#### Input yang diterima
- Deskripsi task singkat
- User story / acceptance criteria
- PRD (Product Requirements Document)
- Action items dari tech spec
- Feature request

#### Output Format WAJIB

Untuk setiap task/fitur yang teridentifikasi, output-kan tabel berikut:

---

#### Breakdown Task

| # | Task | Komponen | Dev Standard (jam) | Industri Umum (SP) | AI Estimate |
|---|---|---|---|---|---|
| 1 | [nama task] | [FE/BE/API/DB] | [X jam] | [X SP] | [X menit/jam] |
| ... | | | | | |
| | **Testing** | | [15-25% dari total] | [20-30%] | [manual review] |
| | **TOTAL** | | **[X jam]** | **[X SP]** | **[X jam]** |

---
