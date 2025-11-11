# Vedat’ın Kod Standartları – Profesyonel Yazılım Geliştirme Rehberi (v1.0.0)

**Yazar:** Vedat
**Not:** Bu rehber profesyonel ölçekli Laravel projeleri için mimari ve isimlendirme standartlarını tanımlar.

---

## Bölüm 1 – Genel Yazım Kuralları
- Kod önce **okunabilir** olmalı; hız veya kısalık ikinci planda.
- İngilizce isimlendirme zorunlu. Türkçe isimlendirme yasak.
- Satırlar mümkünse 120 karakteri geçmemelidir.
- Bir fonksiyon tek iş yapmalıdır (Single Responsibility).
- Girinti (indentation): 4 space.
- Magic string ve magic number yasaktır. Sabitler constant’ta tutulur.
- Gereksiz yorum satırı yok; anlam açıklayan gerektiğinde var.

## Bölüm 2 – Değişken İsimlendirme
- Format: `camelCase`
- Tekil / çoğul ayrımı doğru kullanılmalı. Ör: `$user`, `$users`, `$userList`
- Boolean değişkenler `is`, `has`, `can`, `should` ile başlamalı.
- Tarih değişkenleri: `startedAt`, `finishedAt`
- ID kullanımı:
  - Kodda: `$userId`
  - JSON: `userId`
  - DB: `user_id`
- Yasak isimler: `$data`, `$res`, `$temp`, `$arr`, `$veri`

## Bölüm 3 – Fonksiyon / Metot Standartları
- Format: `camelCase`
- Fonksiyonlar **fiil** ile başlamalı.
- Fonksiyon ismi ne yaptığını tek cümlede anlatmalı.
- REST sabitleri controller’da: `index`, `show`, `store`, `update`, `destroy`
- Boolean dönen fonksiyonlar: `isUserActive()`, `hasRole()`, `canDelete()`

## Bölüm 4 – Class, Model, Trait, Enum, Interface
- Format: **PascalCase**
- Model isimleri tekil: `User`, `Company`, `Meeting`
- Controller isimleri: `UserAccountController`
- Trait isimleri: `LogsActivityTrait`
- Enum isimleri: `UserStatusEnum`
- Interface isimleri: `AuthenticatableInterface`

## Bölüm 5 – Laravel Mimarisi

**Standart akış:**
`Controller → Request → Policy → Service → Repository → Model`
(opsiyonel: `Event/Job`)

### 5.1 Route Standartları
- Modüler routes: `routes/modules/*.php`
- Route name: dot notation → `company.users.index`
- Prefix + name: `Route::prefix('users')->name('users.')`

### 5.2 Controller Standardı
- Controller **iş mantığı içermez**.
- Sadece yönlendirir, service çağırır.

### 5.3 Request & Validation
- Controller içinde `validate()` **yasak**.
- Her işlem **Form Request** ile yapılır.

### 5.4 Migration & DB Standartları
- Tablo isimleri: çoğul `snake_case` → `users`, `company_users`
- Pivot tablo: `role_user` (2 tablo → tekil, alfabetik)
- Varsayılan kolonlar: `timestamps()` + `softDeletes()`

### 5.5 Model & Relation
- `belongsTo` → `user()` (tekil)
- `hasMany` → `users()` (çoğul)
- `belongsToMany` → `roles()` (çoğul)
- `$fillable` zorunlu, `$guarded` yasak

### 5.6 Resource / JSON Standardı
- JSON key → `camelCase`
- Resource veya Resource Collection zorunlu

### 5.7 Policy Standardı
- Yetki if ile yazılmaz → `authorize()` veya `can()` kullanılır

### 5.8 Observer
- Model event yan etkileri Observer’da yönetilir

### 5.9 Event & Listener
- Event → geçmiş zaman (`UserApproved`)
- Listener → fiil tabanlı (`SendUserApprovedMail`)
- Listener’lar queued çalışmalıdır

### 5.10 Job & Queue
- Ağır işler job → queue
- Retry, timeout, backoff tanımlanmalı

### 5.11 Mail & Notification
- Mail asla controller’dan gönderilmez
- Akış: `Service → Job → Mail/Notification`

### 5.12 Exception Handling
- Service `throw` eder → Handler JSON format döner
- `try-catch` yalnızca dış servis durumlarında

---

## Bölüm 6 – Blade & Frontend
- Blade yalnızca **presentation** katmanıdır
- Alpine küçük UI etkileşimlerinde kullanılabilir
- Tailwind utility-first
- View dosyaları modüler dizilmelidir
- Blade’de sorgu ve iş mantığı yasak

---

## Bölüm 7 – Klasör & Mimari

```
app/
  Http/Controllers/Module
  Http/Requests/Module
  Http/Resources/Module
  Services/Module
  Repositories/Module
  DTOs/Module
  Policies/
  Observers/
  Events/
  Listeners/
  Jobs/
  Models/
```

---

## Bölüm 8 – Git & Commit
- Branch: `feature/user-reset-password`
- Commit: `feat: add user reset password flow`

---

## Bölüm 9 – SOLID & Clean Code
- **SRP** → Tek sorumluluk
- **KISS** → Basit tut
- **YAGNI** → Gereksiz geliştirme yapma
- **DRY** → Tekrar yok

---

## Manifesto
> “Kod çalıştığı için değil, doğru olduğu için iyidir.”

**Vedat’ın Standartları – Tüm hakları saklıdır.**
