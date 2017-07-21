# Bazı Dosyaları Takip Etmemek: `.gitignore`

Bazı durumlarda dosya ya da dosyaları ya da dizinleri takip dışında tutmak
istersiniz. Örneğin uygulamanızın `log` dosyaları, ya da kullandığınız text
editörü ile ilgili sadece sizi ilgilendiren dosyaları izole etmek
isteyebilirsiniz.

Belki de kullanıcı adı, şifre, ssh bilgileri ya da **SECRETS** dediğimiz
`ENVIRONMENT` değişkenlerinin ortalıkta dolaşmaması gerekebilir.

İşte bu tür durumlarda GIT’e bu dosyaları kaydetmemesini, yani takip etmemesini
söyleriz. Bu işleme **ignore** işlemi yani görmezden gelme işlemi denir.

Aynı konfigürasyon dosya mantığında, ya proje bazlı **local** ignore dosyaları
kullanırsınız ya da kendi `~/.gitconfig` dosyasında tanımladığınız `excludesfile`
değişkenindeki direktifleri kullanırsınız.

    [core]
        ;
        excludesfile = ~/.gitignore
        ;

Ya da dizin bazında işlem yapabilirsiniz. Repo’nun root’unda duran
`.gitignore` dosyası en derindeki dizine kadar etki eder. Eğer isterseniz alt
derinlikteki dizinlerde başka tanımlamalar yapabilirsiniz. Yani şöyle bir repo
olsa:

    .
    ├── sub-folder
    │   ├── demo.txt
    │   └── demo.xyz
    ├── file-1.txt
    ├── file-2.txt
    ├── file-3.txt
    ├── file-4.txt
    └── file.xyz

Hemen kontrol edelim durum nedir?

    $ git status --untracked-files
    
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
      
    	file-1.txt
    	file-2.txt
    	file-3.txt
    	file-4.txt
    	file.xyz
    	sub-folder/demo.txt
    	sub-folder/demo.xyz
        
    nothing added to commit but untracked files present (use "git add" to track)

Tüm dosyalar **untracked** yani eklenmeyi bekliyor. `xyz` extension’ı olan
dosyaları revizyon kontrol dışında tutalım. Bunun için projenin root’una
`.gitignore` dosyası ekliyorum:

    $ touch .gitignore
    $ echo '*.xyz' >> .gitignore
    $ git status --untracked-files
    
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
      
    	.gitignore
    	file-1.txt
    	file-2.txt
    	file-3.txt
    	file-4.txt
    	sub-folder/demo.txt
        
    nothing added to commit but untracked files present (use "git add" to track)

Dikkat ettiyseniz artık `file.xyz`, `sub-folder/demo.xyz` dosyaları
**untracked** olarak görünmüyor. Özellikle `git status --untracked-files`
şeklinde kullandım ki alt dizinlerin altındaki dosyaların da durumunu
görebilelim.

Hatta hangi dosyaların **ignore** edildiğini;

    $ git ls-files -o -i --exclude-standard
    
    file.xyz
    sub-folder/demo.xyz

şeklinde de görebiliriz. Ben olsam bunu bir **alias** yapardım :) Şimdi dizin
bazlı izolasyonu görelim.

    $ mkdir no-more-php-files
    $ touch test.php
    $ touch no-more-php-files/demo.php
    $ touch no-more-php-files/test.rb
    $ tree
    .
    ├── no-more-php-files
    │   ├── demo.php
    │   └── test.rb
    ├── sub-folder
    │   ├── demo.txt
    │   └── demo.xyz
    ├── file-1.txt
    ├── file-2.txt
    ├── file-3.txt
    ├── file-4.txt
    ├── file.xyz
    └── test.php

`no-more-php-files` dizini altındaki `*.php` dosylarını takip dışı bırakmak
istiyorum:

    $ echo '*.php' > no-more-php-files/.gitignore
    $ git status --untracked-files
    
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
      
    	.gitignore
    	file-1.txt
    	file-2.txt
    	file-3.txt
    	file-4.txt
    	no-more-php-files/.gitignore
    	no-more-php-files/test.rb
    	sub-folder/demo.txt
    	test.php
        
    nothing added to commit but untracked files present (use "git add" to track)

`no-more-php-files/` dizini altındaki `demo.php` izole oldu. Sağlamasını
yapalım:

    $ git ls-files -o -i --exclude-standard
    
    file.xyz
    no-more-php-files/demo.php
    sub-folder/demo.xyz

