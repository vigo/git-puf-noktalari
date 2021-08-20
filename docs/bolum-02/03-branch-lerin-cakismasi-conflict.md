# Branch’lerin Çakışması: Conflict

Aynı dosyalar üzerinde çalışınca **conflict** yanı çakışma yaşamak
kaçınılmazdır. Duruma göre bu çakışmalar çok can sıkıcı olabilir. Bazen kabus
haline bile dönüşebilir. Halk arasında **conflict yemek** olarak da bilinir.

GIT sağ olsun çözüm yöntemlerini öğrenip (*daha doğrusu kaydedip*) benzer
çakışma olduğu zaman otomatik olarak çözebiliyor. Bunun için konfigürasyon
ayarı yapmak gerekiyor:

```bash
$ git config --global rerere.enabled true
```


**rerere** yi ilk gördüğümde bir Beşiktaş taraftarı olarak aklıma
Galatasaray’ın **rerere rarara** tezahüratı gelmişti :) Ne demek rerere ?
**Reuse Recorded Resolution** (*of conflicted merges*) yani: branch’leri merge
ederken (*birleştirirken*) kaydedilen çözüm şeklini, aynı çakışma olduğu an
tekrar kullan.

Bir web uygulaması yapıyoruz, yeni bir feature geliştirmek istiyoruz. Uygulama
yapısı aşağıdaki gibi:

    .
    ├── public
    │   ├── css
    │   │   └── application.css
    │   ├── images
    │   │   └── photo.jpg
    │   └── js
    │       └── global.js
    └── index.html

Yeni feature için bir branch açıp çalışalım:

```bash
$ git checkout -b feature
Switched to a new branch 'feature'

# index.html’e eklemeler yaptık, css’e ek yaptık
$ git add .
$ git commit -m 'Footer information added'
[feature c5084b90ab6e] Footer information added
 2 files changed, 6 insertions(+)
```


![Demo site örnek site ekran görüntüsü](branch-lerin-cakismasi-conflict/feature-c5084b90ab6e.png "Demo site")

```bash
$ git log --graph --decorate --oneline --all

* c5084b90ab6e (HEAD -> feature) Footer information added
* 60ee4fd58668 (master) Demo site initiated
* fea8c5d8e385 [root] Initial commit
```


Şimdi tam bu esnada, bir telefon geldi ve hemen **master** branch’deki
`index.html` dosyasında bir değişiklik yapmanız gerektiğini öğrendiniz. Henüz
geliştirmekte olduğunuz şeyi de bitirmediniz... Ne lazım?

```bash
$ git checkout master
```

gereken değişikliği yaptınız:

```bash
$ git diff head:index.html feature:index.html
```

ve;

```diff
diff --git a/index.html b/index.html
index d62d871da6ef..4fbafe3dfd2b 100644
--- a/index.html
+++ b/index.html
@@ -9,8 +9,10 @@
     </head>
     <body>
         <header>
-            <h1>Demo Site 2017</h1>
+            <h1>Demo Site</h1>
         </header>
-        <script src="public/js/global-1.js"></script>
+        
+        <footer>Address information</footer>
+        <script src="public/js/global.js"></script>
     </body>
 </html>
```

Şimdi commit edelim:

```bash
$ git add .
$ git commit -m 'added: 2017 text to heading1 and some other fixes'

[master 8f9bb3474c79] added: 2017 text to heading1 and some other fixes
 1 file changed, 1 insertion(+), 1 deletion(-)
```


Log’da durum nasıl görünüyor ?

```bash
$ git log --graph --decorate --oneline --all

* 8f9bb3474c79 (HEAD -> master) added: 2017 text to heading1 and some other fixes
| * c5084b90ab6e (feature) Footer information added
|/  
* 60ee4fd58668 Demo site initiated
* fea8c5d8e385 [root] Initial commit
```


`60ee4fd58668` ID’li commit’den türeyen 2 commit var:

1. `c5084b90ab6e`
1. `8f9bb3474c79`

Bu iki commit arasındaki fark ne?

```bash
$ git diff c5084b90ab6e 8f9bb3474c79 # feature ile HEAD arasındaki diff bu yani
$ git diff feature HEAD              # aynı şey
```

