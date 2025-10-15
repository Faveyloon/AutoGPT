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

## 6. Shopify x GitHub Tema Yayın Akışı

Shopify temalarının GitHub üzerinden yönetilmesi, geliştirme ve canlı ortamlar arasında kontrollü bir yayın akışı sağlar. Aşağıdaki adımları izleyin:

1. **GitHub Entegrasyonunu Aktifleştirme**
   - Shopify yönetim panelinden **Settings → Apps and sales channels → Develop apps** adımlarını izleyin.
   - “GitHub ile bağlan” seçeneğini kullanarak Shopify hesabınızı GitHub organizasyonu veya hesabınızla yetkilendirin.
   - Tema deposu olarak kullanacağınız GitHub repository’sini seçin.

2. **Tema Branch Yapısını Oluşturma**
   - `main` branch’i canlı temayı temsil edecek şekilde belirleyin.
   - Geliştirme için `develop` ve özellik bazlı kısa ömürlü feature branch’leri oluşturun.
   - Shopify’ın önizleme temalarını kullanarak her feature branch’ini test edin.

3. **Yerel Geliştirme ve CLI Kurulumu**
   - Shopify CLI’ı kurun (`npm install -g @shopify/cli @shopify/theme`).
   - `shopify theme pull` komutuyla canlı temanın son sürümünü yerel ortama alın.
   - Değişiklikleri tamamladıktan sonra `shopify theme push --allow-live` komutuyla ilgili branch’e gönderin.

4. **Kod İnceleme ve Test Süreci**
   - Her feature branch’i için Pull Request (PR) açın; görsel değişiklikler için tema önizleme bağlantısını PR açıklamasına ekleyin.
   - Stil ve Liquid hatalarını yakalamak için Shopify Theme Check (`shopify theme check`) çalıştırın.
   - Onaylanan PR’ları `develop` branch’ine birleştirin ve gerekli ise staging teması üzerinden kullanıcı kabul testlerini yapın.

5. **Canlıya Alma ve Geri Dönüş Planı**
   - `develop` branch’inden `main` branch’ine release PR’ı açın; sürüm notlarını ve etkilenen sayfaları belgeleyin.
   - Shopify panelinden `main` branch’ine bağlı temayı yayınlayın.
   - Olası geri dönüşler için bir önceki release etiketini `git tag` ile saklayın; acil durumlarda ilgili etikete dönerek `shopify theme push` ile yayına alın.

Bu akış, Faveyloon’un hızlı aksiyon ihtiyaçlarını standart Shopify operasyonlarıyla entegre ederken, GitHub destekli tema yönetimiyle sürdürülebilir bir geliştirme süreci sunar.
