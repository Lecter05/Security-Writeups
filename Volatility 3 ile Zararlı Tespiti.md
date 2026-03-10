## 1. İmajın Alındığı Zamanın Tespiti
```windows.info``` komutu ile timeline için bir adımdır oluşturuyoruz.
<img width="1130" height="648" alt="1  imaj ilk nezmana alındı" src="https://github.com/user-attachments/assets/bd40a269-7b4a-4c92-b3e0-002a0fd5f5c7" />


## 2. Kullanıcı Etkileşimli Şüpheli Süreçlerin Tespiti
Kullanıcının oturumundaki süreçleri incelemek için ```windows.sessions``` komutunu kullanıyoruz.
<img width="852" height="1016" alt="2  windows sessions kullanıcı etkilşimli garip bir durum varmı" src="https://github.com/user-attachments/assets/2cc2a78d-420f-4a97-8e2b-eaebb76726f0" />


## 3. PPID Kontrolü ile Doğrulama
Normal şartlarda ```lsass.exe```'nin ebeveyn süreci (PPID) ```wininit.exe``` olmalıdır. Ancak ```windows.pslist``` komutunu kullandığımızda PPİD explorer.exe görünüyor. 
<img width="1167" height="202" alt="3  Doğrulamak için Ppid kontrlü yapıyoruz" src="https://github.com/user-attachments/assets/e44f95c6-59c7-4b48-9c16-e46c2e62c351" />


## 4. Komut Satırı İncelemesi
Şüpheli sürecin nereden çalıştığını görmek için ```windows.cmdline``` komutunu kullanıyoruz.
<img width="974" height="82" alt="4  cmdline kontlü yapıldığında dosya dizini garip" src="https://github.com/user-attachments/assets/694faa85-badb-40c8-8358-4311b6f92b67" />


## 5. Dizin Şaşırtmacası
Saldırgan ayak oyunları ile ```lsass.exe``` dosyasının dizinini sanki normal bir süreçmiş gibi gizlemeye çalışmış.
<img width="732" height="1023" alt="5  olması gerekenden farklı bir dizin şaşırtmaca" src="https://github.com/user-attachments/assets/0a551fe2-e9e4-412e-a400-8ddc1081e44a" />


## 6. Anomalilerin Görüntülenmesi
Bellekteki gizlenmiş kodları görmek için ```windows.malfind``` komutunu kullanıyoruz. Şüpheli olarak tespit ettiğimiz process göze çarpıyor.
<img width="1133" height="938" alt="6  windows malfind komutu ile anomaliler görüntülendiğinde pid göze çarpıyor" src="https://github.com/user-attachments/assets/d6e6a5f3-b2d0-4817-8b77-b79f44b28a9e" />


## 7. Şüpheli Sürecin Dump Edilmesi
zararlı olduğundan emin olmak için süpheli processi ```windows.pslist --dump --pid <PID>``` komutu ile dump ediyoruz ardından ```sha256sum``` komutu ile dosya hashini alıyoruz. 
<img width="1389" height="244" alt="7  prosesi windows pslist --dump --pid dump edip hashini kontrol etmek üzere kopyalıyoruz" src="https://github.com/user-attachments/assets/b8ee091d-9511-4995-bf27-1bd4555c9bb9" />


## 8. Hash Kontrolü
hashi virustotalde sorguladığımızda herşey ortaya çıkıyor.
<img width="1635" height="985" alt="8  hash kontrol edildiğinde zararlı ortaya çıkıyor" src="https://github.com/user-attachments/assets/2a8288d4-7912-4be8-b0dd-bd260df0c0ca" />


## 9. Kullanıcı Parolası İçin Hash Dump Alınması
kullanıcının NTLM hash'lerini ```windows.hashdump``` komutu ile çekiyoruz.
<img width="863" height="173" alt="9 süreci tetikleyen kullanıcı profili hangisi " src="https://github.com/user-attachments/assets/8c325cec-6471-4b0c-881c-fd211e5e1e4b" />
<img width="954" height="368" alt="10  kullanıcı parolasını görmek için hash dump alıyoruz" src="https://github.com/user-attachments/assets/bfa771bf-906b-4d0b-84aa-a16c73e4f2f5" />

## 10. Hash'in Kırma
Hashin kırılması sürecini, https://crackstation.net/ sitesi sayesinde parolayı deşifre ediyoruz. 
<img width="1548" height="589" alt="11  hashcat&#39;te görüntülediğimizde parolaya ulaşıyoruz" src="https://github.com/user-attachments/assets/0ba0822b-e3bd-4780-bc92-e125a13efa60" />




