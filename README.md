# LAPORAN MODUL 1 — Persiapan Tool Development

---

## Identitas

| Item | Keterangan |
|------|------------|
| Mata Kuliah | Pemrograman Web Lanjut |
| Modul | 1 |
| Framework | Laravel 13 |
| Starter Kit | Livewire 4 |
| Database | MariaDB |
| Cache/Session/Queue | Redis |
| WebSocket | Reverb |
| Tanggal | 30 Agustus 2026 |
| Status | ✅ Selesai |

---

## Tools

- PHP 8.4.24 (ServeBay)
- Composer
- Node.js & NPM
- Git
- MariaDB 10.11
- Redis 7.0

---

## Langkah Pengerjaan

| Tahap | Kegiatan | Perintah |
|-------|----------|----------|
| 1 | Persiapan | `mkdir project-kantin && cd project-kantin` |
| 2 | Buat proyek | `composer create-project laravel/laravel kantin-multi-tenant` |
| 3 | Install Breeze + Livewire | `composer require laravel/breeze --dev && php artisan breeze:install livewire` |
| 4 | Install dependency | `npm install && npm run build` |
| 5 | Setup database | Buat DB `dummy`, isi `.env`, `php artisan migrate:fresh --seed` |
| 6 | Install Reverb | `php artisan install:broadcasting` (pilih reverb) |
| 7 | Quality Gate | `php artisan test`, `vendor\bin\pint`, `npm run build` |
| 8 | Commit & Push | `git add . && git commit -m "chore(setup)" && git push` |

---

## Kendala & Solusi

| No | Kendala | Solusi |
|----|---------|--------|
| 1 | Duplikasi `BROADCAST_CONNECTION` di .env | Hapus salah satu, isi REVERB_* |
| 2 | `Redis::connection()` undefined | Pakai `Redis::ping()` |
| 3 | Dependency conflict Reverb | `composer require laravel/reverb --with-all-dependencies` |
| 4 | Pint formatting error | `vendor\bin\pint` |
| 5 | `redis-cli` not found | Test via `php artisan queue:work --once` |
| 6 | Pusher auth_key null | Isi REVERB_APP_ID, KEY, SECRET |

---

## Hasil Verifikasi

| Perintah | Hasil |
|----------|-------|
| `php artisan --version` | Laravel Framework 13.25.0 ✅ |
| `php artisan db:show` | Connected to dummy ✅ |
| `php artisan test` | 26 passed (77 assertions) ✅ |
| `npm run build` | Build successful ✅ |
| `vendor\bin\pint --test` | All files formatted ✅ |
| `git status` | .env tidak muncul ✅ |

---

## Running Services

```bash
php artisan serve          # Terminal 1 (HTTP)
npm run dev                # Terminal 2 (Vite)
php artisan reverb:start   # Terminal 3 (WebSocket)
php artisan queue:work     # Terminal 4 (Queue)