# Repo’nun Durumu: `git status`

Bu noktaya kadar pek çok kez `git status` yaptık. Ek birkaç parametre ile
değişik çıktılar almak mümkün:

## `git status -s` ve `git status -sb`

**Short Status** yani kısaca durum bilgisi için kullanılır. `-b` bulunduğun
branch’i de göster anlamındadır:

```bash
$ git status -s

 M file1.txt
AM new-file-1.txt
A  new-file-2.txt
?? new-file-3.txt

$ git status -sb

## master
 M file1.txt
AM new-file-1.txt
A  new-file-2.txt
?? new-file-3.txt
```

Bu tek harflerin bir anlamı var.

- ` ` = unmodified, boşluk karakteri, değiştirilmemiş
- `M` = modified, değişiklik var
- `A` = added, eklendi yani staged
- `D` = deleted, silindi
- `R` = renamed, dosya adı değişti
- `C` = copied, kopyalandı
- `U` = updated but unmerged, index güncellendi ama merge edilmedi

## `git status --ignored`

Eğer exclude edilmiş, yani tanımlanan dosyalar, dizinler, ya da dosya
türlerini GIT takibe almasın demişsek, varsa bu tür dosyalar, status içinde
bunları da göster demektir.

[Dosyaları nasıl takip dışında bırakırız?](bazi-dosyalari-takip-etmemek-gitignore.md)

## `git status --untracked-files`

Örnek projede, `git status` dediğimiz zaman;

```bash
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
  
	new file:   new-file-1.txt
	new file:   new-file-2.txt
    
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  
	modified:   file1.txt
	modified:   new-file-1.txt
    
Untracked files:
  (use "git add <file>..." to include in what will be committed)
  
	new-file-3.txt
	test-folder/
```

görüyoruz. Bizi ilgilendiren kısım **Untracked files:** kısmı yani henüz takip
altına alınmamış dosyalar. Bir dosya bir de dizin görüyorum. Acaba bu dizin
altında başka dosya var mı?

```bash
$ git status --untracked-files

On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   new-file-1.txt
	new file:   new-file-2.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   file1.txt
	modified:   new-file-1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	new-file-3.txt
	test-folder/test-file-a.txt
	test-folder/test-file-b.txt
	test-folder/test-file-c.txt
```

Tam üç tane dosya varmış!... 