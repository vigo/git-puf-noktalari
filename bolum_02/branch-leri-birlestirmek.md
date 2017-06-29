# Branch’leri Birleştirmek: `git merge`

Önce değişiklikleri eklemek istediğimiz yani güncelleme yapmak istediğimiz
branch’e geçiyoruz. Sonra, içinde bulunduğumuz brach’e birleştirmek
istediğimiz branch’i `merge` komutu ile parametre olarak geçiyoruz.

Örnek repoda, **idea** branch’indeki değişiklikleri **master** branch’e
aktaracağız:

## Strateji: Fast-Forward

    $ git log --graph --decorate --oneline --all
    
    * 2546539c16e9 (idea) testing commit
    * b34155b6b819 added 2 test files
    * 1304ac22cd97 (HEAD -> master) Example commit
    * 258f67c2e2cd [root] Initial commit
    
    $ git checkout master # güncelleyeceğimiz branch’e geçtik
    $ git merge idea      # idea branch’indeki değişiklikleri master’a al
    
    Updating 1304ac22cd97..2546539c16e9
    Fast-forward
     testing-file-ab-1.sh | 0
     testing-file-ab-2.sh | 0
     2 files changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 testing-file-ab-1.sh
     create mode 100644 testing-file-ab-2.sh

Şimdi ne oldu ? Satır satır bakalım:

    Updating 1304ac22cd97..2546539c16e9

`1304ac22cd97` bulunduğumuz yerdi. `2546539c16e9` ise **idea** branch’inin
HEAD’iydi.

    Fast-forward

![Teyp - Kaset kayıt cihazı](branch-leri-birlestirmek/kaset-kayit.jpg "Kaset kayıt")

Kaset / teyp çalarları hatırlayan varsa, kaset-çalar’ın üzerinde `PLAY`,
`STOP`, `RECORD`, `PAUSE`, `REW`, `FF` gibi düğmeler vardı... Kaseti ileri
sarmak için bu `FF` yani **Fast Forward** düğmesine basardık.

İşte GIT’de aynen bu kaset kayıt cihazı gibi ileri sarma işi yaptı. Log’a
bakıldığında, linear (*doğrusal*) bir durum görünüyor. **idea** branch’inde
değişiklik olmasına rağmen master olduğu yerde kalmış. Yani master branch’de
hiçbir şey değişmediği için GIT:

> Hmmm... Bu merge işini yaparken sadece pointer’ın yerini değişerek operasyonu
tamamlayabilirim...

diye düşünüp birleştirme işlemini **Fast Forward stratejisi** kullanarak
yaptı. Gayet temiz bir operasyon oldu.

    2 files changed, 0 insertions(+), 0 deletions(-)

Zaten hangi dosyalar olduğunu da biliyorduk. Aynen tahmin ettiğimiz ve
istediğimiz gibi oldu herşey. Son durum nedir?

    $ git log --graph --decorate --oneline --all
    
    * 2546539c16e9 (HEAD -> master, idea) testing commit
    * b34155b6b819 added 2 test files
    * 1304ac22cd97 Example commit
    * 258f67c2e2cd [root] Initial commit

Hem **master** hem de **idea** branch’i aynı noktayı işaret ediyorlar.
Önerilen, benim de hep yaptığım şey şu; branch’i merge ettikten sonra, artık o
branch’le işimin kalmadığını düşünüyorum ve siliyorum:

    $ git branch -d idea
    Deleted branch idea (was 2546539c16e9).

    $ git branch -v
    * master 2546539c16e9 testing commit

## Strateji: Recursive

Şimdi master branch’den yeni bir branch oluşturalım:

    $ git checkout -b development           # branch’i oluşturup otomatik olarak checkout yaptık
    Switched to a new branch 'development'

Bir tane yeni dosya ekleyelim:

    $ touch global.js && git add global.js
    $ git commit -m 'main js file added'
    
    [development 7e3c5612484b] main js file added
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 global.js
     
    $ git log --graph --decorate --oneline --all
    
    * 7e3c5612484b (HEAD -> development) main js file added
    * 2546539c16e9 (master) testing commit
    * b34155b6b819 added 2 test files
    * 1304ac22cd97 Example commit
    * 258f67c2e2cd [root] Initial commit

