# İnteraktif ekleme: `git add -i`

Eğer `git add -i` derseniz, **Interactive Mode**’a geçersiniz. Bu durumda
karşınıza çeşitli seçenekler çıkar:

    $ touch file{1,2}.txt
    $ ls -al
    
    total 0
    drwxr-xr-x   6 vigo  wheel   204 Jun 25 19:48 .
    drwxrwxrwt  59 root  wheel  2006 Jun 25 19:39 ..
    drwxr-xr-x  14 vigo  wheel   476 Jun 25 19:48 .git
    -rw-r--r--   1 vigo  wheel     0 Jun 25 18:53 README.md
    -rw-r--r--   1 vigo  wheel     0 Jun 25 19:48 file1.txt
    -rw-r--r--   1 vigo  wheel     0 Jun 25 19:48 file2.txt
    
    $ git status
    
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
      
    	file1.txt
    	file2.txt
        
    nothing added to commit but untracked files present (use "git add" to track)
    
    $ git add -i
    
    *** Commands ***
      1: status	  2: update	  3: revert	  4: add untracked
      5: patch	  6: diff	  7: quit	  8: help
    What now> 

Evet, şimdi ne yapacağız? **4** yani takip dışındakileri ekleyelim.

      1: file1.txt
      2: file2.txt
    Add untracked>> 

Bu durumda ya `1,2` yazıp iki dosyayı da ekleyeceğiz ya da teker teker
ilerleyeceğiz. Ben `1,2` yazdım:

    * 1: file1.txt
    * 2: file2.txt
    Add untracked>>

`*` bunları işleme girdiğini belirtiyor. Tekrar `<ENTER>` yapıp ilerliyorum:

    Add untracked>> 
    added 2 paths
    
    *** Commands ***
      1: status	  2: update	  3: revert	  4: add untracked
      5: patch	  6: diff	  7: quit	  8: help
    What now>

İşim bitti, `7` ile çıkıyorum ve duruma bakıyorum: `git status`:

    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
      
    	new file:   file1.txt
    	new file:   file2.txt

Şimdi commit zamanı...

    $ git commit -m 'Both files are added via git add -i'
    [master bb965e45b9ca] Both files are added via git add -i
     2 files changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 file1.txt
     create mode 100644 file2.txt

İnteraktif modda, oldu ya son anda dosyayı eklemekten vazgeçtiniz;

    $ touch file3.txt && git add -i
    
    *** Commands ***
      1: status	  2: update	  3: revert	  4: add untracked
      5: patch	  6: diff	  7: quit	  8: help
    What now> 4
      1: file3.txt
    Add untracked>> 1
    * 1: file3.txt
    Add untracked>>

`-` ile çıkartabilirsiniz. `-1` ya da `-INDEKS_NO`.

    Add untracked>> -1
      1: file3.txt
    Add untracked>> <ENTER>
    Add untracked>>  
    No untracked files.

    *** Commands ***
      1: status	  2: update	  3: revert	  4: add untracked
      5: patch	  6: diff	  7: quit	  8: help
    What now> 7
    Bye.
