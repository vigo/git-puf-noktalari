# Konfigürasyon İşlemleri

Sonuç olarak konfigürasyon dosyası adı üzerinde bir dosya. Herhangi bir text
editör ile açıp düzenleyebilirsiniz. En hızlı ve kolay yolu bu. Bunun dışında,
`git config` komutuna çeşitli parametreler geçerek değerleri sorgulayabilir,
silebilir, düzeltebilirsiniz. Çok daha fazla [detay için tıklayın][1].

## Comment Out (*Yorum*)

Bu dosyada **comment out** yani programlama dillerindeki gibi yorum satırı ya
da bazen bir şeyleri denemek için anlık satırı **off** etmek için popüler
programlama dillerinden alışkın olduğumuz `#` ve `;` kullanılmış:

```ini
# bu
# yorum
# satırı
; bu
; satır da yorum...
[user]
    name = Uğur Özyılmazel
```

## Değer Okumak: `--get`

Örneğin **core** grubu altında bulunan **filemode** değişkeninin değerini;

```bash
$ git config --get core.filemode
true
```

`--get GRUP.DEĞİŞKEN` şeklinde okuruz. Aslında `--get` opsiyonel. Yani yazmak
zorunda değilsiniz:

```bash
$ git config user.name
Uğur Özyılmazel
```

Ben [homebrew](https://brew.sh)’la beraber `bash-completion` paketini de
kullandığım için, pek çok GIT işlemini **auto-complete** ya da
**tab-completion** ya da otomatik olarak `TAB` tuşuna basınca tamamlama ile
kullanıyorum. İşlerim süper kolaylaşıyor ve daha az şey ezberlemek durumunda
kalıyorum.

---

**19 Ağustos 2021**

Mutlaka tavsiye ederim:

```bash
$ brew install git-extras
```

---

Linux türevleri genelde GIT paketini kurunca otomatik olarak bu tamamlamayı da
beraberinde getiriyor.

## Değeri Silmek: `--unset`

Şimdi denemek için kullanıcı seviyesinde değer ataması yapalım:

```bash
$ git config --global alias.s status
```

bu komut ile kısa yol tanımladık. artık `git status` yerine `git s` yapmak
yeterli. Bu **alias** konusuna ileride daha detaylı gireceğiz. Şimdi bu kısa
yolu silmek için:

```bash
$ git config --global --unset alias.s
```

yapmak yeterli.

## `include` ve `includeIf`

Yanılmıyorsam GIT versiyon 2.10+ ile gelen, benim çok sevdiğim hayatımı
kolaylaştıran 2 direktif. Benim gibi evde kişisel bilgisayar, işte ofis
bilgisayarı kullanıyorsanız aslında 2 farklı insan gibisiniz.

Belki birden fazla bilgisayarınız var. Duruma göre her bilgisayarın özel bir
konfigürasyon direktifine ihtiyacı olabilir.

Ya da sadece belli dizinlerin altında belli ayarlar çalışsa?

Her bilgisayarda ortak `~/.gitconfig` dosyasını kullanmak ama bilgisayarına
göre ayar yapmak istiyordum. İşte bu durumda imdadıma `include` yetişti.

```ini
[include]
    path = ~/.gitlocalconfig
```

`~/.gitlocalconfig` bu dosya her iki bilgisayarımda da bulunuyor. Ana GIT
konfigürasyon dosyamda `user` grubunda `name` ve `email` ayarları var. Farklı
bilgisayarlarda farklı GPG anahtarları kullandığım için (*bunun ne olduğunu
ileride anlatacağım*) `user.signingkey` değeri her makine için farklı :)

Eğer bulunduğum dizin `~/Dev/Amiga/Bronx-Sources/` ise
`~/.gitconfig-bronx-repos` konfigürasyon dosyasını kullan demek istiyorum.
Nasıl mı?

```ini
[includeIf "gitdir:~/Dev/Amiga/Bronx-Sources/"]
    path = ~/.gitconfig-bronx-repos
```

Bu dosyada yani `~/.gitconfig-bronx-repos` dosyasında ne mi var?

```ini
[user]
    name = vigo/bronx
    email = vigo@bronx....org
    signingkey = D3M(O)(SC/\/3)
```

yani ben ne zaman `cd ~/Dev/Amiga/Bronx-Sources/` yapıp, bu dizin altında bulunan
herhangi bir repoda işlem yapacak olursam, yukarıdaki değerler aktif olacak!

Bana şu soruyu sorabilirsiniz:

> Neden Local olarak ayar yapmadın?

İlgili dizin altın **300 tane repo** olsa? tek-tek dizinlerin altına gidip 
`git config` yapmak zorunda kalmak iyi bir fikir mi?

Son olarak `path = dosya` mantığında birden fazla path tanımlamak mümkün:

```ini
[include]
    path = ~/.git-localconfig-1
    path = ~/.git-localconfig-2
    path = ~/.git-localconfig-3
[includeIf "gitdir:~/Dev/C64/Zombie-Boys-Sources/"]
    path = ~/.git-zb-config-1
    path = ~/.git-zb-config-2
```

gibi...

[1]: https://git-scm.com/docs/git-config/
