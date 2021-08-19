# Konfigürasyon Nedir?

3 kapsamlı konfigürasyon bulunur:

## Local

Sadece içinde bulunduğunuz (*dizin*) repository için geçerlidir. Kişisel
projelerinizde **kişisel** e-posta adresi kullanırken, şirket projelerinde şirket
tarafından verilen e-posta adresini kullanmanız gerekebilir.

## Global

Bilgisayara giriş yapmış (*login olmuş*) kullanıcının erişim 
yetkisi olan tüm repository’ler için geçerlidir. Değer atarken `--global` anahtar 
kelimesi kullanılır.

## System

Bilgisayardaki tüm kullanıcıları etkileyen en üst seviyedeki 
konfigürasyondur. Değer atarken `--system` anahtar kelimesi kullanılır.

Konfigürasyon ayarlarını yapmak için; `git config` komutunu kullanırız. İlk
GIT kurulumunda olmazsa olmaz olan iki tane konfigürasyon öğesi bulunur:

1. `user.name`
1. `user.email`
