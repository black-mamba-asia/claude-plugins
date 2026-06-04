# sp-estimate

Plugin Claude Code untuk estimasi Story Point dari PRD atau deskripsi task, berdasarkan standar tim ESB/ESO.

## Skills

| Command | Kegunaan |
|---|---|
| `/sp-estimate <deskripsi>` | Estimasi SP dari deskripsi task, user story, atau PRD |

## Instalasi

### Option 1: Install ke project (direkomendasikan untuk tim)

```bash
claude plugin add ./sp-estimate --project
```

Tambahkan ke `.claude/settings.json` agar otomatis aktif untuk semua anggota tim:

```json
{
  "plugins": ["./sp-estimate"]
}
```

Commit `.claude/settings.json` ke git, dan tambahkan ini ke `.gitignore`:

```
.claude/settings.local.json
```

### Option 2: Install global (untuk semua project)

```bash
claude plugin add ./sp-estimate
```

## Contoh Penggunaan

```bash
# Dari deskripsi singkat
/sp-estimate tambah endpoint reset password dengan rate limiting

# Dari user story
/sp-estimate As a user, I want to see my transaction history filtered by date range

# Paste PRD langsung
/sp-estimate <paste isi PRD>

# Tanpa argumen — Claude akan menanyakan deskripsi task
/sp-estimate
```

## Output yang Dihasilkan

Setiap estimasi menghasilkan 3 perspektif:

1. **Standar Developer Tim (ESB/ESO)** — dalam jam, dengan skala XS/S/M/L/XL/XXL
2. **Standar Industri** — Fibonacci SP (1/2/3/5/8/13), setara sprint capacity 40 SP/2 minggu
3. **Estimasi AI** — waktu jika dikerjakan dengan AI assist, beserta faktor reduksinya

Lengkap dengan breakdown per task, analisa kompleksitas, dan confidence level.

## Struktur Plugin

```
sp-estimate/
├── .claude-plugin/
│   └── plugin.json          # Manifest plugin
├── skills/
│   └── sp-estimate/
│       └── SKILL.md         # Instruksi estimasi SP
└── README.md
```

## Pengembangan

Untuk modifikasi referensi SP atau skala tim, edit file `skills/sp-estimate/SKILL.md`, lalu jalankan `/reload-plugins` di dalam sesi Claude Code.
