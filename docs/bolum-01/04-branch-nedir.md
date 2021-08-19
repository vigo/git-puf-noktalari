# Branch Nedir?

İstediğiniz bir anda, elinizdeki koddan hızlıca bir ya da **N tane** kopya
çıkartma işlemidir. Yerel bir operasyondur. Yani yaptığınız her **branch**,
siz paylaşmadıkça sadece sizde bulunur.

Daha teknik bir anlatımla **branch** aslında içinde `commit-id` yazan bir
işaretçiden başka bir şey değildir.

`git`, sıfır bir repository oluşturulduğunda, aksi belirtilmedikçe, varsayılan
(*default*) branch olarak **main** branch’i oluşturur. Eskiden bu default
olarak `master`’dı.

```bash
$ git init proje
Initialized empty Git repository in /private/tmp/proje/.git/

$ cd proje/
$ git status
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

şu an **main** branch’deyiz (*eskiden master’dı*) ve commit edecek hiçbir şey
yok...