çıktısı:

```diff
diff --git a/index.html b/index.html
index 4fbafe3dfd2b..d62d871da6ef 100644
--- a/index.html
+++ b/index.html
@@ -9,10 +9,8 @@
     </head>
     <body>
         <header>
-            <h1>Demo Site</h1>
+            <h1>Demo Site 2017</h1>
         </header>
-        
-        <footer>Address information</footer>
-        <script src="public/js/global.js"></script>
+        <script src="public/js/global-1.js"></script>
     </body>
 </html>
diff --git a/public/css/application.css b/public/css/application.css
index e166ec262bd6..018697659236 100644
--- a/public/css/application.css
+++ b/public/css/application.css
@@ -9,8 +9,4 @@ h1, h2, h3, h4, h5, h6 {
     color: #b65;
     padding: 0;
     margin: 1rem 0;
-}
-
-footer {
-    color: #a73;
 }
\ No newline at end of file
```

Birinde olan diğerinde yok ya da diğerinde tamamen başka bir şey var. Biz
master branch’deyiz ve `git merge feature` dediğimiz an conflict yiyeceğimiz ap
açık ortada. Karşımızdaki seçenekler:

1. Kodu yazan biz olduğumuz için ne olması gerektiğini biliyoruz, elle gereken
düzeltmeleri yapacağız.
1. Doğru olan kısım **master** branch’deki kısım, esas olan o!
1. Doğru olan kısım **feature** branch’deki kısım, esas olan o!
1. Amaaaan, bana ne ya, vazgeçiyorum! kim merge ederse etsin! :)

Haydi o zaman:

```bash
$ git merge feature
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Recorded preimage for 'index.html'
Automatic merge failed; fix conflicts and then commit the result.
```


Evet, GIT, otomatik olarak `index.html`’i **merge** etmek istedi ama bu
dosyada **merge conflict** ile karşılaştı ve olası çözüm için kayda geçti:

    Recorded preimage for 'index.html'

Durum ne?

```bash
$ git status

On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)
  
Changes to be committed:

	modified:   public/css/application.css
    
Unmerged paths:
  (use "git add <file>..." to mark resolution)
  
	both modified:   index.html
```


`public/css/application.css` bunda sıkıntı yok. `both modified` ne demek?
Kelime anlamı olarak **her ikisi de değişti** gibi bir şey çıkıyor. Burada bahsi
geçenler kim? Az önce karşımızdaki seçeneklerden bahsetmiştim. Doğru olan
kısım **master** ya da **feature**...

GIT, birleştirmek istediğimiz branch’i **ONLARIN** yani **theirs**, içinde
bulunduğumuz branch’i de **BİZİM** yani **ours** olarak sınıflandırıyor.
Bir şeyin `both modified` olması demek, hem bizim tarafın, hem de onların
tarafın modifiye olması demek.

Şimdi son seçenek olan: **Bana ne! vazgeçtim** i yapalım. master branch için
(*şu an master branch’deyiz ya*) merge’den önceki son commit hangisiydi?

```bash
$ git reset --hard 8f9bb3474c79
HEAD is now at 8f9bb3474c79 added: 2017 text to heading1 and some other fixes
```

Her commit, aslında zamanın fotoğrafını çekmek değil miydi? Şimdi o an’a geri
döndük. Özellikle `--hard` kullandık ki geride bir şey kalmasın. `git reset`
konusunu ileride göreceğiz. Şimdi tekrar merge edip conflict’e geri dönelim:

```bash
$ git merge feature
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Recorded preimage for 'index.html'
Automatic merge failed; fix conflicts and then commit the result.
```

Şu sorunlu `index.html`’e bir bakalım:

```html
<!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title>Demo site</title>
        <link rel="stylesheet" href="public/css/application.css" type="text/css" />
    </head>
    <body>
        <header>
            <h1>Demo Site 2017</h1>
        </header>
<<<<<<< HEAD
        <script src="public/js/global-1.js"></script>
=======
        
        <footer>Address information</footer>
        <script src="public/js/global.js"></script>
>>>>>>> feature
    </body>
</html>
```

