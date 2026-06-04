# Black Mamba Asia — Claude Plugins

Kumpulan plugin Claude Code dari [Black Mamba Asia](https://black.mamba.asia).

## Plugins

| Plugin | Versi | Deskripsi |
|--------|-------|-----------|
| [sp-estimate](./spestimate) | 1.0.0 | Estimasi Story Point dari PRD atau deskripsi task |
| [buatkan](./buatkan) | 1.0.0 | Otomatisasi dokumentasi project (changelog, dll) |

## Instalasi Cepat

### sp-estimate

```bash
# Install global (langsung dari GitHub)
claude plugin add github:black-mamba-asia/claude-plugins/spestimate

# Atau install ke project tertentu
claude plugin add github:black-mamba-asia/claude-plugins/spestimate --project
```

### buatkan

```bash
claude plugin add github:black-mamba-asia/claude-plugins/buatkan
```

### Untuk tim (via settings.json)

Clone repo ini sekali, lalu daftarkan plugin ke `.claude/settings.json` project:

```bash
git clone https://github.com/black-mamba-asia/claude-plugins
```

```json
{
  "plugins": [
    "./claude-plugins/spestimate",
    "./claude-plugins/buatkan"
  ]
}
```

Commit `settings.json` agar aktif otomatis untuk seluruh tim. Tambahkan ke `.gitignore`:

```
.claude/settings.local.json
```

---

## Daftar Plugin

### sp-estimate

Estimasi Story Point dari task description, user story, atau PRD — menghasilkan 3 perspektif (jam tim, SP industri, estimasi AI).

| Skill | Command | Kegunaan |
|-------|---------|----------|
| sp-estimate | `/sp-estimate <deskripsi>` | Estimasi SP dari deskripsi task atau PRD |

Lihat [spestimate/README.md](./spestimate/README.md) untuk detail penggunaan.

---

### buatkan

Skills untuk otomatisasi pembuatan dokumentasi developer.

| Skill | Command | Kegunaan |
|-------|---------|----------|
| changelog | `/buatkan:changelog <deskripsi>` | Generate changelog entry berformat Keep a Changelog |

Lihat [buatkan/README.md](./buatkan/README.md) untuk detail penggunaan.

---

## Kontribusi

Plugin baru bisa ditambahkan sebagai subfolder di repo ini. Setiap plugin wajib memiliki:

```
nama-plugin/
├── .claude-plugin/
│   └── plugin.json     # Manifest (name, version, author, dll)
├── skills/
│   └── nama-skill/
│       └── SKILL.md    # Instruksi skill untuk Claude
└── README.md
```

Daftarkan plugin baru ke [`.claude-plugin/marketplace.json`](./.claude-plugin/marketplace.json).
