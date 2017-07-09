# Repository ya da Repo Nedir?

Revizyon kontrolü altındaki dizin bir Repository’dir. Sözlük anlamına
baktığınızda; *depo*, *dolap*, *kutu*, *kab* gibi karşılığı olduğunu
görürsünüz. Bence tam anlamıyla içinde dosyaların (*daha doğrusu kaynak
kodların*) bulunduğu bir depodur Repository.

Halk arasında kısaca **Repo** olarak kullanılır. Film sektöründe çalışan biri
için Repo tatil anlamına geldiği gibi finans / bankacılık sektöründe de
*gecelik repo* gibi faiz içerikli anlamları da bulunur.

Eğer bilgisayarınızda GIT kuruluysa;

    $ git --version
    $ git help

gibi komutların çalıştığını göreceksiniz. Eğer yukarıdaki komutlar
çalışmıyorsa, kullandığınız işletim sistemine göre; bu [link][1] yardımıyla
GIT’i indirebilir ve kurabilirsiniz.

GIT, içinde harika bir dokümantasyon ile geliyor. Kullanacağınız komut
hakkında bilgi almak çok kolay:

    $ git help commit
    $ git help status
    $ git help clone
    
    # git help KOMUT


Hızlıca repository oluşturmak için iki yöntem var; ilk yöntem, bir dizin
oluşturup, içine girip repoyu oluşturmak: `git init`

    $ mkdir proje
    $ cd proje/
    $ git init
    Initialized empty Git repository in /private/tmp/proje/.git/

GIT bize **boş bir repository** oluşturduğunu söyler. Diğer yöntem ise tek
satırda;

    $ git init proje
    Initialized empty Git repository in /private/tmp/proje/.git/

işi halletmektir. Örnekleri kendi bilgisayarımda `/tmp/` yani temporary /
geçici dizinde yapmaktayım. Bu bakımdan gördüğünüz `/private/tmp/proje/` gibi
dizinler sizi şaşırtmasın!

Tamam, repo oluştu. Peki sonra ? Bence en çok kullanılan komutlardan biri olan
`git status` ile tanışalım.

    $ git status
    
    On branch master
    
    Initial commit
    
    nothing to commit (create/copy files and use "git add" to track)

`git status` ile o anki durumu görüntülüyoruz. An itibariyle `master`
branch’deyiz, commit edecek hiçbir şey yok. Bu durumda karşımızda iki tane
yeni kavram var. `branch` ve `commit`.

[1]: https://git-scm.com/