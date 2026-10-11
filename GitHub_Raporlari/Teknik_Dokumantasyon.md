# ⚙️ Teknik Dokümantasyon

Bu doküman, projede çalışan geliştiriciler için kod mimarisini, kullanılan Unity bileşenlerini ve sınıfların teknik sorumluluklarını detaylandırmaktadır.

## 📐 Mimari Genel Bakış
*   **Design Patterns (Tasarım Şablonları):** Projede global yöneticiler için (Örn: `GorevYoneticisi.cs`, `SubtitleManager.cs`) **Singleton** mimarisi kullanılmıştır. Bu sayede sahnedeki herhangi bir obje, merkez yöneticilere kolayca ulaşabilir (`GorevYoneticisi.Instance.VarilPatladi()`).
*   **Olay Güdümlü Mimari (Event-Driven):** Arayüzler ve sinematik geçişler `UnityEvent` yapıları kullanılarak esnek hale getirilmiştir (Örn: `TopcuBirligi` içerisindeki `onHucumBasla` eventi).
*   **Optimizasyon Yaklaşımı:** Çoklu AI birimleri veya mermi fiziği yerine `Physics.SphereCast` ve `OverlapSphere` kullanılarak performans artırılmış, framerate düşüşleri engellenmiştir.

## 🧩 Temel Sınıflar ve Görevleri

### 1. `KarakterHareket.cs` (Oyuncu Kontrolcüsü)
*   **Gereksinim:** `CharacterController`, `Animator`, `Health`.
*   **Detay:** Input (hem eski Input Manager hem de `#if ENABLE_INPUT_SYSTEM` ile yeni Input System destekli) okumalarını yapar. Vektörel matematik kullanarak yerçekimi ve yön vektörlerini (`transform.forward`, `transform.right`) hesaplar. Animator parametrelerini Hash ID'ler (`Animator.StringToHash`) üzerinden tetikleyerek string karşılaştırma maliyetini ortadan kaldırır (Büyük bir optimizasyon tekniğidir).

### 2. `Sword.cs` (Silah Balistiği ve Çarpışma)
*   **Detay:** Geleneksel Collider tetikleyicileri yerine `Physics.SphereCast` kullanır. Raycast'ten farklı olarak hacimli bir tarama yaptığı için, kılıç savrulmalarında kareden (frame) kaçan hitbox'ları yakalayarak kusursuz vuruş hissi sağlar.
*   **Hit-Stop:** Bir `IEnumerator` rutini başlatarak animatörün hızını (`ownerAnim.speed = 0f`) kısa süreliğine sıfırlar ve sonra geri yükler.

### 3. `Health.cs` (Sağlık ve Hasar Mekanizması)
*   **Detay:** Can barını anında düşürmek yerine `Mathf.Lerp` kullanarak yumuşak (Smooth) bir düşüş sağlar. Hata toleransı (Exception Handling - `try-catch`) barındırır, böylece kalkan kontrollerinde oluşabilecek olası bir referans hatası tüm oyunun donmasını engeller. Ölüm anında Rigidbody'i kinematik yapar ve NavMeshAgent'ı kapatarak gereksiz fizik hesaplamalarını durdurur.

### 4. `TopcuBirligi.cs` (Sinematik Olay Döngüsü)
*   **Gereksinim:** Özel tanımlı `TopEfektAyari` sınıf listesi (Serialization).
*   **Detay:** Bütün olay döngüsünü `Coroutine` yapılarıyla yönetir. Müzik değişimlerini, saniye saniye gecikmeleri `yield return new WaitForSeconds()` ile kusursuz senkronize eder. Kod içerisinden direkt obje referansı vermek yerine `UnityEvent` kullanarak Unity Editör esnekliği sağlar.

### 5. `PowderBarrel.cs` (Dinamik Etkileşim ve AoE)
*   **Detay:** Kamerayı sarsmak için `CinemachineImpulseSource` kullanır. Hasar alanı `Physics.OverlapSphere` ile hesaplanıp, tespit edilen tüm Collider'lar `foreach` döngüsüne alınır ve eğer `Health` bileşenine sahiplerse hasar uygulanır.

## 🔮 Geliştirme Notları (Future Scope)
*   **Obje Havuzu (Object Pooling):** Askerlerin kılıç hasar efektleri (kan veya kıvılcım) oluşturulurken bellek yönetimi için Instantiate yerine Object Pooling mimarisi entegre edilebilir.
*   **Durum Makinesi (State Machine):** `SoldierAI.cs` içerisindeki if-else yapısı ilerleyen aşamalarda Finite State Machine (FSM) veya Behavior Tree (Davranış Ağacı) sistemine geçirilerek yapay zeka daha da karmaşık hale getirilebilir.
