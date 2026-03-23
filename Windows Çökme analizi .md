Sebebini bilmediğim, platform farketmeksizin videoları tam ekrana aldığımda windowsta çökme sorunu yaşıyordum.
araştırdığımda sorunu incelemek için şu şekilde bir yol izledim:

## 1. Güvenilirlik geçmişini görüntüle
<img width="783" height="333" alt="1  Güvenilirlik geçmişini görüntüle" src="https://github.com/user-attachments/assets/f5a18231-b820-4a52-8157-5ba7af1aa4e6" />

## 2. Windows Düzgün Kapatılamadı
Teknik ayrıntıları görüntüle
<img width="1906" height="676" alt="2  windows düzgün kapatılamadı" src="https://github.com/user-attachments/assets/961b35d8-12ed-4135-ade5-19a56ff84364" />


## 3. C:\Windows\Minidump
bu dizinde sorun yaşandığında windows otomatik olarak bir dump almış. ```Sorun yaşandığı sırada yeterince beklenmeden oturum kapatılırsa dump dosyası oluşmaz.```
<img width="1634" height="340" alt="3  Windows çalışmayı durdurdu" src="https://github.com/user-attachments/assets/ba9ab5ee-926f-4770-bdab-14c81c62b5bc" />

## 4. [WinDbg](https://apps.microsoft.com/detail/9pgjgd53tn86?launch=true&mode=mini&hl=tr-TR&gl=TR)
Yönetici olarak Windbg açılır ve File -> Open dump file diyerek Ardından komut satırına(kd>) ```!analyze -v``` komutu girilir. 
<img width="888" height="705" alt="4  windbg" src="https://github.com/user-attachments/assets/ef7e5a5e-0588-4162-a3bf-c615e63fad50" />

## 5. Analiz - İncelenmesi gereken kısımlar
- **BUGCHECK_CODE**: 133 (sorunun türü)
> Bu kısımda doğrudan hatanın ne olduğu araştırılabilir. 133 kodunun tam adı DPC_WATCHDOG_VIOLATION'dır — sistemin bir işlemin çok uzun süre takılı kaldığını fark edip kendini kapattığı anlamına gelir.

- **MODULE_NAME**: dxgmms2 (Suçlu)
> Hataya neden olan sürücü bu kısımda belirtilir. Sürücünün ne işe yaradığı buradan hareketle araştırılabilir. Bu örnekte dxgmms2.sys, Windows'un GPU bellek yöneticisidir.

- **FAILURE_BUCKET_ID**: 0x133_ISR_dxgmms2!VidSchIsMonitoredFenceSignaled (suçluyu ve konumunu)
> Bu satır, yukarıdaki iki bilgiyi bir araya getiren özet bir tanımlayıcıdır. Hata kodunu, hatanın yaşandığı sürücüyü ve hatanın tam olarak hangi fonksiyonda meydana geldiğini tek satırda gösterir. Kısaca "133 hatasını, dxgmms2 sürücüsünün VidSchIsMonitoredFenceSignaled fonksiyonu tetikledi" şeklinde okunabilir.

<img width="783" height="644" alt="image" src="https://github.com/user-attachments/assets/803acc8e-474b-484d-87e1-920587556871" />


## 6. Soruna dair
Benim sıkıntım özelinde sorunun GPU'dan kaynaklandığını, **FAILURE_BUCKET** kısmını araştırdığımda AMD sürücüsünü güncellenmesi gerektiği vurgulanmış.
Kontrol ettiğimde sürücünün sürümünün eski olması dikkat çekici.

<img width="400" height="184" alt="5  sürücü tarihi" src="https://github.com/user-attachments/assets/45e8fc3a-3eeb-48d2-9120-60e75ff2fc4c" />
<img width="399" height="184" alt="6  sürücü sürüm" src="https://github.com/user-attachments/assets/0e459582-7ee8-4fa3-bdf5-03925ae669c8" />

## 7. Çözüm 
yedek aldıktan sonra, sürücüyü güvenli modda kaldırılıp güncel versiyonunu kurduğumda sorun çözüldü.(DDU kullanılarak ta yapılabilir.)
