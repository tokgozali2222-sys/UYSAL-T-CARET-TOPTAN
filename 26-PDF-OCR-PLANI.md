# 26 PDF'den otomatik ürün çıkarma planı

## Dosyalar nereye yüklenecek?
Nihai yönetim panelinde **PDF İçe Aktar** bölümü olacak. Telefonda Dosyalar uygulamasından 26 PDF'yi seçip toplu yükleyebileceksiniz. Her dosya bir kategoriyle eşleştirilecek. İsterseniz önce 1 PDF ile pilot yapılacak.

## Sistem nasıl işleyecek?
1. PDF, özel bir `catalog-source-pdfs` depolama alanına yüklenir. Bu alan herkese açık olmaz.
2. Sunucu tarafındaki işleyici PDF sayfalarını işler. PDF'de gömülü metin varsa önce metin katmanı okunur; ürün görsellerinin içindeki yazılar için OCR/görüntü tanıma çalışır.
3. Her ürün için ürün görseli, önerilen ürün adı, birim fiyat, kategori ve kaynak PDF/sayfa bilgisi çıkarılır.
4. Sonuçlar doğrudan yayına girmez. **Kontrol bekliyor** ekranına gelir. Özellikle virgüllü fiyatlar, küsuratlar ve benzer ürün adları insan kontrolünden geçer.
5. Onaylanan kayıtlar ürün tablosuna eklenir ve ürün görselleri depoya aktarılır.
6. Fiyat güncellemesi için yeni PDF yüklenince sistem mevcut kayıtlarla eşleştirme önerir; farkları gösterir. Yönetici onayından sonra fiyatlar güncellenir.

## Gerçekçi beklenti
OCR %100 doğru değildir. Düşük çözünürlük, küçük yazı, eğik görüntü, arka plan ve fiyatın görselin içine basılmış olması hata oluşturabilir. Bu yüzden otomatik tanıma + kontrol kuyruğu tasarlanmalıdır. Fiyatın yanlış yayınlanmasını önlemek için onaysız OCR sonucu müşteriye gösterilmemelidir.

## Gerekli teknik parçalar
- Supabase Storage: PDF ve ürün görselleri
- Supabase Database: kategoriler, ürünler, OCR sonuçları ve durumları
- Sunucu tarafı PDF işleyici / Edge Function: PDF sayfalarını ayırma ve OCR servisine güvenli istek
- OCR servisi: basılı ürün adı ve fiyatını görüntüden okuma
- Yönetim paneli: PDF yükleme, kategori seçme, OCR sonuçlarını düzeltme ve toplu onay

Bu ZIP, web kataloğu ve veritabanı başlangıç iskeletidir. OCR motorunun API bağlantısı ve tam yönetici paneli henüz tamamlanmış değildir; bunun için seçilecek OCR servisi, güvenli sunucu işleyicisi ve test gerekir.
