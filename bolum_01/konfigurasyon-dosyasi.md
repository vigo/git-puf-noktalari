## Konfigürasyon Dosyası

Windows işletim sistemi dünyasındaki `.ini` formatını andıran bir deklarasyon
sistemi bulunur. Dosya içinde **whitespaces** yani boşluk / alfabe dışındaki
karakterler görmezden gelinir. Kabaca;

    [bölüm]
        değişken = değer
        değişken = değer
        :
        :

stilindedir.

### `.git/config`

Bu dosya Local yani bulunduğumuz repo altındaki `.git/` altında bulunur ve
sadece o repo ile ilgili ayarları tutar. Bu kapsamda ayar yapmak için;

    git config user.name "Bu repo için kullanacağınız AD SOYAD bilginiz"
    git config user.email "Bu repo için kullanacağınız E-POSTA bilginiz"
    
    # ya da:
    git config --local user.name "Bu repo için kullanacağınız AD SOYAD bilginiz"
    git config --local user.email "Bu repo için kullanacağınız E-POSTA bilginiz"
    
    # örnek:
    # git config user.name "Uğur Özyılmazel"
    # git config user.email "vigo@example-local.com"

şeklinde işlem yapılır. `--local` anahtar kelimesi opsiyoneldir.
Kullanmazsanız sıkıntı olmaz.

### `~/.gitconfig`

Global dediğimiz, işletim sistemine **login** olmuş kullanıcı ile ilgili
ayarların tutulduğu dosyadır. Bu kapsamda ayar yapmak için;

    git config --global user.name "AD SOYAD"
    git config --global user.email "E-POSTA"
    
    # git config --global user.name "Uğur Özyılmazel"
    # git config --global user.name "ugurozyilmazel@...com"

şeklinde işlem yapılır. İşin sırrı `--global` anahtar kelimesindedir.

### `/etc/gitconfig`

Bu da tüm işletim sistemini etkileyen **system-wide** ayarların saklandığı
dosyadır. Bu kapsamda ayar yapmak için; **sudo** yetkisi gerekir ve;

    git config --system alias.st status
    git config --system color.ui true

gibi işlem yapılır ve tüm kullanıcıların ortak kullanabilecekleri şeyleri
ayarlamak mantklıdır. Eğer benim [macOS][1] kullanıyorsanız ve GIT’i [Homebrew][2]’dan
kurduysanız, bu dosyanın bulunduğu yer: `/usr/local/etc/gitconfig`’dir.

[1]: https://www.apple.com/macos/
[2]: https://brew.sh/
