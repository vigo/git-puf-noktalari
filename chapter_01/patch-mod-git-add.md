# Patch mod’da ekleme: `git add -p`

Belkide GIT’in yapılma sebeplerinden biri **Patching**. Linus Torvalds, Linux
kernel’i geliştiriken, diğer katkı yapan developerlar, yaptıklarını e-posta ile 
[patch formatında][1] yolluyorlarmış.

Bu e-postalarla mücadele etmek, gelenleri kontrol etmek, bir tür **review**
işleminden geçirmek vs çok zahmetli işler. GIT bu durum için özel bir seçeneğe
sahip.

    $ echo 'file information 1' > file-info-1.txt
    $ echo 'file information 2' > file-info-2.txt
    $ ls
    README.md
    file-info-1.txt
    file-info-2.txt
    file1.txt
    file2.txt
    
    $ git add .
    $ git status
    
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
      
    	new file:   file-info-1.txt
    	new file:   file-info-2.txt
        
    $ git commit -m 'added two info files for demo purposes'

Şimdi, `file-info-1.txt` dosyasına bir-kaç satır ekleyelim:

    $ echo 'added new line' >> file-info-1.txt
    $ echo 'added one more new line' >> file-info-1.txt
    $ git status
    
    On branch master
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)
      
    	modified:   file-info-1.txt
        
    no changes added to commit (use "git add" and/or "git commit -a")

Şimdi patch mode’a geçelim:

    $ git add -p
    
    diff --git a/file-info-1.txt b/file-info-1.txt
    index 833822e8a04b..a333d502478e 100644
    --- a/file-info-1.txt
    +++ b/file-info-1.txt
    @@ -1 +1,3 @@
     file information 1
    +added new line
    +added one more new line
    Stage this hunk [y,n,q,a,d,/,e,?]?

GIT, bildiği son hali ile yeni değişikliği arasını bize `diff` ile gösteriyor
ve soruyor. Bu **hunk**’ı yani parçayı ne yapayım?

* `y` : YES, bu hunk’ı al.
* `n` : NO, bu hunk’ı alma.
* `q` : QUIT, hiçbir şey yapmadan çık ve devam etme.
* `a` : ALL, bu hunk dahil, dosyadaki diğer tüm hunk’ları al.
* `d` : DON’T, bu hunk dahil, diğer tüm hunk’ları alma.
* `/` : SEARCH, girilecek REGEX paternine göre hunk ara.
* `e` : EDIT, elle hunk’ı düzenle.
* `?` : HELP, yardım için.

Ben `a` yapıyorum ve `git status`:

    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
      
    	modified:   file-info-1.txt

Bu yöntem kodu tekrar gözden geçirme imkanı verdiği gibi, son dakikada
birşeyleri düzeltme değiştirme şansı da veriyor.

Bu patch modu aslında çaktırmadan `git add -i` yapıyor ve direk olarak oradaki
patch seçeneğini açıyor. Daha fazla bilgi almak için `git help add` demek
mümkün.


[1]: https://en.wikipedia.org/wiki/Patch_(Unix)