Bu sırada aklımıza birşey geldi, hemen master branch’e dönüp o unuttuğumuz işi
yapalım:

    $ git checkout master
    Switched to branch 'master'
    
    $ touch server-{1,2}.rb && git add server-{1,2}.rb
    $ git commit -m 'server files added'
    
    [master e2fba879b0df] server files added
     2 files changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 server-1.rb
     create mode 100644 server-2.rb
     
     $ git log --graph --decorate --oneline --all
     
     * e2fba879b0df (HEAD -> master) server files added
     | * 7e3c5612484b (development) main js file added
     |/  
     * 2546539c16e9 testing commit
     * b34155b6b819 added 2 test files
     * 1304ac22cd97 Example commit
     * 258f67c2e2cd [root] Initial commit

İlk kez böyle dallı budaklı bir log ile karşı karşıyayız. `2546539c16e9`
numaralı commit’ten iki tane türeme olmuş. Bunlar;

1. `7e3c5612484b (development) main js file added`
1. `e2fba879b0df (HEAD -> master) server files added`

Yani `7e3c5612484b` ve `e2fba879b0df` komitlerinin atası: `2546539c16e9`

    $ git show --pretty=%h 7e3c5612484b^ # git help show
    2546539c16e9
    
    $ git show --pretty=%h e2fba879b0df^
    2546539c16e9

1. master branch’deki 2 dosya: `server-1.rb` ve `server-2.rb` development
branch’inde yok
1. development branch’indeki `global.js` de master branch’de yok

Biz ne yapmak istiyoruz ? development branch’deki değişiklikleri master
branch’e aktarmak... O zaman;

    $ git checkout master # master branch’e geçtik
    Switched to branch 'master'
    
    $ git merge development

İşte bu noktada karşımıza pat diye mesaj editörü çıktı ve ne görüyoruz?

    Merge branch 'development'

    # Please enter a commit message to explain why this merge is necessary,
    # especially if it merges an updated upstream into a topic branch.
    #
    # Lines starting with '#' will be ignored, and an empty message aborts
    # the commit.

Otomatik üretilmiş bir commit mesajından başka birşey değil bu! GIT bize;

> Lütfen bu birleştirmeyi açıklayan bir mesaj yaz!

diye uyarıda bulunuyor. Hiçbir şey yazmadan kaydedip çıkıyorum. Mini not: Eğer
`$EDITOR` environment variable ataması yapmadıysanız ya da [Temel
Konfigürasyon Öğeleri - core.editor][3] ayarı yapmadıysanız karşınıza `vi`
text editörü çıkacak. Bu durumda mesajı kaydedip çıkmak için: `:wq` yapmanız
gerekecek.

    Merge made by the 'recursive' strategy.
     global.js | 0
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 global.js
     
     $ git log --graph --decorate --oneline --all
     
     *   5424468beb69 (HEAD -> master) Merge branch 'development'
     |\  
     | * 7e3c5612484b (development) main js file added
     * | e2fba879b0df server files added
     |/  
     * 2546539c16e9 testing commit
     * b34155b6b819 added 2 test files
     * 1304ac22cd97 Example commit
     * 258f67c2e2cd [root] Initial commit

İşte **Recursive strateji** ile yapılan merge sonucunda nur topu gibi bir
**merge commit**’imiz oldu. Buna **merge bubble** da denir.

    5424468beb69 (HEAD -> master) Merge branch 'development'

Recursive olmasının ne sıkıntısı ya da faydası var ? Şöyle bakalım. Ne
demiştim? İşimiz bitince branch’i siliyoruz. Yani şimdi development branch’i
uçurup log’a tekrar bakalım:

    $ git branch -d development
    Deleted branch development (was 7e3c5612484b).
    
    $ git log --graph --decorate --oneline --all
    
    *   5424468beb69 (HEAD -> master) Merge branch 'development'
    |\  
    | * 7e3c5612484b main js file added
    * | e2fba879b0df server files added
    |/  
    * 2546539c16e9 testing commit
    * b34155b6b819 added 2 test files
    * 1304ac22cd97 Example commit
    * 258f67c2e2cd [root] Initial commit

Bu log’a baktığımızda, ilk anda `5424468beb69` numaralı commit’in bir merge
commit olduğunu, hatta bunun development branch’inden türediğini
görebiliyoruz. Bu kimileri için faydalı olabilir. Ben **linear history** yani
doğrusal, satır satır log görmeyi sevenlerdenim.

Peki hemen şu soru gelmeli:

> Peki benzer bir durumda, merge commit olmadan, linear history yapmak mümkün mü?

