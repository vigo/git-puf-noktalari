# Konfigürasyon nedir?

3 kapsamlı konfigürasyon bulunur:

1. **Local**: Sadece içinde bulunduğunuz (*dizin*) repository için geçerlidir. Kişisel
projelerinizde **kişisel** e-posta adresi kullanırken, şirket projelerinde şirket
tarafından verilen e-posta adresini kullanmanız gerekebilir.
1. **Global**: Bilgisayara giriş yapmış (*login olmuş*) kullanıcının erişim 
yetkisi olan tüm repository’ler için geçerlidir. Değer atarken `--global` anahtar 
kelimesi kullanılır.
1. **System**: Bilgisayardaki tüm kullanıcıları etkileyen en üst seviyedeki 
konfigürasyondur. Değer atarken `--system` anahtar kelimesi kullanılır.

Konfigürasyon ayarlarını yapmak için; `git config` komutunu kullanırız. İlk git
kurulumunda olmazsa olmaz olan iki tane konfigürasyon öğesi bulunur:

1. `user.name`
1. `user.email`
