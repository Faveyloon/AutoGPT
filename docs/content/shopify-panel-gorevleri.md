# Shopify Panel Görevleri ve Otomasyon Yol Haritası

Bu doküman, Faveyloon için hazırlanmış hızlı aksiyon planı ile standart Shopify panel yönetim adımlarını tek bir kronolojik akışta birleştirir. Amaç, mağaza güncellemelerinin ilk günden itibaren disiplinli biçimde yürütülmesini ve süreç sonunda otomasyonların devreye alınmasını sağlamaktır.

## 1. Stratejik Hazırlık ve Hızlı Durum Analizi

1. **Mağaza Sağlık Kontrolü:** Tema sürümü, kritik uygulamalar ve ödeme sağlayıcıları gözden geçirilerek mevcut problemler listelenir.
2. **Önceliklendirilmiş Hedefler:** Kampanya takvimi, satış hedefleri ve müşteri segmentleri doğrultusunda ilk 30 gün için en kritik iş kalemleri belirlenir.
3. **Veri Kaynaklarının Eşleştirilmesi:** Shopify, ERP/fulfillment sistemleri ve pazarlama kanalları arasında veri entegrasyonu için mevcut bağlantılar doğrulanır.

## 2. Tema ve Deneyim Optimizasyonu

1. **Tema Yedeklemesi:** Canlı temanın kopyası alınır, değişiklikler yedek tema üzerinde yapılır.
2. **Hızlı UX Düzeltmeleri:** Navigasyon, koleksiyon sayfaları ve checkout akışında tespit edilen kritik sorunlar düzeltilir.
3. **Performans İyileştirmeleri:** Görsel optimizasyonu, gereksiz uygulamaların kaldırılması ve yükleme hızını artıran ayarlar uygulanır.

## 3. Ürün ve Koleksiyon Yönetimi

1. **Ürün Verisi Temizliği:** SKU, barkod, fiyat ve stok verileri kontrol edilir; eksik veya hatalı bilgiler düzeltilir.
2. **Koleksiyon Hiyerarşisi:** Koleksiyon yapısı kampanya hedefleriyle uyumlu olacak şekilde yeniden düzenlenir.
3. **Otomatik Koleksiyon Kuralları:** Hedeflenen segmentlere göre etiket, stok durumu veya fiyat aralıklarına dayalı otomasyon kuralları tanımlanır.

## 4. İçerik, Kampanya ve Pazarlama Entegrasyonları

1. **Landing Page ve Blog İçerikleri:** Güncel kampanyaları destekleyecek sayfalar oluşturulur veya güncellenir.
2. **Promosyon Kurulumları:** İndirim kodları, otomatik indirimler ve upsell/cross-sell teklifleri yapılandırılır.
3. **Pazarlama Entegrasyon Kontrolleri:** Meta, Google ve e-posta servis sağlayıcılarıyla veri paylaşımı test edilir; izleme pikselleri doğrulanır.

## 5. Süreç Otomasyonu ve İzleme

1. **Sipariş ve Fulfillment Otomasyonları:** Sipariş durumlarına göre e-posta bildirimleri ve fulfillment entegrasyonları gözden geçirilir.
2. **Raporlama Panelleri:** Satış, stok ve kampanya performansını günlük/haftalık takip edecek rapor şablonları oluşturulur.
3. **Görev Yönetimi:** Tüm aksiyon maddeleri proje yönetim aracına (ör. Linear, Asana) taşınır ve sorumlular atanır.

## 6. Shopify x GitHub Tema Yayın ve Otomasyon Akışı

Shopify temalarının GitHub üzerinden yönetilmesi, geliştirme ve canlı ortamlar arasında kontrollü bir yayın akışı sağlar. Aşağıdaki adımları izleyin:

1. **GitHub Deposu ve Erişim Hazırlığı**
   - Shopify mağazasında **Settings → Apps and sales channels → Develop apps** yolunu izleyip mağaza için bir custom app oluşturun.
   - “GitHub ile bağlan” seçeneğiyle Shopify hesabınızı GitHub organizasyonunuza yetkilendirin.
   - Shopify’da kullanacağınız tema deposunu seçip canlı temayla eşleştirin; gerekli mağaza ve repository izinlerini verdiğinizden emin olun.

2. **Tema Branch Yapısı ve Koruma Kuralları**
   - `main` branch’i canlı temayı temsil edecek şekilde işaretleyin, yayınlanan her sürüm için `git tag` kullanın.
   - `develop` branch’ini staging temasıyla eşleştirerek QA süreçlerini burada yürütün.
   - Kısa ömürlü feature branch’lerde geliştirme yapın; GitHub üzerinde branch koruma kuralları ve zorunlu inceleme ayarlarını etkinleştirin.

3. **Yerel Geliştirme Ortamı ve CLI Kullanımı**
   - Shopify CLI’ı kurun (`npm install -g @shopify/cli @shopify/theme`).
   - `shopify login --store <mağaza-adı>` ve ardından `shopify theme pull --environment=live` komutuyla güncel temayı çekin.
   - Geliştirme sırasında `shopify theme dev` ile canlı önizleme açın; değişiklikleri `git add`, `git commit` ve `git push origin <branch>` komutlarıyla GitHub’a gönderin.

4. **Kod İnceleme, Test ve Otomatik Kontroller**
   - Her feature branch’i için Pull Request açın; Shopify önizleme bağlantısını PR açıklamasına ekleyin.
   - Shopify Theme Check (`shopify theme check --init && shopify theme check`) ve varsa jest/liquid testlerini yerel olarak çalıştırın.
   - `.github/workflows/theme-ci.yml` benzeri bir GitHub Actions iş akışı ekleyerek `npm install -g @shopify/cli @shopify/theme` ve `shopify theme check` komutlarını otomatik hale getirin.
   - CI kontrolleri geçtikten sonra PR’ları `develop` branch’ine birleştirip staging teması üzerinden kullanıcı kabul testlerini tamamlayın.

5. **Canlıya Alma, Otomatik Yayın ve Geri Dönüş Planı**
   - `develop` branch’inden `main` branch’ine release PR’ı açın; değişiklik özetini ve etkilenen şablonları dokümante edin.
   - Shopify panelindeki GitHub entegrasyon ekranında `main` branch’ine bağlı temayı yayınlayın veya otomatik yayın seçeneğini aktifleştirin.
   - Canlıya aldıktan sonra `git tag vYY.MM.DD` gibi sürüm etiketleri oluşturun; acil durumlarda etikete dönüp `git revert` akışıyla onarım sağlayın.

Bu akış, Faveyloon’un hızlı aksiyon ihtiyaçlarını standart Shopify operasyonlarıyla entegre ederken, GitHub destekli tema yönetimi ve CI kontrolleriyle sürdürülebilir bir geliştirme süreci sunar.
