# Temel Konfigürasyon Öğeleri

## `core.editor`

`git commit`, `git merge` gibi durumlarda mesaj yazacağınız editörü ayarlamak
için kullanılır. Default olarak GIT, environment’ınızdaki `$VISUAL` ya da
`$EDITOR` değişkenlerine bakar.

Örneğin, editor olarak **emacs** kullanacaksanız ve;

```bash
$ export EDITOR="emacs"
```

şeklinde bir atama yaptıysanız editörünüz **emacs** olmuş demektir.
Environment bazlı `$EDITOR` değişkeni örnekleri:

```bash
export $EDITOR="mate -w"        # TextMate <3
export $EDITOR="emacs"          # Emacs
export $EDITOR="vim"            # Vim
export $EDITOR="atom --wait"    # Atom
export $EDITOR="subl -n -w"     # Sublime Text
```

Eğer environment’dan ayar yapmadıysanız, GIT üzerinden de bu ayarlamayı
yapabilirsiniz. Aşağıda çeşitli editör ayar örnekleri var. Hangi editörü
kullanacaksanız ilgili satırı uygulayabilirsiniz.

```bash
$ git config --global core.editor emacs           # emacs
$ git config --global core.editor vim             # vim
$ git config --global core.editor "mate -w"       # TextMate
$ git config --global core.editor "atom --wait"   # Atom
$ git config --global core.editor "subl -n -w"    # Sublime
```

## `color`

Renk ile ilgili işler için kullanırız. `git status`, `git diff` gibi
durumlarda renkli görmek algılamamızı kolaylaştırır. Bunu aktive etmek için:

```bash
$ git config --global color.ui true
```

yapmamız gerekir. Renklerini düzenleyebileceğimiz alt başlıklardan bazıları:
`branch`, `diff`, `status` aşağıdaki gibi ayarlanabilir.

```bash
$ git config --global color.status auto
$ git config --global color.diff auto
$ git config --global color.branch auto
```

Bu, GIT’in sizin ortamınıza göre, kullandığınız Terminal’e göre renk
ayarlaması yapması anlamındadır. İsteğe göre renk değerleri vermek mümkün.
Hemen `~/.gitconfig` dosyanızı açıp:

```ini
[color "branch"]
    current = yellow reverse
    local = yellow
    remote = green
    
[color "diff"]
    meta = yellow bold
    frag = magenta bold
    old = red bold
    new = green bold
    
[color "status"]
    added = yellow bold
    changed = green
    untracked = red
```

gibi ayar çekebilirsiniz. Yaptığımız ayarı kontrol etmek için;

```bash
$ git config color.status.added
yellow bold
```

geldiyse ayar doğru yapılmış demektir.

## `commit.template`

İlerleyen bölümlerde; [Commit nedir? Commit Mesajı nedir?](13-commit-mesaji-nedir.md)
konusunda çok işimize yarayacak bir ayar özelliğidir. Commit mesajı yazarken
bize hazır şablon çıkmasını sağlarız bu özellikle.

Şablon için bir dosya oluşturmak gerekiyor ve daha sonra kendi konfigürasyon
dosyanızda bu dosyanın yerini bildirmeniz gerekiyor. Ben bu dosyayı 
`$HOME/.git-commit-template.txt` şeklinde kullanıyorum.

```bash
$ git config --global commit.template ~/.git-commit-template.txt # örnek
```

