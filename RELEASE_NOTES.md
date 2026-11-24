## Android Universal Debloat & Sistem Optimizasyon Aracı v2.0.0

Tüm Android cihazlar ve markalar (**AOSP, Samsung, Xiaomi/MIUI/HyperOS, OPPO/Realme/OnePlus, Huawei/Honor, Motorola, Vivo, Transsion, Sony, Asus, Nokia**) için tek dosya halinde çalışan evrensel debloat ve sistem optimizasyon aracıdır.

### Yenilikler ve Özellikler

- **Akıllı ADB Yönetimi (Online + Offline):** İnternet varsa Google'ın resmi sunucusundan en güncel Platform-Tools (`adb.exe`) sürümünü otomatik indirip kurar; internet yoksa betiğin içine gömülü olan offline ADB'yi çıkartarak çalışır.
- **Tekil Veri Klasörü:** ADB dosyaları, yedekler, loglar ve whitelist dosyası yalnızca tek bir `AndroidDebloatData\` klasöründe toplanır.
- **Cihaz Bazlı Otomatik Yedekleme ve Geri Yükleme (`[R]`):** Her işlem öncesi `<Marka>_<Model>_<SeriNo>_<Tarih>_backup.json` yedeği alır; kaldırılan paketleri ve orijinal sistem ayarlarını tek tıkla geri yükleyebilirsiniz.
- **Güvenli Katalog Revizyonu (370 Paket):**
  - **Google Drive**, **Android Auto**, **Galaxy Wearable**, **SmartThings** ve **Samsung Health** gibi kritik uygulamalar yalnızca **Seviye 3 (Agresif / Hard)** katmanına taşındı.
  - Bootloop riski taşıyan `com.miui.cloudservice` otomatik listeden çıkarıldı.
- **Seçmeli Private DNS (`[4]`):** AdGuard DNS, AdGuard Aile, Cloudflare, Quad9, NextDNS veya özel DNS sunucusu isteğe bağlı olarak ayarlanabilir.
- **Görsel Paket Seçici (`[G]`):** `Out-GridView` ile eşleşen paketleri açıklamalarıyla birlikte görsel listeden seçerek işlem yapabilirsiniz.
- **Manuel Paket Yöneticisi & Whitelist (`[M]`):** Kurulu paketlerde arama, tekil kaldırma/dondurma/geri yükleme ve hariç tutma listesi.
- **Kablosuz ADB (`[9]`) & CLI Modu:** Android 11+ kablosuz hata ayıklama ve komut satırı parametre desteği (`-Tier`, `-DryRun`, `-Optimize`, `-PrivateDns`, `-RestoreBackup`, `-NonInteractive`).

### Hızlı Başlangıç

1. Aşağıdaki **Assets** bölümünden `Android-Universal-Debloat.ps1` dosyasını indirin.
2. Telefonunuzda **USB Hata Ayıklama**'yı açıp bilgisayara bağlayın.
3. PowerShell ile çalıştırın:
   ```powershell
   powershell -ExecutionPolicy Bypass -File .\Android-Universal-Debloat.ps1
   ```
