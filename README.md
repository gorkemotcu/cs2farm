# CS2 Farm Bot ve Yönetim Sistemi

Bu proje, CS2 oyununda tam otomatik XP farming yapmak için geliştirilmeye çalışılan bir programdır ve henüz eğitim amaçlıdır. YOLOv8 tabanlı görüntü işleme kullanarak rakipleri tespit eder, hedefler ve yüksek hassasiyetle ateş eder.

## Özellikler

- **YOLOv8 Nesne Tespiti**: Özel eğitilmiş modelinizi kullanarak oyuncu tespiti
- **Özerk Çalışma**: Kullanıcı girdisi olmadan düşmanları taramak, hedef almak ve ateş etmek için otomatik döndürme
- **Akıllı Hedef Seçimi**: Mesafe, boyut ve güven düzeyine dayalı öncelikli hedefler
- **Geri Tepme Kontrolü**: Silah geri tepmesini kontrol etmek için kompanse edici fare hareketleri
- **Burst Atış Modu**: Daha gerçekçi atış desenleri için yapılandırılabilir seri atış boyutu ve gecikmesi
- **Ayarlanabilir Parametreler**: Tüm parametreleri yapılandırma dosyası üzerinden kolayca ayarlama
- **Oturum İstatistikleri**: Performansı izler ve ayrıntılı günlükler kaydeder
- **Tam AFK Çalışma**: Tamamen gözetimsiz çalışır
- **Web Tabanlı Yönetim**: Çoklu VM yönetimi için web arayüzü
- **VM Entegrasyonu**: Hyper-V sanal makineleri ile entegrasyon

## Sistem Bileşenleri

Proje üç ana bileşenden oluşur:

1. **CS2 Bot (cs2_aimbot.py ve cs2_advanced_bot.py)**
   - YOLOv8 tabanlı hedef tespiti
   - Hassas nişan alma ve ateş etme mekanizmaları
   - Gelişmiş silah geri tepme kontrolü
   - Hareket tahmini ve izleme

2. **Web Kontrol Paneli (web_control.py)**
   - Flask tabanlı web arayüzü
   - VM ve bot yönetimi
   - Kullanıcı yönetimi ve kimlik doğrulama
   - İş kuyruğu ve durumu izleme

3. **VM İstemcisi (client.py)**
   - Sunucuyla iletişim
   - Bot işlerini yerel olarak çalıştırma
   - Steam ve CS2 otomatik başlatma
   - Oturum istatistikleri ve ekran görüntüleri

## Kurulum

### Sunucu (Web Kontrol Paneli)

1. Gereksinimleri yükleyin:
```bash
pip install Flask flask-login werkzeug psutil requests
```

2. Sunucuyu başlatın:
```bash
python web_control.py
```

3. Tarayıcınızda `http://localhost:8000` adresine gidin ve varsayılan kullanıcı adı/şifre ile giriş yapın (admin/admin)

### VM İstemcisi

1. Gereksinimleri yükleyin:
```bash
pip install ultralytics opencv-python numpy pyautogui keyboard mss torch pywin32 requests psutil
```

2. YOLOv8 modelinizi `runs\detect\cs2_model2\weights\best.pt` konumuna yerleştirin.

3. İstemciyi başlatın:
```bash
python client.py --server http://localhost:8000 --api-key API_ANAHTARINIZ
```

## Kullanım

### Web Arayüzünden

1. VM'leri yönetin (başlatma, durdurma, yapılandırma)
2. Bot işleri oluşturun (XP farm, ekran görüntüsü, drop talep etme)
3. İş durumlarını ve istatistiklerini izleyin

### VM Yapılandırması

VM'ler için `bot_config.json` dosyasını düzenleyerek şu ayarları yapabilirsiniz:

- `model_path`: YOLOv8 modelinizin yolu
- `confidence_threshold`: Düşman tespiti için minimum güven düzeyi (0.0-1.0)
- `rotation_speed`: Tarama yaparken dönüş hızı
- `aim_speed`: Fare hareketi hızı çarpanı
- `fov_x`, `fov_y`: Tespit için görüş alanı (ekranın yüzdesi)
- `headshot_offset`: Kafadan vuruş için dikey ofset (negatif değerler daha yükseğe nişan alır)
- `aim_smoothness`: Daha doğal, insan benzeri hareketler için daha yüksek değerler
- `recoil_control`: Geri tepme telafisini etkinleştir/devre dışı bırak
- `burst_fire`: Seri atış modunu etkinleştir/devre dışı bırak
- `burst_size`: Seri başına atış sayısı
- `burst_delay`: Seriler arasındaki gecikme (saniye)
- `auto_reload`: Otomatik yeniden doldurmayı etkinleştir/devre dışı bırak
- `reload_ammo_threshold`: Otomatik yeniden doldurmayı tetikleyecek atış sayısı

## Önemli Notlar

- Bu bot yalnızca eğitim amaçlıdır
- Rekabetçi çevrimiçi oyunlarda bot kullanmak hizmet şartlarını ihlal edebilir
- Her zaman sorumlu ve etik bir şekilde kullanın
- Yalnızca özel/çevrimdışı modlarda kullanmayı düşünün

## YOLOv8 Modelini Özelleştirme

En iyi tespit performansı için, YOLOv8 modelinizi şunlarla eğitin:
- Çeşitli oyun içi ekran görüntüleri
- Farklı karakter modelleri ve haritalar
- Çeşitli aydınlatma koşulları
- Farklı silah görünümleri

Bot'un takım arkadaşları ve düşmanlar arasında ayrım yapabilmesi için sınıf etiketlerini dahil etmeyi unutmayın. 
