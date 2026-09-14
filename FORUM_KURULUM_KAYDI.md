# MyBB Forum Kurulum Kaydı

**Tarih:** 2026-09-14
**Durum:** Kurulum tamamlandı ve çalışıyor

## Kurulum Bilgileri

| Konu | Değer |
|---|---|
| Forum | MyBB 1.8.40 (git tag `mybb_1840`, commit `bd2a34479`) |
| Kaynak repo | `mybb/mybb` (resmi repo) |
| Web kökü | `/var/www/mybb` |
| Web sunucusu | Apache2 (port 12000) |
| PHP | 8.4.24 |
| Veritabanı | MariaDB 11.8.6 |
| DB adı / kullanıcı | `mybb` / `mybb`@localhost+127.0.0.1 |
| DB şifre | `mybb_password` |
| Forum adresi | https://work-1-duppgirybejoyhmt.prod-runtime.all-hands.dev/ |
| Admin paneli | https://work-1-duppgirybejoyhmt.prod-runtime.all-hands.dev/admin/ |
| Yönetici kullanıcı | `admin` / `Admin1234!` |
| Forum adı | "Benim Forumum" |

## Kurulum Adımları

1. `mybb/mybb` reposundan MyBB 1.8.40 klonlandı (`/workspace/project`)
2. Apache2 + PHP 8.4 + MariaDB kuruldu ve servisler başlatıldı
3. `mybb` veritabanı ve kullanıcı oluşturuldu
4. MyBB dosyaları `/var/www/mybb` altına kopyalandı (sahibi `www-data`)
5. Apache vhost port 12000 yapılandırıldı
6. Kurulum sihirbazı tamamlandı (tablolar, tema, ayarlar, admin hesabı)
7. Güvenlik: `/var/www/mybb/install` klasörü silindi
8. Forumun kamusal URL'den çalıştığı doğrulandı (HTTP 200)

## Test İçerikleri (2026-09-14)

Açılan 5 deneme kategorisi ve her birinde 10 konu:

| Kategori (kök) | Forum (alt) | Konu sayısı |
|---|---|---|
| Deneme Kategori 1 | Deneme Kategori 1 Forum | 10 |
| Deneme Kategori 2 | Deneme Kategori 2 Forum | 10 |
| Deneme Kategori 3 | Deneme Kategori 3 Forum | 10 |
| Deneme Kategori 4 | Deneme Kategori 4 Forum | 10 |
| Deneme Kategori 5 | Deneme Kategori 5 Forum | 10 |
| **Toplam** | | **50 konu** |

- Forum yapısı DB'de: kayıtlar `forums` tablosunda `fid` 3-12 (kategori `type='c'`, forum `type='f'`)
- Konular MyBB `PostDataHandler->insert_thread()` API'siyle eklendi; forum sayaçları otomatik güncellendi
- Cache'ler tazelendi (`update_forums`, `update_stats`); geçici betikler temizlendi

## Bilinen Durumlar / Notlar

- `/var/www/mybb` altında `.git` klasörü var (kurulum için klonlanmıştı) — web kökünde durması güvenlik açısından istenmezse kaldırılmalı
- `/var/www/mybb/inc/settings.php` kurulum sonrası oluşuyor (boş değil, normal)
- İkinci port (12001) vhost'u kullanıcı isteğiyle geri alındı; sadece 12000 aktif
- "Promosyonlarım → Etkinliklerim" görevi iptal edildi, değişiklik yapılmadı

## Önerilen Sıradaki Adımlar

- Türkçe dil paketi kurulumu
- Tema özelleştirme
- Admin şifresi değişikliği (isterken)
- Test kategorilerinin/konularının silinmesi
- `.git` klasörünün web kökünden kaldırılması (güvenlik)