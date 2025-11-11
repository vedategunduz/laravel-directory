# 📁 Laravel Modüler Klasör Yapısı Açıklaması

Bu doküman, Laravel projelerinde kullanılan modüler klasör yapısının amacını ve her klasörün sorumluluğunu açıklar. Bu yapı, büyük ölçekli projelerde kodun okunabilirliğini, sürdürülebilirliğini ve test edilebilirliğini artırmak için kullanılır.

---

## 📂 Http/Controllers/Blog

-   **Amaç:** HTTP isteklerini karşılayan controller sınıfları.
-   **Görev:** Request alır, servisleri çağırır, response döner.
-   **Örnek:** `BlogController`, `PostController`

---

## 📂 Http/Requests/Blog

-   **Amaç:** Form doğrulama ve yetkilendirme kurallarını içerir.
-   **Görev:** Gelen veriyi doğrular, controller'a temiz veri sağlar.
-   **Örnek:** `StoreBlogRequest`, `UpdatePostRequest`

---

## 📂 Http/Resources/Blog

-   **Amaç:** API response'larını biçimlendirmek için kullanılır.
-   **Görev:** Model verisini JSON formatına dönüştürür.
-   **Örnek:** `BlogResource`, `PostResource`

---

## 📂 Services/Blog

-   **Amaç:** İş mantığını içerir.
-   **Görev:** Controller'dan gelen çağrıları işler, repository ile konuşur.
-   **Örnek:** `BlogService`, `PostService`

---

## 📂 Repositories/Blog

-   **Amaç:** Veritabanı işlemlerini soyutlar.
-   **Görev:** Model sorgularını içerir, servis katmanına veri sağlar.
-   **Örnek:** `BlogRepository`, `PostRepository`

---

## 📂 DTOs/Blog

-   **Amaç:** Veri taşıma nesneleri (Data Transfer Object).
-   **Görev:** Servisler arası veri aktarımı için kullanılır.
-   **Örnek:** `BlogDTO`, `PostDTO`

---

## 📂 Models/

-   **Amaç:** Veritabanı tablolarını temsil eder.
-   **Görev:** ORM (Eloquent) ile veri işlemleri yapılır.
-   **Örnek:** `Blog`, `Post`, `Comment`

---

## 📂 Policies/

-   **Amaç:** Yetkilendirme kurallarını içerir.
-   **Görev:** Kullanıcının bir işlemi yapmaya yetkisi olup olmadığını kontrol eder.
-   **Örnek:** `BlogPolicy`, `PostPolicy`

---

## 📂 Observers/

-   **Amaç:** Model olaylarını dinler (create, update, delete).
-   **Görev:** Otomatik işlemler tetiklenebilir (örneğin loglama, bildirim).
-   **Örnek:** `BlogObserver`, `PostObserver`

---

## 📂 Events/

-   **Amaç:** Uygulama içi olayları temsil eder.
-   **Görev:** Listener'lar tarafından dinlenir, sistemde reaksiyon tetikler.
-   **Örnek:** `BlogPublished`, `PostLiked`

---

## 📂 Listeners/

-   **Amaç:** Event'lere verilen tepkileri içerir.
-   **Görev:** Event tetiklendiğinde çalışacak işlemleri tanımlar.
-   **Örnek:** `SendBlogNotification`, `NotifyAuthor`

---

## 📂 Jobs/

-   **Amaç:** Kuyruk sisteminde çalışacak görevler.
-   **Görev:** Zaman alan işlemleri asenkron olarak çalıştırır.
-   **Örnek:** `PublishBlogJob`, `SendEmailJob`

---

## ✅ Notlar

-   `Controllers`, `Requests`, `Resources`, `Models`, `Policies`, `Observers`, `Events`, `Listeners`, `Jobs` klasörleri için Artisan komutları mevcuttur.
-   `Services`, `Repositories`, `DTOs` klasörleri elle oluşturulmalı veya özel Artisan komutları tanımlanmalıdır.

---

Bu yapı, Laravel projelerinde **temiz kod**, **modülerlik** ve **uzun vadeli sürdürülebilirlik** sağlar.
