# Cursor ile C Proje Şablonu

Cursor (VS Code)  ile C programlama için yapılandırılmış çalışma ortamı.

## Gereksinimler

### macOS

- **Xcode Command Line Tools** (zaten yüklü)
  ```bash
  xcode-select --install
  ```
- **VS Code C/C++ Extension** (ms-vscode.cpptools)

### Windows 7

- **MinGW-w64** - GCC derleyici
- **VS Code C/C++ Extension** (ms-vscode.cpptools)

## Kurulum

### Windows 7 için MinGW-w64 Kurulumu

1. **WinLibs'den indirin** (Önerilen - En Basit Yöntem)
   - https://winlibs.com/ adresine gidin
   - "Release Versions" bölümünden **GCC 13.x.x + MinGW-w64 (UCRT) - Win64** sürümünü indirin
   - Zip dosyasını `C:\` klasörüne çıkartın (bu `C:\mingw64` oluşturacak)

2. **PATH'e ekleyin**
   - Bilgisayarım → Sağ tık → Özellikler
   - Gelişmiş sistem ayarları
   - Ortam Değişkenleri
   - "Path" değişkenini bulun ve Düzenle
   - Yeni satıra `C:\mingw64\bin` ekleyin
   - Tamam'a tıklayın

3. **Doğrulama**
   - Yeni bir CMD penceresi açın
   ```cmd
   gcc --version
   gdb --version
   ```

### VS Code Extension Kurulumu

1. VS Code'u açın
2. `⌘⇧X` (macOS) veya `Ctrl+Shift+X` (Windows) tuşlarına basın
3. "C/C++" araması yapın
4. Microsoft tarafından sağlanan extension'ı yükleyin

## Kullanım

### Derleme

1. Derlemek istediğiniz `.c` dosyasını açın
2. `⌘⇧B` (macOS) veya `Ctrl+Shift+B` (Windows) tuşlarına basarak derleyin
3. Çalıştırılabilir dosya, kaynak dosyayla aynı klasörde oluşturulur

### Derleme ve Çalıştırma

1. Komut paletini açın: `⌘⇧P` (macOS) veya `Ctrl+Shift+P` (Windows)
2. "Tasks: Run Task" yazın
3. "Build and Run C Program" seçeneğini seçin

### Debug (Hata Ayıklama)

1. Hata ayıklamak istediğiniz `.c` dosyasını açın
2. Kod içinde breakpoint ekleyin (satır numarasının soluna tıklayın)
3. `F5` tuşuna basın veya Run and Debug panelinden başlatın
4. **macOS:** "Debug C Program (macOS)" seçin
5. **Windows:** "Debug C Program (Windows)" seçin

### Çalıştırma (Debug olmadan)

1. `.c` dosyasını açın
2. `⌃F5` (Ctrl+F5) tuşuna basın veya Run and Debug panelinden seçin
3. **macOS:** "Run C Program (macOS)" seçin
4. **Windows:** "Run C Program (Windows)" seçin

## Proje Yapısı

```
cproject/
├── .vscode/
│   ├── c_cpp_properties.json  # IntelliSense yapılandırması
│   ├── launch.json            # Debug yapılandırması
│   └── tasks.json             # Build görevleri
├── main.c                     # Ana C dosyası
└── README.md                  # Bu dosya
```

## Klavye Kısayolları

| İşlem | macOS | Windows |
|-------|-------|---------|
| Derleme | `⌘⇧B` | `Ctrl+Shift+B` |
| Debug Başlat | `F5` | `F5` |
| Çalıştır (Debug'sız) | `⌃F5` | `Ctrl+F5` |
| Breakpoint Ekle/Kaldır | Satır numarasına tıkla | Satır numarasına tıkla |
| Komut Paleti | `⌘⇧P` | `Ctrl+Shift+P` |

## Özellikler

- ✅ Otomatik derleme ve çalıştırma
- ✅ GDB/LLDB ile debug desteği
- ✅ IntelliSense kod tamamlama
- ✅ macOS ve Windows 7 uyumluluğu
- ✅ C17 standardı desteği
- ✅ Breakpoint ve step-through debugging
- ✅ Değişken izleme ve call stack görüntüleme

## Sorun Giderme

### "gcc: command not found" hatası
- **macOS:** Xcode Command Line Tools yüklü değil
  ```bash
  xcode-select --install
  ```
- **Windows:** MinGW PATH'e eklenmemiş veya CMD yeniden başlatılmamış

### Build task yanlış dosyayı derliyor
- Derlemek istediğiniz `.c` dosyasının VS Code'da **aktif** (açık ve seçili) olduğundan emin olun
- `tasks.json` veya başka bir dosya açıkken değil, C kaynak dosyası açıkken build yapın

### Debug başlamıyor (Windows)
- `gdb.exe` yolunun doğru olduğunu kontrol edin: `C:\mingw64\bin\gdb.exe`
- MinGW kurulumunuzda `gdb` olduğundan emin olun

### Debug başlamıyor (macOS)
- CodeLLDB extension'ı gerekmez (built-in LLDB kullanılıyor)
- Programın derlendiğinden ve çalıştırılabilir dosyanın oluştuğundan emin olun

## Notlar

- Derlenmiş çalıştırılabilir dosyalar kaynak dosyayla aynı klasörde oluşturulur
- **macOS/Linux:** Çıktı dosyası uzantısız (örn: `main`)
- **Windows:** Çıktı dosyası `.exe` uzantılı (örn: `main.exe`)
- Tüm programlar debug sembolleriyle (`-g` flag) derlenir
