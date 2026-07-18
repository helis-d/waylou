# Waylou ACE CLI

![Waylou ACE CLI Banner](/docs/assets/waylou-banner.png)

Waylou ACE CLI, terminalinizden çalışan açık kaynaklı bir AI kodlama asistanıdır.
Google Gemini CLI projesinden fork'lanmıştır ve çoklu AI sağlayıcı desteği,
otonom ajan yetenekleri ve genişletilebilir mimarisiyle farklılaşır.

> ⚠️ **Durum:** Bu proje aktif geliştirme aşamasındadır. Temel işlevsellik
> çalışır durumdadır ancak bazı özellikler henüz tamamlanmamıştır. Katkılarınız
> beklenir.

## Neden Waylou ACE CLI?

- **Çoklu AI desteği**: Gemini, OpenAI, Anthropic, Ollama, DeepSeek — tek bir arayüzden hepsine erişin
- **Terminal öncelikli**: Kodla yaşayan geliştiriciler için tasarlandı
- **Otonom & interaktif**: Hem sohbet modunda hem de headless/otonom modda çalışır
- **ACE Spesifikasyonu**: CORE, STANDARD ve ENTERPRISE uyumluluk seviyeleriyle standartlaştırılmış ajan davranışı
- **MCP desteği**: Model Context Protocol ile özel entegrasyonlar
- **Açık kaynak**: Apache 2.0 lisanslı

## Kurulum

### Hızlı kurulum (npm)

```bash
npm install -g @waylou/cli
```

### Geliştirme kurulumu (kaynaktan)

```bash
git clone https://github.com/helis-d/waylou.git
cd waylou
npm install
npm run build
node run.js
```

## Kullanım

```bash
# İnteraktif mod
waylou

# Headless mod (script'ler için)
waylou -p "Bu kod tabanını açıkla"

# Belirli bir sağlayıcı ile
waylou --provider ollama
```

## Mimari

Waylou ACE CLI, monorepo yapısında birkaç ana paketten oluşur:

| Paket | Açıklama |
|-------|----------|
| `cli` | Terminal UI (Ink/React tabanlı) ve komut satırı arayüzü |
| `core` | Temel ajan mantığı, prompt yönetimi, tool sistemi |
| `provider` | Çoklu AI sağlayıcı katmanı (Gemini, OpenAI, Anthropic, Ollama, DeepSeek) |
| `ace-spec` | Agentic Coding Environment spesifikasyon ve validasyon |
| `autonomous-engine` | Otonom/headless çalışma motoru |
| `context-engine` | Vektör ve AST tabanlı semantik kod arama |
| `sandbox` | Güvenli çalıştırma ortamı |
| `sdk` | Harici entegrasyonlar için SDK |
| `vscode-ide-companion` | VS Code eklentisi |

## Sağlayıcılar (Providers)

Şu anda desteklenen AI sağlayıcıları:

- **Google Gemini** (varsayılan)
- **OpenAI** (GPT serisi)
- **Anthropic** (Claude serisi)
- **Ollama** (yerel modeller)
- **DeepSeek**

> Provider katmanı projenin en aktif geliştirilen kısmıdır. Yeni sağlayıcı
> eklemek için [CONTRIBUTING.md](./CONTRIBUTING.md) dosyasına bakın.

## ACE Spesifikasyonu

Waylou ACE CLI, standartlaştırılmış ajan davranışı için ACE (Agentic Coding
Environment) spesifikasyonunu uygular. Üç uyumluluk seviyesi vardır:

- **CORE**: Temel ajan yetenekleri — dosya işlemleri, shell komutları, web fetch
- **STANDARD**: Gelişmiş yetenekler — MCP entegrasyonu, checkpointing, sandbox
- **ENTERPRISE**: Kurumsal özellikler — politika motoru, audit logging, takım orkestrasyonu

## Katkıda Bulunma

Bu proje açık kaynaklıdır ve katkılara açıktır. Özellikle şu alanlarda yardıma
ihtiyacımız var:

- **Provider katmanı**: En büyük geliştirme ihtiyacı burada. Yeni AI sağlayıcıları entegre etmek, mevcut olanları iyileştirmek.
- **CLI özellikleri**: Yeni komutlar, UI iyileştirmeleri, kullanıcı deneyimi
- **Dokümantasyon**: Daha iyi rehberler ve örnekler
- **Test**: Test kapsamını artırmak

Detaylar için [CONTRIBUTING.md](./CONTRIBUTING.md) dosyasına bakın.

## Lisans

Apache License 2.0 — Detaylar için [LICENSE](./LICENSE) dosyasına bakın.

## Teşekkür

Bu proje [Google Gemini CLI](https://github.com/google-gemini/gemini-cli)
projesinden fork'lanmıştır. Orijinal projeye ve emeği geçen herkese teşekkür ederiz.