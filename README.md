# Pi-hole engelleme listesi

Pi-hole için kendi GitHub deponda barındırdığın bağımsız `hosts` dosyası. Dış bir
kaynağa bağlanmaz; liste tamamen bu depodaki `hosts.txt` dosyasından okunur.
Güncellemek için dosyayı elle düzenleyip commit edersin.

## Pi-hole kurulumu

1. Pi-hole arayüzünde **Adlists → Add** (veya **Group Management → Adlists**).
2. Adres kutusuna şunu yapıştır:

   ```text
   https://raw.githubusercontent.com/<KULLANICI>/<DEPO>/main/hosts.txt
   ```

   Bu depo için örnek:

   ```text
   https://raw.githubusercontent.com/ailantus/pihole-hosts/main/hosts.txt
   ```

3. **Tools → Update Gravity** çalıştır (komut satırından `pihole -g`).
4. Kontrol için `pihole -q doubleclick.net` gibi bir sorgu çalıştır.

> Depo **public** (herkese açık) olmalı. Özel depoda `raw.githubusercontent.com`
> adresi Pi-hole için yetki ister ve liste güncellenemez.

## GitHub'a yükleme

Klasör yerel olarak hazır (`main` dalı, ilk commit atılmış durumda). GitHub'da
`pihole-hosts` adında public bir depo açıp şunları çalıştır:

```powershell
cd "C:\Users\Ahmet\Documents\Varsayılan Proje\pihole-hosts"
git remote add origin https://github.com/ailantus/pihole-hosts.git
git push -u origin main
```

Depo adı farklı olursa yukarıdaki raw adresi ona göre düzenle. `git push` kimlik
bilgisi isterse GitHub Personal Access Token (repo yetkisi) kullan.

## Listeyi güncelleme

`hosts.txt` dosyasını istediğin gibi düzenle:

```text
0.0.0.0 reklam.example.com
0.0.0.0 izleyici.example.com
```

Sonrasında commit edip push et:

```powershell
git add hosts.txt
git commit -m "Engelleme listesi guncellendi"
git push
```

Pi-hole listeyi kendiliğinden çekmez; değişiklikten sonra **Tools → Update Gravity**
çalıştır.

## Notlar

- `hosts.txt` yaklaşık 2,5 MB ve 80 bininden fazla alan adı içerir; ilk gravity
  güncellemesi biraz sürebilir.
- Dosya `hosts` biçimindedir (`0.0.0.0 alan.adı`); Pi-hole bu biçimi doğrudan okur.
- `127.0.0.1 localhost` gibi yerel kayıtlar korunmuştur; bunları silme.
