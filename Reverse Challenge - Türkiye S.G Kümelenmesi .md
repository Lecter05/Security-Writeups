## 1. Packer ve Dil Tespiti

[Detect It Easy (DIE)](https://github.com/horsicq/Detect-It-Easy) aracı ile Python dilinde yazıldığını ve PyInstaller ile paketlendiği görüyoruz.
<img width="1718" height="513" alt="1  packlenmiş mi" src="https://github.com/user-attachments/assets/8486a623-fdd9-489a-be80-74d6c697f541" />

## 2. Unpack
PyInstaller ile paketlenmiş, derlenmiş python dosyalar [pyinstxtractor](https://github.com/extremecoders-re/pyinstxtractor) ile dışarı çıkarılır.
<img width="1092" height="589" alt="2  pyinstxtractor indirilir ve bu komut çalıştırılır " src="https://github.com/user-attachments/assets/0b52ebb9-ced0-4017-93b4-5ffd4bb82c18" />

## 3. Komut sonrası oluşan dosyalar
```python3 pyinstxtractor.py reverse_challenge.exe``` komutu sonrası oluşan dosyalardan program çıktısındaki "[+] Possible entry point:" belirtilen dosyalar incelendi.
<img width="1841" height="501" alt="3  böyle dosyalar bırakır" src="https://github.com/user-attachments/assets/92e97440-429c-4901-9c15-8357ccd3720d" />

## 4. String İncelemesi
strings komutu ile incelenen dosyalardan **reverse.pyc** dosyası incelendiğinde, reverse_challenge.exe çalıştırıldığında görüntülenen yazılara raslandı.
<img width="1219" height="857" alt="4  string reverse py diyorum programdaki komutları gördüm" src="https://github.com/user-attachments/assets/0ea3d8f9-7843-41f2-97ba-44c0895844d8" />

## 5. Decompile İşlemi
**reverse.pyc** dosyasını kaynak koduna görebilmek için online python decompiler araştırıldı. [pylingual.io](https://pylingual.io/)
<img width="1149" height="398" alt="5  internette pyc file decompiller aratıyorum" src="https://github.com/user-attachments/assets/1254cb82-b378-4aa6-960b-214fe6667ac6" />

## 6. Kaynak Kod
Decompile edilen **reverse.py** kodlarına bakıldığında if bloğu içerisinde şifreye raslandı. 
<img width="1110" height="689" alt="6  işte kodlar" src="https://github.com/user-attachments/assets/1f4c2f4d-b534-4ea6-bbd4-b4f2732e3442" />

## 7. Şifre Deneme
şifre **reverse_challenge.exe**'de denendiğinde 1 saniyelik flag beliriyor.
<img width="708" height="292" alt="7  şifre çözüldü" src="https://github.com/user-attachments/assets/4365c5c8-d91c-4763-8fd3-f7d829002593" />

## 8. Flag ASCII hale getirme 
kod içerisindeki **flag_bytes** decimal formattan okunabilir hale getirildi ve flag elde edildi. 
<img width="723" height="300" alt="8  flag" src="https://github.com/user-attachments/assets/e2a01340-926c-4487-824b-ae95853d9829" />