## Öncelik Sırası

Öncelik önemlidir. Her şey öncelik sırasına göre işlenir.

1. `core.excludesfile` konfigürasyonunda tanımlı olanlar
2. Repo’nun root’undaki `.gitignore`
3. Alt dizinlerdeki `.gitignore`’lar

Diyelim ki `log/` dizini var. Tüm log üreten servisler buraya yazıyor.
[Nginx](https://nginx.org/en/) buraya `access.nginx` şeklinde yazıyor,
[Gunicorn](http://gunicorn.org/) ise `gunicorn.log` şeklinde yazıyor. Biz,
sadece `*.log` yaparak gunicorn’u izole edebiliriz:

    $ mkdir log/ && echo '*.log' > log/.gitignore
    $ touch log/gunicorn.log
    $ git ls-files -o -i --exclude-standard
    
    file.xyz
    log/gunicorn.log
    no-more-php-files/demo.php
    sub-folder/demo.xyz

Peki, bir durum oldu, başka bir servis daha kullanmaya başladık ve o servis de
`foo.log` şeklinde log üretiyor ve senaryo bu ya, bunu konfigüre edemiyoruz.
Hatta bu dosyayı da takip etmek istiyoruz yani izole etmek **istemiyoruz!**
Yapmamız gereken `log/.gitignore` dosyasına bir satır daha eklemek:

    $ echo '!foo.log' >> log/.gitignore
    $ touch log/foo.log
    $ git status --untracked-files
    
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)

    	.gitignore
    	file-1.txt
    	file-2.txt
    	file-3.txt
    	file-4.txt
    	log/.gitignore
    	log/foo.log
    	no-more-php-files/.gitignore
    	no-more-php-files/test.rb
    	sub-folder/demo.txt
    	test.php
        
    nothing added to commit but untracked files present (use "git add" to track)


Gördüğünüz gibi `log/foo.log` artık track edilmeye hazır durumda.
`log/.gitignore` dosyasındaki sıralama çok önemli:

    *.log
    !foo.log

İlk satırda GIT’e `*.log` dosyalarını görme diyoruz. Hemen ikinci satırda da
`foo.log` dosyasını boş geçme, takip et diyoruz. `!` tersi anlamında. GIT ilk
olarak tüm `*.log` dosyalarını ignore ediyor ve sonra gelen direktife göre
`foo.log` dosyasını etmiyor.

Eğer bu ters yazılsaydı yani;

    !foo.log
    *.log

olsaydı, GIT önce `foo.log` dosyasını tutacak, sonra gelen satır **TÜM *.log
dosyalarını izole et** emrini vereceği için `foo.log` da kaynayıp gidecekti.

## Boş Dizinler

Repo’da, içinde dosya olmayan dizinler otomatik olarak görmezden gelinir.
`images/` diye bir dizinimiz olsa ve `.gitignore`’da:

    images/*.jpg

yazsa, `images/` altında sadece `*.jpg` dosyaları olsa, bu dizin komple ignore
edilir. 

    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
      
    	.gitignore
        
    nothing added to commit but untracked files present (use "git add" to track)

Eğer içinde başka bir dosya olursa, mesela `images/test.png` olsa;

    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
      
    	.gitignore
    	images/test.png
        
    nothing added to commit but untracked files present (use "git add" to track)

durum değişir ve bu dizin artık izole edilmez. Bu dizin ve içinde `*.jpg`
olmayan dosyalar repo’nun parçası olur.

[Ruby on Rails](http://rubyonrails.org/) dünyasından gördüğüm, hoşuma giden
bir taktiği paylaşmak istiyorum. Bazı durumlarda dizini korumak gerekir, yani
repo’nun bir parçası olması gerekir ama dizin altındaki belli dosyalar ya da
tüm dosyalar **ignore** edilmiş olabilir.

Bu durumda `!.gitkeep` devreye girer. Hemen örnek `.gitignore` dosyasına
bakalım:

    /.env
    /bin/
    *.sqlite3
    /project/media/*
    /project/fixtures/*
    /project/config/settings/development.py
    !.gitkeep

Sıralama önemli dedik. `!.gitkeep` mutlaka ignore edilenlerden sonra gelmeli.
Bu sayede, korumak istediğim herhangi bir dizin altına `.gitkeep` dosyası
koyduğum an o dizin track edilmeye başlayacak ve ignore edilmesi gereken
dosyalar da ignore edilecektir.