şeklinde konfigürasyonu ayarlamanız gerekir. Peki bu şablon dosyasında ne
yazıyor?

    [İlk 50 karakter: Özet]
    
    [Açıklama: Neler oldu?]
    
    [Fixed #]
    

gibi bir şema kullanabilirsiniz. Bu durumda her `git commit` dediğinizde bu
şablon karşınıza çıkacak ve gerekli yerleri doldurmanız/silmeniz yeterli
olacaktır.

## `help.autocorrect`

Yanlış yazdığınızda, size yardımcı olacak bir asistan! Örneğin `git commit`
yerine `git conmit` yazdığınızda bunun `commit` olduğunu anlayacak ve bu
şekilde hareket edecek.

```bash
$ git config --global help.autocorrect true
```

Not: GIT pratiği açısından bunu aktif etmeyi önermiyorum. El alışkanlığı için
doğru yazmayı öğrenmek her zaman daha doğru diye düşünüyorum.

## `core.autocrlf`

İşletim sistemlerine göre **LINE ENDINGS** yani satır sonu/bitimi farklılıklar
gösteriyor. Özellikle Windows! Bir projede hem Windows hem Unix kullanıcısı
dosya kaydettiğinde, aralarında sıkıntı yaşamamak için ufak bir ayar yapmaları
gerekiyor.

Windows kullanıcısı:

```bash
$ git config --global core.autocrlf true
```

Unix (*Mac/Linux vb...*)

```bash
$ git config --global core.autocrlf input
```

yapması her iki kullanıcı için de sıkıntıyı ortadan kaldırıyor. Windows satır
sonlarına `\r\n` eklerken Unix türevleri `\n` ekliyor. `\n` **Line feed**
anlamındadır ve sonraki satırı ifade eder. **C**arriage **R**eturn **L**ine
**F**eed ise ek olarak cursor’u (*imleçi*) da başa alır. Bu bakımdan `\n`
yerine `\r\n` kullanır.

Konfigürasyondaki bu ayarlama özelliği sayesinde Windows kullanıcısının
düzenlendiği dosyayı Linux/Unix kullanıcısı açtığında sorun yaşamadığı gibi
Windows kullanıcısı da Linux/Unix kullanıcısından gelen dosyaları sıkıntısız
açabiliyor.

## `core.whitespace`

GIT default olarak **boşluk** karakteriyle ilgili bir kısım anlama özelliği
ile geliyor. Default olarak gelen **3 seçenek**;

1. **blank-at-eol**: Satır sonundaki space (*boşluk*) karakter(ler)i
1. **blank-at-eof**: Dosya sonundaki space (*boşluk*) karakter(ler)i
1. **space-before-tab**: Satır başındaki `tab` karakterinden önce gelen space (*boşluk*) karakter(ler)i

Buna ek olarak kapalı (*disabled*) gelen **3 özellik**;

1. **indent-with-non-tab**: `tab` yerine `space` ile indent (girintilenmiş) edilmişler
1. **tab-in-indent**: Satır içindeki `tab` ile girintilenmiş yerler
1. **cr-at-eol**: Satır sonundaki **carriage returns** yani ENTER/RETURN tuşuna basınca çıkanlar düzgün mü?

Bu konu ile ilgili farklı konfigürasyon kullanımları bulunmakta.
**whitespace** sorunu yaşamamak için ben;

```bash
$ git config --global core.whitespace fix,-indent-with-non-tab,trailing-space,cr-at-eol
```

şeklinde kullanıyorum. Başka bir örnekte:

```bash
$ git config --global core.whitespace trailing-space,space-before-tab
```

## `core.excludesfile`

`.gitignore` dosyasının global olanı. Dizin bazında `.gitignore` ile dosyaları
revizyon kontrol dışında tutabiliyoruz. Bunu genel olarak kullanmak istersek,
aynı `~/.gitconfig` gibi `~/.global_gitignore` gibi bir dosya oluşturup:

```bash
$ git config --global core.excludesfile ~/.global_gitignore
```

gibi ayarlarsak, otomatik olarak belirlediğimiz dosyaları revizyon kontrol
dışına alabiliriz. Unutmayın ki, proje bazlı `.gitignore` dosyası, repository
içinde olduğu için, projeye katkı yapan diğer kullanıcılar tarafından da
kullanılabiliyor.

Bu bakımdan, global olarak **ignore** ettiğiniz şeyler başka kimseye
geçmeyeceği için dikkatli kullanın.

Örnek bir `.gitignore`:

    .DS_Store
    ._*
    .Spotlight-V100
    .Trashes
    *.pyc
    xcuserdata
    .sass-cache
    .bundle
    vendor/bundle

Pek çok temporary (*temp*) dosya ve benzeri şeyleri ignore eden [bu dosyaya][1] 
bir göz atın derim.

## `rerere`

**Re**use **re**corded **re**solution yani merge esnasında yaşanan
conflict’lerin çözümlerini hatırla ve bir daha aynısı olursa otomatik olarak
çöz! GIT bazen bizden daha akıllı olabiliyor :) Bu özelliği aktive etmek için;

```bash
$ git config --global rerere.enabled true
```

yapmak yeterli.

## `status.submoduleSummary`

Submodule’ler le çalıştığınız zaman işinize yarayacak. `git status`
dediğinizde, repo altındaki submodule’lerin de durumunu görmeniz gerekebilir.

```bash
$ git config --global status.submoduleSummary true
```

[1]: https://raw.githubusercontent.com/github/gitignore/master/Python.gitignore
