# Android Universal Debloat & Sistem Optimizasyon Aracı (v2.0.0)

Tüm Android cihazlar ve markalar (**AOSP, Samsung One UI, Xiaomi / Redmi / POCO (MIUI & HyperOS), OPPO / Realme / OnePlus, Huawei / Honor, Motorola, Vivo, Transsion, Sony, Asus, Nokia**) için geliştirilmiş, **tek dosya** halinde çalışan, **yedeklemeli ve geri yüklemeli** evrensel PowerShell debloat & optimizasyon aracıdır.

> **Uyumluluk:** Windows PowerShell 5.1+ ve PowerShell 7+ (Root gerektirmez, yalnızca USB/Kablosuz Hata Ayıklama yeterlidir.)

---

## Öne Çıkan Özellikler

- **Akıllı ADB Yönetimi (Online + Offline Yedek):**
  - Önce yerel klasör ve sistemdeki eksiksiz ADB kurulumlarını kontrol eder.
  - Bulamazsa **internet bağlantısı varsa** Google'ın resmi `platform-tools-latest-windows.zip` paketini indirip en güncel `adb.exe` dosyalarını otomatik kurar.
  - İnternet yoksa betiğin içine gömülü olan **offline ADB** aracını otomatik çıkartır.
- **Klasör Kirliliği Yok (Tekil Veri Klasörü):**
  - ADB dosyaları, cihaz yedekleri, oturum logları ve whitelist dosyası betiğin yanındaki tek bir `AndroidDebloatData\` klasöründe toplanır.
- **Cihaz Bazlı Otomatik Yedekleme & Tek Tıkla Geri Yükleme (`[R]`):**
  - Her debloat ve sistem ayarı değişikliğinden önce `<Marka>_<Model>_<SeriNo>_<Tarih>_backup.json` şeklinde otomatik yedek alır.
  - Değiştirilen Android ayarlarının işlem öncesi orijinal değerlerini kaydeder; geri yüklemede hem kaldırılan/devre dışı bırakılan paketleri (`install-existing` / `pm enable`) hem de sistem ayarlarını tam olarak eski haline döndürür.
- **3 Katmanlı Güvenli Katalog (370 Paket):**
  - **Seviye 1 — Güvenli:** Telemetri, reklam servisleri, operatör bloatware'leri ve arka plan izleme paketleri.
  - **Seviye 2 — Dengeli:** Medya, ofis, AI ve opsiyonel üretici uygulamaları.
  - **Seviye 3 — Agresif (Hard):** Google Drive, Android Auto, Galaxy Wearable, SmartThings, Samsung Health, mağaza ve bulut servisleri gibi kritik/derin sistem paketleri. *(Bootloop riski taşıyan `com.miui.cloudservice` otomatik listeden çıkarılmıştır.)*
- **Sistem Ayar Optimizasyonları & Seçmeli Private DNS (`[4]`):**
  - Animasyon hızlandırma (`0.5x`), pil/Doze ve arka plan optimizasyonu, marka bazlı gizlilik/telemetri kapatma.
  - **İsteğe Bağlı Private DNS:** AdGuard DNS (`dns.adguard-dns.com`), AdGuard Aile, Cloudflare, Quad9, NextDNS veya özel DNS sunucusu.
- **Görsel Paket Seçici (`[G]`) & Manuel Paket Yöneticisi (`[M]`):**
  - `Out-GridView` ile cihazda eşleşen paketleri açıklamalarıyla birlikte görsel pencerede seçip işlem yapma.
  - Cihazdaki tüm paketlerde arama, tekil kaldırma/dondurma/geri yükleme ve `whitelist.txt` (hariç tutma listesi) yönetimi.
- **Kablosuz ADB (`[9]`) & Bakım (`[7]`):**
  - Android 11+ için `adb pair` / `adb connect` desteği.
  - Sistem önbellek temizliği (`pm trim-caches`) ve Android sürümüne uyumlu ART derleme optimizasyonu (`bg-dexopt`).

---

## Kurulum ve Kullanım

### 1. Hazırlık (Telefon)
1. Telefonunuzda **Ayarlar > Telefon Hakkında > Derleme Numarası** (veya MIUI/HyperOS Sürümü) üzerine 7 kez dokunarak **Geliştirici Seçenekleri**'ni açın.
2. **Geliştirici Seçenekleri > USB Hata Ayıklama** seçeneğini aktif edin.
3. Telefonu USB kablosuyla bilgisayara bağlayın ve ekranda çıkan **"USB hata ayıklamaya izin ver"** penceresini onaylayın.

### 2. Çalıştırma (İnteraktif Menü)
[Releases](../../releases) sayfasından `Android-Universal-Debloat.ps1` dosyasını indirin ve PowerShell ile çalıştırın:

```powershell
powershell -ExecutionPolicy Bypass -File .\Android-Universal-Debloat.ps1
```

### 3. Komut Satırı (CLI / Otomasyon Modu)
Betiği parametreli olarak da kullanabilirsiniz:

```powershell
# Sadece cihazda eşleşen paketleri önizle (hiçbir şey silmez)
.\Android-Universal-Debloat.ps1 -DryRun

# Seviye 1 güvenli temizlik + sistem optimizasyonları (onay sormadan)
.\Android-Universal-Debloat.ps1 -Tier 1 -Optimize -NonInteractive

# Seviye 2 dengeli temizlik + AdGuard Private DNS + çıkışta ADB sunucusunu kapat
.\Android-Universal-Debloat.ps1 -Tier 2 -PrivateDns "dns.adguard-dns.com" -KillAdbOnExit

# Belirli bir yedekten geri yükle
.\Android-Universal-Debloat.ps1 -RestoreBackup ".\AndroidDebloatData\backups\Samsung_SM-S918B_XXXX_backup.json"
```

---

## Klasör Yapısı

Betiği çalıştırdığınızda yalnızca tek bir veri klasörü oluşur:

```text
Android-Universal-Debloat.ps1
└── AndroidDebloatData/
    ├── adb/           # Güncel (online) veya gömülü (offline) ADB dosyaları
    ├── backups/       # <Marka>_<Model>_<SeriNo>_<Tarih>_backup.json yedekleri
    ├── logs/          # <Marka>_<Model>_<SeriNo>_<Tarih>.log işlem kayıtları
    └── whitelist.txt  # Dokunulmasını istemediğiniz paketler
```

---

## Sorumluluk Reddi

Bu araç, root erişimi olmadan yalnızca `--user 0` (mevcut kullanıcı) kapsamında paket kaldırma/devre dışı bırakma ve standart ADB `settings` komutlarını uygular. Her işlem öncesi otomatik yedek alınır; yine de özellikle **Seviye 3 (Agresif)** işlemleri öncesinde `[6] Onizleme (Dry-Run)` çıktısını kontrol etmeniz önerilir.