Aynı örnekteki gibi, master ve development branch’lerinde farklılıklar olacak
ve biz merge commit olmadan merge yapacağız? Evet mümkün... Buna **rebase**
işlemi deniliyor. Yaptığımız şey de **branch rebasing** oluyor. Bu konuya
geleceğiz.

GIT default olarak branch’leri merge ederken **Fast-Forward** stratejisini
deniyor ilk olarak. Eğer istersek bunu değiştirebiliriz. İster konfigürasyon
seviyesinde ister işlem seviyesinde.

Eğer default olarak branch’lerin merge işlemini Recursive strateji kullanarak
yapmasını isterseniz:

    $ git config --global merge.ff false

eğer işlem seviyesinde yapmasını isterseniz de:

    $ git checkout -b no-ff # demo amaçlı no-ff adında bir branch aç ve checkout yap
    Switched to a new branch 'no-ff'
    
    $ touch file-for-no-ff.txt && git add file-for-no-ff.txt
    $ git commit -m 'no-ff commit'
    [no-ff 8810d33ff41f] no-ff commit
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 file-for-no-ff.txt
    
    $ git checkout master
    $ git merge no-ff --no-ff
    Merge made by the 'recursive' strategy.
     file-for-no-ff.txt | 0
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 file-for-no-ff.txt
    
    $ git log --graph --decorate --oneline --all
    
    *   c83d33173bbe (HEAD -> master) Merge branch 'no-ff'
    |\  
    | * 8810d33ff41f (no-ff) no-ff commit
    |/  
    *   5424468beb69 Merge branch 'development'
    |\  
    | * 7e3c5612484b main js file added
    * | e2fba879b0df server files added
    |/  
    * 2546539c16e9 testing commit
    * b34155b6b819 added 2 test files
    * 1304ac22cd97 Example commit
    * 258f67c2e2cd [root] Initial commit

`--no-ff` ile otomatik olarak birleştirme sonunda merge commit
üretebilirsiniz. Hatta, önce ne olduğuna bakıp sonrasında kendiniz commit’i
manual olarak yapabilirsiniz:

    $ git checkout -b no-ff-no-commit
    $ touch file-for-no-ff-no-commit.txt && git add $_
    $ git commit -m 'commit for no-ff and no-commit demo'
    [no-ff-no-commit 4d32113f1100] commit for no-ff and no-commit demo
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 file-for-no-ff-no-commit.txt
     
    $ git checkout master 
    $ git merge no-ff-no-commit --no-ff --no-commit
    Automatic merge went well; stopped before committing as requested

`--no-commit` yüzünden merge işlemi tamamlandı ama merge commit yapılmadı.
Bunu biz yapacağız. Hatta bu noktada eğer gerekiyorsa başka dosyalar eklemek
çıkartmak da mümkün:

    $ git status
    
    On branch master
    All conflicts fixed but you are still merging.
      (use "git commit" to conclude merge)
      
    Changes to be committed:
    
    	new file:   file-for-no-ff-no-commit.txt

Haydi bitirelim bu işlemi:

    $ git commit -m 'this is manual merge commit. merged with branch: no-ff-no-commit'
    [master dc0c3779544f] this is manual merge commit. merged with branch: no-ff-no-commit
    
    $ git log --graph --decorate --oneline --all
    
    *   dc0c3779544f (HEAD -> master) this is manual merge commit. merged with branch: no-ff-no-commit
    |\  
    | * 4d32113f1100 (no-ff-no-commit) commit for no-ff and no-commit demo
    |/  
    *   c83d33173bbe Merge branch 'no-ff'
    |\  
    | * 8810d33ff41f (no-ff) no-ff commit
    |/  
    *   5424468beb69 Merge branch 'development'
    |\  
    | * 7e3c5612484b main js file added
    * | e2fba879b0df server files added
    |/  
    * 2546539c16e9 testing commit
    * b34155b6b819 added 2 test files
    * 1304ac22cd97 Example commit
    * 258f67c2e2cd [root] Initial commit

ASCII’den grafik çizer gibi... Dallar budaklar hepsi burada :)

---

[Teyp Fotoğrafı][1] &copy; [vicent.zp][2]

[1]: https://www.flickr.com/photos/44337451@N00/4381924568/sizes/l/
[2]: https://www.flickr.com/photos/44337451@N00/
[3]: ../bolum_01/temel-konfigurasyon-ogeleri.md#core-editor