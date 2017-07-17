# Branch Nedir?

İstediğiniz bir anda, elinizdeki kod’dan hızlıca bir ya da N tane kopya
çıkartma işlemidir. Yerel operasyondur. Yani yaptığınız her branch, siz
paylaşmadıkça sadece sizde bulunur.

Daha teknik bir anlatımla branch aslında içinde commit-id yazan bir
işaretçiden başka bir şey değildir.

GIT, sıfır bir repository oluşturulduğunda, aksi belirtilmedikçe, varsayılan
(*default*) branch olarak **master** branch’i oluşturur:

[Repository ya da Repo nedir?](repository-nedir.md) bölümündeki örneği
hatırlayalım:

    $ git init proje
    Initialized empty Git repository in /private/tmp/proje/.git/
    
    $ git status
    
    On branch master
    
    Initial commit
    
    nothing to commit (create/copy files and use "git add" to track)

şu an **master** branch’deyiz ve commit edecek hiçbir şey yok...
