# Branch’lerle Çalışmak

GIT’in bence en önemli özelliği branch mekanizmasıdır. O an için çalıştığınız
yani içinde bulunduğunuz branch her ne ise, o branch’den ya da başka bir
branch’den **N tane**, belkide **onlarca**, **yüzlerce** kopya
çıkartabilirsiniz ve bu işlem **SIFIR MALİYETLİ** bir işlemdir.

GIT’in olmadığı ya da herhangi bir revizyon kontrol sisteminin olmadığı bir
ortamda çalışıyorsunuz ve projenin belli bir aşamasında, bir özelliği denemek
istiyorsunuz. Ne yaparsınız? Ya projeyi ya da o çalıştığınız dosyayı
kopyalarsınız ve o kopya üzerinde çalışırsınız.

Düşünsenize, 500 Megabytle’ık bir proje olsa, ufacık bir deneme için, ne olur
ne olmaz işi garantiye almak için, komple kopya aldınız. Diskinizden **500MB**
daha yer işgal ettiniz. Böyle 5-10 kere kopya yapsanız **Gigabyte**’lar
seviyesinde disk alanı harcamış olursunuz.

Diyebilirsiniz ki; 

> Amaaaan, ne olacak? bende Terrabyte seviyesinde disk var, 3-5 Gigabyte’ın lafı mı olur?

Hadi diyelim yer sorunu sıkıntı değil. 20 tane kopya yaptınız;

    proje        # bu esas dizin!
    proje_yedek
    proje_yedek_1
    proje_yedek_2
    proje_yedek_esas_1
    proje_yedek_esas_1_deneme
    proje_yedek_esas_1_deneme_son
    proje_yedek_3
    proje_yedek_3_son
    :
    :

gibi böyle çılgıncasına dizinler var bilgisayarınızda. Peki neler değişti?
Değişen dosyalar hangileri? Bunların listesini tuttunuz mu? Son aşamadan
`proje/` dizinini altına hangi dosyaları atacaksınız?

İşte bu ve buna benzer durumlar GIT tarafından süper basit bir şekilde
çözümleniyor:

    $ git branch # repo’daki branch’leri listele
    * master

GIT bize çalıştığımız kopyayı, branch’i söylüyor: **master branch**. Haydi
deneme yapalım, aklımıza bir şey geldi:

    $ git branch idea # adı idea olan yeni bir branch oluştur
    $ git branch
      idea
    * master

İçinde bulunduğumuz branch `*` ile işaretli. Şimdi yeni oluşturduğumuz
**idea** branch’ine geçelim:

    $ git checkout idea
    Switched to branch 'idea'

Artık bu alanda istediğimiz her şeyi deneyebiliriz. Birkaç yeni dosya ekleyelim:

    $ touch testing-file-ab-{1,2}.sh
    $ git add .
    $ git commit -m 'added 2 test files'
    $ ls
    
    file-1.txt
    file-2.txt
    file-3.txt
    file-4.txt
    file.xyz
    log
    no-more-php-files
    sub-folder
    test.php
    testing-file-ab-1.sh
    testing-file-ab-2.sh
    
    $ git log --graph --decorate --oneline --all
    
    * b34155b6b819 (HEAD -> idea) added 2 test files
    * 1304ac22cd97 (master) Example commit
    * 258f67c2e2cd [root] Initial commit

Bu çıktı bize şunu ifade ediyor:

1. Toplam 3 tane commit var
1. Çalıştığım yer **idea** branch’i (*HEAD*)

Şimdi master’a dönüp orada directoy list alalım:

    $ git checkout master
    Switched to branch 'master'
    
    $ ls
    
    file-1.txt
    file-2.txt
    file-3.txt
    file-4.txt
    file.xyz
    log
    no-more-php-files
    sub-folder
    test.php

İki branch arasındaki fark ne? master branch’de `testing-file-ab-1.sh` ve
`testing-file-ab-2.sh` dosyaları yok. Hatta şöyle sağlamasını yapalım:

    $ git diff HEAD idea --name-only # git help diff
    
    testing-file-ab-1.sh
    testing-file-ab-2.sh

**idea** branch’inde denemelerimizi tamamladık ve bu iki dosyayı artık
**master** branch’e almaya karar verdik. Bunu yapmak için yöntemlerden bir
tanesi branch’leri birleştirmek yani **merge** etmek!
