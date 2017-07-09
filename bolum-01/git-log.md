# Log’a Bakış

Üzerinden hassasiyetle durduğumuz **Commit Mesajı** konusu işte bu kısımda çok
önemli bir rol oynar çünkü o yazdığımız mesajlar, repomuzun tarihçesini
gösterir bize.

`git log` dediğimizde;

    commit 5579b829b6a801f8ebd7597db7e1a9fd43f28d49
    Author: Uğur Özyılmazel <ugurozyilmazel@gmail.com>
    Date:   Sun Jun 25 20:35:42 2017 +0300
    
        file added via git add -p
        
    commit c52805a3c8f5c78588e9b7fbc2e4f1b31675d5e2
    Author: Uğur Özyılmazel <ugurozyilmazel@gmail.com>
    Date:   Sun Jun 25 20:19:43 2017 +0300
    
        added two info files for demo purposes
        
    commit bb965e45b9ca8d60de77ff066f6f4eb6ea819c97
    Author: Uğur Özyılmazel <ugurozyilmazel@gmail.com>
    Date:   Sun Jun 25 19:55:24 2017 +0300
    
        Both files are added via git add -i
        
    commit 6601df8286905fee9942dfc5fe6a36b7e95f1e7e
    Author: Uğur Özyılmazel <ugurozyilmazel@gmail.com>
    Date:   Sun Jun 25 19:19:40 2017 +0300
    
        Added: readme file
        
    commit 7639a730f5c7979ca8a5ecaed3731e0e360f280a
    Author: Uğur Özyılmazel <ugurozyilmazel@gmail.com>
    Date:   Sun Jun 25 18:53:15 2017 +0300
    
        [root] Initial commit

gibi bir çıktı ile karşılaşırız. Burada, default olarak sondan başa doğru
sıralanmış bir şekilde, yapılan commit, yapan, yapılış tarihi ve mesajı
gibi meta bilgilerini görüntüleriz.

Alacağı farklı parametrelerle çok daha öz ve kolay anlaşılır bilgiler verir
bize `git log`:

    $ git log --oneline
    
    5579b829b6a8 file added via git add -p
    c52805a3c8f5 added two info files for demo purposes
    bb965e45b9ca Both files are added via git add -i
    6601df828690 Added: readme file
    7639a730f5c7 [root] Initial commit
    
    $ git log --oneline --stat
    
    5579b829b6a8 file added via git add -p
     file-info-1.txt | 2 ++
     1 file changed, 2 insertions(+)
    c52805a3c8f5 added two info files for demo purposes
     file-info-1.txt | 1 +
     file-info-2.txt | 1 +
     2 files changed, 2 insertions(+)
    bb965e45b9ca Both files are added via git add -i
     file1.txt | 0
     file2.txt | 0
     2 files changed, 0 insertions(+), 0 deletions(-)
    6601df828690 Added: readme file
     README.md | 0
     1 file changed, 0 insertions(+), 0 deletions(-)
    7639a730f5c7 [root] Initial commit

Benim bir alias’ım var. `lg` yani `git lg` olarak çağırıyorum:

    $ git log --graph --decorate --oneline --all # git lg
    
    * 5579b829b6a8 (HEAD -> master) file added via git add -p
    * c52805a3c8f5 added two info files for demo purposes
    * bb965e45b9ca Both files are added via git add -i
    * 6601df828690 Added: readme file
    * 7639a730f5c7 [root] Initial commit

Siz de yapabilirsiniz:

    $ git config --global alias.lg "log --graph --decorate --oneline --all"
    $ git help lg
    `git lg' is aliased to `log --graph --decorate --oneline --all'
