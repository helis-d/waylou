# Waylou ACE CLI'ye Katkıda Bulunma

Bu projeye katkıda bulunmak istediğiniz için teşekkür ederiz. Waylou ACE CLI,
Google Gemini CLI projesinden fork'lanmış, açık kaynaklı bir projedir. Amacımız
terminalde çalışan, çoklu AI sağlayıcısını destekleyen, güçlü ve kullanışlı bir
kodlama asistanı oluşturmak.

## Projenin Şu Anki Durumu

Dürüst olalım: Bu proje henüz tam anlamıyla olgunlaşmamıştır. Fork sonrası
aktif olarak üzerinde çalışıyoruz ve eksiklerimiz var.

### En Büyük İhtiyaç: Provider Katmanı

Şu anda projenin **en büyük geliştirme ihtiyacı provider katmanındadır**
(`packages/provider`). Bu katman şunları yapar:

- Birden fazla AI sağlayıcısına (Gemini, OpenAI, Anthropic, Ollama, DeepSeek) tek bir arayüzden erişim
- Sağlayıcılar arası geçiş ve yük dengeleme
- BYOK (Bring Your Own Key) modeli ile kullanıcının kendi API anahtarını kullanabilmesi
- Takım orkestrasyonu (birden fazla sağlayıcıyı birlikte kullanarak iş bölümü)

Bu katmandaki bilinen sorunlar ve yapılacak işler:

- **Test kapsamı yetersiz**: `byok.test.ts` ve `orchestrator.test.ts` var ancak henüz temel seviyede
- **Yeni sağlayıcı entegrasyonları**: Yerel modeller (LM Studio, llama.cpp), bulut sağlayıcıları (Azure, Bedrock) için açık talepler var
- **Streaming kararlılığı**: Bazı sağlayıcılarda streaming yanıtlarında tutarsızlıklar olabiliyor
- **Hata yönetimi**: Sağlayıcı hatalarında daha iyi geri düşme (fallback) mekanizmaları gerekli

Eğer AI API'leri, SDK'lar veya provider entegrasyonları konusunda deneyiminiz varsa,
**tam olarak aradığımız kişisiniz**.

### CLI Katmanı

CLI katmanı (`packages/cli`) çalışır durumda ancak **yeni özelliklere açık**.
Özellikle şunlara ihtiyacımız var:

- Yeni slash komutları (`/explain`, `/fix`, `/refactor` gibi)
- Tema ve kişiselleştirme seçenekleri
- Çoklu oturum yönetimi
- Daha iyi hata mesajları ve kullanıcı geri bildirimi

CLI'ı olabildiğince zengin özelliklerle donatmak istiyoruz. Yaratıcı fikirleriniz
varsa lütfen paylaşmaktan çekinmeyin.

### Diğer Alanlar

- **Dokümantasyon**: README, kurulum rehberleri, kullanım örnekleri
- **Test**: Birim testleri, entegrasyon testleri
- **ACE Spesifikasyonu**: CORE, STANDARD ve ENTERPRISE seviyelerinin tanımlanması ve validasyonu

## Geliştirme Ortamı Kurulumu

```bash
# Repoyu klonla
git clone https://github.com/helis-d/waylou.git
cd waylou

# Bağımlılıkları yükle (Node.js ~20.19.0 gerekli)
npm install

# Projeyi derle
npm run build

# Geliştirme modunda çalıştır
node run.js
```

## Katkı Süreci

1. Önce bir **issue açın** ve ne yapmak istediğinizi anlatın. Böylece boşa emek harcamamış oluruz.
2. Repoyu fork'layın ve yeni bir branch oluşturun.
3. Değişikliklerinizi yapın.
4. Testleri çalıştırın: `npm test`
5. PR (Pull Request) gönderin.

### Commit Mesajları

Anlamlı ve açıklayıcı commit mesajları yazın. Örnek:

```
feat(provider): Anthropic provider'a streaming desteği eklendi
fix(cli): headless modda çökme sorunu giderildi
docs: kurulum rehberi güncellendi
```

## Kod Standartları

- TypeScript kullanın, tip güvenliğine dikkat edin
- Yeni özellikler için test yazın
- Prettier ve ESLint kurallarına uyun (`npm run lint`)
- Büyük değişiklikleri küçük PR'lara bölün

## Çalışma Şeklimiz

Bu proje tek kişi tarafından yönetiliyor ancak açık kaynak topluluğunun katkılarına
tamamen açık. Hiyerarşik bir yapımız yok — iyi fikir her yerden gelebilir.

İletişim için GitHub Issues'u kullanın. Mümkün olduğunca şeffaf ve açık
iletişim kurmaya çalışıyoruz.

## Lisans

Bu projeye yaptığınız katkılar Apache License 2.0 altında lisanslanacaktır.
Katkıda bulunarak bu şartları kabul etmiş olursunuz.