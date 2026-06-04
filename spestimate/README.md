# sp-estimate

Plugin Claude Code untuk estimasi Story Point dari PRD atau deskripsi task, berdasarkan standar tim ESB/ESO.

## Instalasi

### Langsung dari GitHub (paling mudah)

```bash
# Global — aktif di semua project
claude plugin add github:black-mamba-asia/claude-plugins/spestimate

# Per-project saja
claude plugin add github:black-mamba-asia/claude-plugins/spestimate --project
```

### Untuk seluruh tim via settings.json

Clone repo sekali, lalu daftarkan di `.claude/settings.json` project:

```bash
git clone https://github.com/black-mamba-asia/claude-plugins
```

```json
{
  "plugins": ["./claude-plugins/spestimate"]
}
```

Commit `settings.json` ke git agar aktif otomatis untuk semua anggota tim. Tambahkan ke `.gitignore`:

```
.claude/settings.local.json
```

## Skills

| Command | Kegunaan |
|---|---|
| `/sp-estimate <deskripsi>` | Estimasi SP dari deskripsi task, user story, atau PRD |

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
spestimate/
├── .claude-plugin/
│   └── plugin.json          # Manifest plugin
├── skills/
│   └── sp-estimate/
│       └── SKILL.md         # Instruksi estimasi SP
└── README.md
```

## Update Plugin

```bash
claude plugin update sp-estimate
```

Atau jika install via clone:

```bash
git -C ./claude-plugins pull
```

## Modifikasi Referensi SP

Edit [skills/sp-estimate/SKILL.md](./skills/sp-estimate/SKILL.md) untuk menyesuaikan skala tim, lalu jalankan `/reload-plugins` di dalam sesi Claude Code.
