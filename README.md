# Black Mamba Asia — Claude Plugins

Kumpulan plugin Claude Code dari [Black Mamba Asia](https://black.mamba.asia).

## Plugins

| Plugin | Versi | Deskripsi |
|--------|-------|-----------|
| [buatkan](./buatkan) | 1.0.0 | Otomatisasi dokumentasi project (changelog, dll) |

## Instalasi

### Per-project (direkomendasikan untuk tim)

Clone repo ini, lalu tambahkan plugin yang diinginkan ke `.claude/settings.json` project kamu:

```bash
git clone https://github.com/black-mamba-asia/claude-plugins
```

```json
{
  "plugins": ["./claude-plugins/buatkan"]
}
```

Commit `settings.json` ke git agar plugin aktif otomatis untuk seluruh tim. Tambahkan ke `.gitignore`:

```
.claude/settings.local.json
```

### Global (semua project)

```bash
claude plugin add ./buatkan
```

---

## Daftar Plugin

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
