# İlk Commit

Dedik ya, zamanın, o anın fotoğrafını çekiyoruz... Fotoğrafı çekebilmek için
repomuzda dosyaların olması gerekiyor. Ben, yeni bir projeye başladığım zaman,
ilk yaptığım commit’i **boş commit** olarak yapıyorum.

Reponun ilk commit’i aslında root-commit olup hiçbir parent commit’e sahip
değildi. Madem öyle, hiçbir dosya ile de ilişkilendirmek istemiyorum:

```bash
$ cd /tmp/
$ git init my-awesome-tool && cd $_
$ git commit --allow-empty -m '[root] Initial commit'
[master (root-commit) 2a88b16f848c] [root] Initial commit

$ git log --oneline
* 2a88b16f848c (HEAD -> master) [root] Initial commit
```

Commit mesajlarını **İngilizce** yazacağım. Elimizi buna alıştırmamız lazım. Hep
açık-kaynak projelerde çalışırken ya da ekibe Türkçe bilmeyen biri dahil
olduğunda ya da size yabancı bir ekiple / projeyle çalıştığınızda sıkıntı
çekmemeniz için iyi bir antrenman olur :)