Bu dosyada dikkat edeceğimiz şeylerin başında gelen işaretle:

1. `<<<<<<<`
1. `>>>>>>>`
1. `=======`

`<<<<<<< HEAD` diye ifade işaretlenen yer **master** branch’de olan fark. Yani
**BİZİM** yani `--ours`. `>>>>>>> feature` diye işaretlenen yer **feature**
branch’de olan fark. Yani **ONLARIN** yani `--theirs`. `=======` ise ayraç.
Üst ile alt kısmı ayırıyor.

Şimdi;

1. Ya doğru olanı, olması gerekeni biz bildiğimiz için kendi kafamıza göre
gereken değişikliği yapacağız
1. Ya doğru olan bizim taraf, onların tarafı unut diyeceğiz
1. Ya da doğrusu onların, bizimkini çöpe at diyeceğiz

Bu örnek süper basit ve çok rahat anlaşılıyor ne olduğu. Daha karmaşık
kompleks projelerde bu işi çözmek için 3.parti araçlar kullanmak bile
gerekebiliyor.

Ben "esas olan onların yaptıklarıdır, ben zaten uydurdum" diyorum ve;

```bash
$ git checkout --theirs index.html
# yok bizimkini al: git checkout --ours index.html
$ cat index.html
```

ve;

```html
<!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title>Demo site</title>
        <link rel="stylesheet" href="public/css/application.css" type="text/css" />
    </head>
    <body>
        <header>
            <h1>Demo Site</h1>
        </header>
        
        <footer>Address information</footer>
        <script src="public/js/global.js"></script>
    </body>
</html>
```

`checkout` sadece branch’ler arası geçiş dışında da başka fonksiyonları olan
bir komut. `git reset` konusunda değineceğim ama hızlıca; 
`git checkout -- DOSYA` aslında `git status` komutundan aşina olduğumuz bir şey:

    Changes not staged for commit:
      (use "git checkout -- <file>..." to discard changes in working directory)

derki: *to discard changes in working directory* yani, çalıştığınız
yerde/dizinde/branch’de, yaptığınız değişiklikleri çöpe atmak için: 
`git checkout -- <file>...` kullanın!

Bu mini nottan sonra bari en azından **2017**’yi ekleyeyim:

```bash
$ git add index.html
$ git status

On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)
  
Changes to be committed:

	modified:   index.html
	modified:   public/css/application.css
```


Artık commit yapacak kıvama geldi:

```bash
$ git commit -m 'fixed: funny merge conflict'
Recorded resolution for 'index.html'.
[master d1d1d648b034] fixed: funny merge conflict
```

Dikkat ettiyseniz GIT hemen atladı ve bu çözümü öğrendiğini söyledi hemen. Log
ne alemde?

```bash
$ git log --graph --decorate --oneline --all

*   d1d1d648b034 (HEAD -> master) fixed: funny merge conflict
|\  
| * c5084b90ab6e (feature) Footer information added
* | 8f9bb3474c79 added: 2017 text to heading1 and some other fixes
|/  
* 60ee4fd58668 Demo site initiated
* fea8c5d8e385 [root] Initial commit
```

Nur topu gibi bir **merge bubble/commit** ile işimize devam ediyoruz. Hemen
master’daki güncellemeleri feature’a da alalım, işimiz henüz bitmedi:

```bash
$ git checkout feature
Switched to branch 'feature'

$ git merge master
Updating c5084b90ab6e..d1d1d648b034
Fast-forward
 index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Temiz bir **Fast-forward** oldu. Log ne durumda?

```bash
$ git log --graph --decorate --oneline --all

*   d1d1d648b034 (HEAD -> feature, master) fixed: funny merge conflict
|\  
| * c5084b90ab6e Footer information added
* | 8f9bb3474c79 added: 2017 text to heading1 and some other fixes
|/  
* 60ee4fd58668 Demo site initiated
* fea8c5d8e385 [root] Initial commit
```

Bulunduğumuz yer yani `HEAD`, hem **master**’ı hem de **feature**’ı işaret
ediyor. History’nin (*yani log’un*) temiz olması için bize ne lazım ?
