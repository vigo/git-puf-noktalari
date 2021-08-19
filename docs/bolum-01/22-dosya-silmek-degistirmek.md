# Dosya Silmek, Dosya Adını Değiştirmek

## `git mv`

Linus Torvalds, Linux’daki dosya operasyonlarının pek çoğunu GIT’e entegre
etmiş. Nasıl ki Unix/Linux’da bir dosyanın adını değiştirmek için;

```bash
$ mv dosya dosya_yeni_isim
```


kullanılıyorsa, aynı işi;

```bash
$ git mv dosya dosya_yeni_isim
```


şeklinde yapmak mümkün. Eğer adını ya da yerini değiştireceğimiz dosya
revizyon kontrolü altında değilse GIT size uyarı verir:

```bash
$ git mv file1 file_new_1

fatal: not under version control, source=file1, destination=file_new_1
```

Dosya track ediliyor, unuttunuz ve `mv` işlemini GIT üzerinden değil de,
işletim sistemi üzerinden yaptınız.

```bash
$ mv app.js application.js
$ git status

On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  
    deleted:    app.js
    
Untracked files:
  (use "git add <file>..." to include in what will be committed)
  
    application.js

no changes added to commit (use "git add" and/or "git commit -a")
```


GIT, `app.js` dosyasının silindiğini ve `application.js` dosyasının takip
altında olmayan yepyeni bir dosya olduğunu düşündü. Hatta artık `app.js`
dosyasını takipten çıkarmamız için bize;

```bash
$ git status

:
(use "git add/rm <file>..." to update what will be committed)
:
```

bile dedi... Şimdi biz bu değişikliği kayıt altına alalım, yani stage edelim:

```bash
$ git add .
$ git status

On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
  
    renamed:    app.js -> application.js
```

Ve GIT `app.js` dosyasını silmediğimizi sadece adını değiştirdiğimizi anladı.

```bash
$ git status

:
renamed:    app.js -> application.js
:
```

GIT, default olarak **Similarity Index** diye bir değere bakar. Eğer bu
karşılaştırma minimum **0.5** olması durumunda GIT bu iki dosyanın aynı olduğuna
karar verir.

GIT için önemli olan dosya adına değildir, **dosyanın içeriğidir**.

## `git rm`

Aynı `mv` gibi, işletim sisteminin bir kopya operasyonu da buradadır. Normalde
dosya silmek için;

```bash
$ rm file
$ rm -r folder/
```


yaparız. Aynı mantıkta önüne bir tek `git` takıyoruz:

```bash
$ git rm file
$ git rm -r folder
```


Eğer silme işini GIT üzerinden yapmazsak;

```bash
$ rm index-test.html
$ git status

On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  
    deleted:    index-test.html
    
no changes added to commit (use "git add" and/or "git commit -a")
```

Silinme durumunu GIT anladı ama staging’e atmadı. Bu işlemi bizim yapmamızı
istiyor. Eğer bunu `git rm` ile yapsaydık;

```bash
$ git rm index-test.html
$ git status

On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
  
    deleted:    index-test.html
```

otomatik olarak staging’e alındı. Tek yapmamız gereken şey commit etmek.

Silme ya da isim değiştirme işlerini kullandığınız **IDE** yerine mutlaka
komut satırından yapmanız sizin için daha kolay GIT kullanımı pratiği
yapmanızı sağlar.
