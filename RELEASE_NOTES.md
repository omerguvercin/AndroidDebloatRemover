## Android Universal Debloat & Sistem Optimizasyon Aracı v2.0.1

Bu sürüm hata düzeltmeleri, CLI `-DryRun` güvenlik iyileştirmeleri ve en güncel gömülü Google Platform-Tools (`ADB`) paketini içerir.

### v2.0.1 Değişiklikler & Düzeltmeler

- **Güncel Gömülü ADB (`37.0.3-16887417`):** Çevrimdışı yedek olarak betiğe gömülü Google Platform-Tools (`adb.exe`, `AdbWinApi.dll`, `AdbWinUsbApi.dll`) sürümü `35.0.2` → `37.0.3-16887417` sürümüne güncellendi.
- **`-DryRun` Güvenlik & Seviye Düzeltmesi:**
  - `-Tier <1|2|3> -DryRun` artık yalnızca seçilen seviyeye kadar olan paketleri önizler.
  - `-DryRun` ile birlikte `-Optimize`, `-PrivateDns` veya `-RestoreBackup` verildiğinde cihazda hiçbir değişiklik yapılmaması garanti altına alındı.
- **Fallback Paket Takibi Düzeltildi:** Kaldırılamayıp otomatik fallback ile devre dışı bırakılan (`pm disable-user`) paketlerin sonraki taramalarda tekrar hedef olarak görünmesi engellendi.
- **Sistem Ayarı & Geri Yükleme Doğrulaması:**
  - `Set-AndroidSetting` artık yalnızca başarıyla uygulanan ayarları yedek kaydına ekler.
  - `Set-PrivateDnsConfig` başarısız olduğunda hatalı `[OK]` mesajı ve boş yedek dosyası oluşturmaz.
  - `Restore-DeviceBackup` içindeki `settings delete` işlemleri için hata kontrolü ve özet raporu eklendi.
- **Varsayılan Ayar & Whitelist İyileştirmeleri:**
  - `Reset-SystemOptimizations` içinde `sys_traced` varsayılan değeri `"0"` olarak düzeltildi.
  - Whitelist'e aynı paketin mükerrer eklenmesi engellendi ve manuel paket etkinleştirme (`[E]`) loglama/hata kontrolü eklendi.
  - Çevrimiçi ADB indirmesinde yalnızca güvenli `TLS 1.2` protokolü kullanılacak şekilde güncellendi.

### Hızlı Başlangıç

1. Aşağıdaki **Assets** bölümünden `Android-Universal-Debloat.ps1` dosyasını indirin.
2. Telefonunuzda **USB Hata Ayıklama**'yı açıp bilgisayara bağlayın.
3. PowerShell ile çalıştırın:
   ```powershell
   powershell -ExecutionPolicy Bypass -File .\Android-Universal-Debloat.ps1
   ```
