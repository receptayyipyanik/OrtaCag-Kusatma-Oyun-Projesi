# 🏰 [Oyunun Adı] - Proje Tanıtımı ve Vizyon Raporu

## 📖 Proje Özeti
Bu proje, tarihi savaşları, taktiksel ordu yönetimini ve sürükleyici bir Üçüncü Şahıs (Third-Person) aksiyon deneyimini bir araya getiren bir **Orta Çağ Kuşatma ve Savaş** oyunudur. Oyuncu, savaş meydanında birebir kılıç tokuştururken aynı zamanda ordusuyla birlikte fetihlere katılır ve düşman hatlarının gerisine sızarak sabotaj görevleri gerçekleştirir.

## 🎯 Şirketler, Yayıncılar (Publishers) ve Yatırımcılar İçin Öne Çıkan Özellikler (USPs)

Oyun dünyasında aksiyon oyunlarının kalitesini belirleyen en temel unsur "Game Feel" (Oyun Hissiyatı) metrikleridir. Bu proje, standart bağımsız yapımlardan ayrılarak aşağıdaki AAA (Yüksek Bütçeli) stüdyo tekniklerini çekirdek (core) yapısına entegre etmiştir:

1. **Gelişmiş Vuruş Hissiyatı (Hit-Stop Mekaniği):** Kılıç vuruşlarında düşman bedeniyle temas edildiği an animasyonun milisaniyeler bazında dondurularak (Hit-Stop) oyuncuya silahın ağırlığının ve darbenin gücünün hissettirilmesi sağlanmıştır.
2. **Açısal ve Dinamik Savunma Sistemi:** Kalkan kullanımı yalnızca bir animasyondan ibaret değildir. Yapay zeka veya oyuncu kalkan kaldırdığında, gelen saldırının açısı hesaplanır (Örn: 70 derecelik ön açı). Saldırı bu açıdan gelirse bloklanır ve saldıran tarafın animasyonu kırılarak (interrupt) oyuncuya taktiksel bir üstünlük yaratılır.
3. **Sinematik Sekanslar ve Olay Güdümlü Hikaye Anlatımı:** Oyunda sadece düz bir savaş alanı yoktur. Örneğin `TopcuBirligi` sistemi ile oyun içi ara sahneler (cutscenes) kullanılmadan, tamamen oyun motoru içinde (in-engine) ardışık top atışları, sur yıkımları, savaş boruları ve ordunun topluca hücuma kalkması senkronize bir şekilde işlenmiştir.
4. **Cinemachine Destekli Etki Geri Bildirimi:** Sabotaj görevlerinde patlayan barut fıçıları, sadece alana hasar vermekle kalmaz; Cinemachine Impulse sistemleri ile ekranda şiddetli sarsıntılar yaratır ve çevresel etmenleri (ev yangınları) tetikleyerek dünyayı değiştirir.
5. **Ölçeklenebilir Ordu Sistemi (Swarm/Horde Altyapısı):** `OrduYoneticisi` sistemi sayesinde, savaş alanındaki yüzlerce yapay zeka askeri tek bir merkezden koordine edilip belirli bir stratejik noktaya hücum ettirilebilir.

## 🔄 Temel Oynanış Döngüsü (Core Gameplay Loop)
1. **Keşif ve Hikaye:** Oyuncu haritadaki ipuçlarını (Gizli Harita vb.) bularak yeni sabotaj görevlerini açar. (Subtitle Manager ile anlatım)
2. **Sabotaj ve Zayıflatma:** Düşman hatlarının gerisine sızılarak düşman cephanelikleri (Barut Fıçıları) yok edilir.
3. **Büyük Kuşatma (Siege):** Topçu birliklerinin surları yıkmasıyla birlikte müttefik ordularla hücuma kalkılır.
4. **Yakın Çarpışma (Melee Combat):** Hayatta kalan düşman askerleriyle gelişmiş AI sistemlerine karşı birebir ve grup halinde çarpışılır.
5. **Fetih:** Tüm düşmanlar temizlendiğinde bölge ele geçirilir (Fetih Başarılı).

## 🚀 Projenin Mevcut Durumu
Projenin temel "Core Combat" (Çekirdek Savaş), "AI" (Yapay Zeka) ve "Görev/Etkileşim" (Quest/Interact) sistemleri başarıyla tamamlanmış ve modüler (kolayca yeni içerik eklenebilir) bir kod mimarisi ile inşa edilmiştir. Model, ses ve bölüm tasarımı (Level Design) ile cilalanarak (polish) hızla dikey kesit (Vertical Slice) aşamasına getirilmeye hazırdır.
