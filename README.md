# Shadow Chat — iOS (Mac'siz derleme)

Bu klasör, Shadow Chat'in iOS App Store sürümünü **Mac olmadan** derlemek için
hazırlanmış native kabuktur (Capacitor). Uygulama `https://myshadow.live`'ı yükler.
Derleme **Codemagic** bulutunda (Apple'ın Mac'lerinde) yapılır.

---

## 1) Bu kodu GitHub'a yükle (~3 dk)

GitHub'da yeni boş bir repo aç: **github.com/new** → ad: `shadow-chat-ios` → **Create**.
Sonra bu klasörde (sunucuda) şu komutları çalıştır — `! ` ile başlat:

```
! cd /root/shadow-chat-ios && git init && git add -A && git commit -m "iOS wrapper" \
  && git branch -M main \
  && git remote add origin https://github.com/myshadowchat/shadow-chat-ios.git \
  && git push -u origin main
```

> Push sırasında kullanıcı adı + **GitHub şifresi yerine "Personal Access Token"** ister.
> Token: github.com → Settings → Developer settings → Tokens (classic) → Generate →
> "repo" iznini seç → kopyala, şifre sorulunca onu yapıştır.

## 2) Apple API anahtarı oluştur (Codemagic'in imzalaması için)

1. https://appstoreconnect.apple.com → **Users and Access → Integrations → App Store Connect API**
2. **Generate API Key** (Access: **Admin** veya **App Manager**).
3. İnen **.p8** dosyasını + **Key ID** + **Issuer ID**'yi sakla (bir kez iner!).

## 3) Codemagic'i bağla (~10 dk)

1. https://codemagic.io → **GitHub ile giriş yap** (ücretsiz).
2. **Add application → GitHub → shadow-chat-ios** seç.
3. **Teams → Integrations → App Store Connect → Connect**: yukarıdaki .p8 + Key ID +
   Issuer ID'yi gir, isim ver: **`ShadowAppStoreKey`** (codemagic.yaml'daki adla aynı!).
4. Uygulamada **Start new build → ios-release** workflow'unu çalıştır.

Codemagic; iOS projesini üretir, imzalar, derler ve **TestFlight**'a yükler.

## 4) App Store'a gönder

1. https://appstoreconnect.apple.com → **My Apps → +** ile uygulamayı oluştur
   (Bundle ID: **`live.myshadow.app`**, ad: Shadow Chat).
2. TestFlight'taki sürümü seç, **ekran görüntüleri + açıklama + gizlilik politikası
   URL'si** ekle (`PRIVACY.md` ve ikonlar hazır).
3. **Submit for Review** → Apple 1-3 günde yanıtlar.

---

## Notlar
- **appId / Bundle ID**: `live.myshadow.app` — App Store Connect'te de aynı olmalı.
- Apple "sadece web sitesi" kabuklarını reddedebilir; gerçek mesajlaşma/arama
  özellikleri olduğu için geçme şansı yüksek ama garanti değil.
