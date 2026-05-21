# buatkan Plugin

Plugin Claude Code untuk otomatisasi changelog project.

## Skills

| Command | Kegunaan |
|---|---|
| `/go-docs:godoc <file>` | Generate godoc comments untuk exported symbols yang belum terdokumentasi |
| `/go-docs:changelog <deskripsi>` | Generate changelog entry berformat Keep a Changelog |
| `/go-docs:pr-summary <deskripsi>` | Generate PR description yang informatif |

## Instalasi

### Option 1: Install ke project (direkomendasikan untuk tim)

```bash
# Taruh folder go-docs di dalam repository kamu, lalu:
claude plugin add ./go-docs --project
```

Tambahkan ke `.claude/settings.json` agar otomatis aktif untuk semua anggota tim:

```json
{
  "plugins": ["./go-docs"]
}
```

Commit `.claude/settings.json` ke git, dan tambahkan ini ke `.gitignore`:

```
.claude/settings.local.json
```

### Option 2: Install global (untuk semua project)

```bash
claude plugin add ./go-docs
```

## Contoh Penggunaan

```bash
# Generate godoc untuk satu file
/go-docs:godoc internal/user/service.go

# Generate godoc untuk beberapa file sekaligus
/go-docs:godoc internal/user/service.go internal/user/repository.go

# Buat changelog entry setelah selesai fitur
/go-docs:changelog "tambah endpoint reset password dengan rate limiting 5 req/menit"

# Buat changelog dari git log
/go-docs:changelog $(git log --oneline main..HEAD)

# Buat PR description dari deskripsi singkat
/go-docs:pr-summary "refactor database layer untuk support multi-tenant dengan row-level security"

# Buat PR description dari nama branch
/go-docs:pr-summary feat/add-user-authentication
```

## Struktur Plugin

```
go-docs/
├── .claude-plugin/
│   └── plugin.json          # Manifest plugin
├── skills/
│   ├── godoc/
│   │   └── SKILL.md         # Generate godoc comments
│   ├── changelog/
│   │   └── SKILL.md         # Generate changelog entries
│   └── pr-summary/
│       └── SKILL.md         # Generate PR descriptions
└── README.md
```

## Tips

- Untuk `godoc`: berikan path file lengkap agar hasilnya lebih akurat
- Untuk `changelog`: semakin detail deskripsi input, semakin baik hasilnya. Bisa juga paste output `git log --oneline`
- Untuk `pr-summary`: bisa digabung dengan output `git diff --stat` untuk hasil yang lebih lengkap

## Pengembangan

Untuk modifikasi skill, edit file `SKILL.md` di folder skill yang bersangkutan, lalu jalankan `/reload-plugins` di dalam sesi Claude Code.
