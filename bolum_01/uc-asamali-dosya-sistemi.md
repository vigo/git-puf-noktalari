# Üç Aşamalı Dosya Sistemi

GIT ile çalışırken 3 aşamalı dosya sistemini hep aklımızda tutmalıyız:

1. Staged
2. Modified
3. Commited

## Staged

Bazı değişiklikler ya da eklemeler yaptın, sepete attın ama henüz GIT’e
bildirmedin! Yani sahneye aldın fakat öylece duruyor orada.

## Modified

Değişiklikler var, GIT bunun farkında ama henüz kaydetmedin yani commit
etmedin! Bu ne demek? Hemen bakalım:

    $ ls
    
    README.md
    file-info-1.txt
    file-info-2.txt
    file1.txt
    file2.txt

Şimdi `file-info-2.txt` üzerinde değişiklik yapalım.

    $ echo 'adding another great line' >> file-info-2.txt
    $ git status
    
    On branch master
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)
    	modified:   file-info-2.txt
    no changes added to commit (use "git add" and/or "git commit -a")

GIT, değişikliği anladı, bu dosyanın değiştiğini yani **modified** olduğunu
söylüyor. Değişikliği geri almak için `git checkout -- <file>` yapabiliriz.
Acaba `file-info-2.txt` içinde ne yazıyor?

    $ cat file-info-2.txt
    
    file information 2
    adding another great line

Hmmm... peki alalım geri:

    $ git checkout -- file-info-2.txt
    $ git status
    
    On branch master
    nothing to commit, working tree clean

Dosyanın içeriği?

    $ cat file-info-2.txt
    file information 2

Şimdi biraz daha değişik birşey deneyelim. Tekrar aynı işlemi yapalım ama küçük
bir farkla:

    $ echo 'adding another great line' >> file-info-2.txt
    $ git add file-info-2.txt
    $ echo 'adding another great line for the 3rd time' >> file-info-2.txt
    $ git status
    
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
      
    	modified:   file-info-2.txt
        
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)
      
    	modified:   file-info-2.txt

Durum şu; `file-info-2.txt` dosyası sanki 2 kere **modified** yani değişikliği
uğramış ama birinde **staged**, diğerinde ise **modified**. Evet aynen de
böyle oldu. Değişiklik yaptık ve `git add` ile staging’e aldık, commit
yapmadık ve tekrar değişiklik yaptık...

Tekrar ekleyelim ki bu ikinci değişiklik de kayıt altına alınsın:

    $ git add file-info-2.txt
    $ git status
    
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
      
    	modified:   file-info-2.txt


## Committed

Veri, yerel veritabanına güvenli olarak kaydedildi. Neticede GIT kendi
yerelinde, kendi anlayacağı şekilde bir veritabanı saklıyor. Şimdi yukarıda
yarım kalan işi bitirelim:

    $ git commit -m 'staged, modifed and commited example'
    
    [master 5fe19937b38f] staged, modifed and commited example
     1 file changed, 2 insertions(+)
    
    $ git log --oneline
    
    5fe19937b38f staged, modifed and commited example
    5579b829b6a8 file added via git add -p
    c52805a3c8f5 added two info files for demo purposes
    bb965e45b9ca Both files are added via git add -i
    6601df828690 Added: readme file
    7639a730f5c7 [root] Initial commit
