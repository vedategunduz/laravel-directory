# 🧩 Laravel Blog Modülü Senaryosu

Bu senaryo, Laravel'de modüler klasör yapısını kullanarak geliştirilen bir **Blog platformunun** işleyişini ve mimarisini örneklemektedir. Amaç, her klasörün nasıl bir sorumluluğa sahip olduğunu gerçek bir kullanım üzerinden göstermektir.

---

## 🎯 Senaryo: “Yazarlar İçin Blog Platformu”

Kullanıcılar blog yazıları oluşturabilir, düzenleyebilir ve diğer kullanıcılar bu yazıları okuyabilir. Her yazının bir yazarı, başlığı, içeriği ve yayın durumu (taslak/yayınlandı) vardır.

---

## 🧱 Modüler Yapının Kullanımı

### 1. Kullanıcı yeni bir blog yazısı oluşturur

-   `BlogController@store` → HTTP isteği alınır.
-   `StoreBlogRequest` → Gelen veri doğrulanır.
-   `BlogDTO` → Request verisi DTO’ya dönüştürülür.
-   `BlogService@create` → İş mantığı uygulanır.
-   `BlogRepository@create` → Veritabanına kayıt yapılır.
-   `BlogObserver@created` → Loglama veya otomatik etiketleme yapılır.
-   `BlogPublished` event’i tetiklenir.
-   `SendBlogNotification` listener’ı admin’e e-posta gönderir.
-   `BlogResource` → JSON response olarak döner.

---

### 2. Kullanıcı kendi yazısını günceller

-   `BlogPolicy@update` → Yetki kontrolü yapılır.
-   `UpdateBlogRequest` → Yeni içerik doğrulanır.
-   `BlogService@update` → Güncelleme işlemi yapılır.

---

### 3. Yönetici tüm yazıları listeler

-   `BlogController@index` → Tüm yazılar çekilir.
-   `BlogService@getAll` → Servis üzerinden veri alınır.
-   `BlogRepository@allWithAuthors` → Yazar bilgileriyle birlikte veri çekilir.
-   `BlogResource::collection` → JSON olarak döner.

---

### 4. Yayınlanan yazılar için kuyrukta işlem yapılır

-   `PublishBlogJob` → Kuyruğa alınır.
-   `BlogPublished` event’i tetiklenir.

---

### 5. Yazı silindiğinde log tutulur

-   `BlogObserver@deleted` → Silinen yazı bilgisi loglanır.

---

## 🧠 Ek Özellikler

| Özellik               | Kullanılan Yapı             |
| --------------------- | --------------------------- |
| Yazar yetkilendirmesi | `BlogPolicy`                |
| Otomatik bildirim     | `Events` + `Listeners`      |
| Kuyruklu yayınlama    | `Jobs`                      |
| JSON API çıktısı      | `Resources`                 |
| Temiz veri taşıma     | `DTOs`                      |
| Servis/repo ayrımı    | `Services` + `Repositories` |
| Model olayları        | `Observers`                 |

---

## 🧪 Test Edilebilirlik

-   `BlogService` için unit test yazılabilir.
-   `BlogController` için feature test uygulanabilir.
-   `BlogPolicy` ile yetkilendirme testleri yapılabilir.
-   Event ve Listener’lar için integration testler geliştirilebilir.

---

## 📌 Notlar

Bu senaryo, Laravel'de modüler mimarinin nasıl uçtan uca kullanılabileceğini gösterir. Her klasör, tek bir sorumluluğa sahiptir ve sistemin sürdürülebilirliğini artırır.
