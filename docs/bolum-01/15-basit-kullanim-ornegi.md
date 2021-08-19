# Basit Kullanım Örneği

GIT **146**’dan fazla komut içermektedir. Bunların bazıları günde sadece 1-2
kere, bazıları 40-50 kere, bazıları da ayda-yılda belki 1 kere kullanacağınız
komutlar olacaktır. Eğer;

    git help everyday

derseniz, karşınıza bir geliştiricinin ortalama kullanacağı komutları, nasıl
kullanacağı bilgisini ve günlük rutin işlerinizde size yardımcı olabilecek
çalışma yöntemlerini gösteren harika bir yardım sayfası gelir.

Kabaca bakıldığında;

1. `git init`
1. `git log`
1. `git status`
1. `git checkout`
1. `git add`
1. `git reset`
1. `git commit`
1. `git pull`
1. `git push`

en sık kullanacağınız komutlardan olacaktır. Hemen sıfırdan yeni bir repo
oluşturalım:

```bash
$ cd /tmp/
$ git init git-basics && cd $_
Initialized empty Git repository in /private/tmp/git-basics/.git/

$ git commit --allow-empty -m'[root] Initial commit'
[master (root-commit) 7639a730f5c7] [root] Initial commit
```

Şimdi içine bir dosya atalım ve reponun durumuna bakalım: `git status`

```bash
$ touch README.md
$ git status

On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
  
	README.md
    
nothing added to commit but untracked files present (use "git add" to track)
```


Takip dışında dosyalar var! (*Untracked files*) Eğer bu dosyaları takip altına
almak isterseniz: `git add <file>` yapın... Peki yapalım: `git add`

```bash
$ git add README.md
$ git status

On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
  
	new file:   README.md
```


GIT, yeni bir dosya takip etmeye başladığını anladı. Çünkü biz `git add` ile
emir verdik GIT’e. Dikkat ettiyseniz şöyle bir uyarı var:

    (use "git reset HEAD <file>..." to unstage)

`git add README.md` dediğimiz anda, `README.md` dosyasını **STAGING AREA**
yani sahneye almış olduk. Sahneye alınan her dosya commit edilebilir hale
gelir. Bu dosyanın içeriği GIT’in **index** mekanizmasına eklenmiştir. Bu
işlem **STAGING** olarak da bilinir.

Eğer henüz bu dosyayı takibe almak istemiyor ya da değişikliği geri almak
istiyorsanız `git reset HEAD README.md` yapıp sahneden aşağı indirmeniz yani
**UNSTAGE** etmeniz gerekir.

Bu noktada iki yeni kavram çıkar karşımıza. `HEAD` ve `git reset`.

## HEAD

`HEAD` aslında bir kısayol yani alias’dır. Bulunduğunuz branch’deki en yeni /
en son commit’i işaret eder.

---

Şimdi örneğe dönüp hiçbir commit yapmadan `git log --oneline` dersek:

```bash
$ git log --oneline
* 7639a730f5c7 (HEAD -> master) [root] Initial commit
```

`HEAD`’in **master** branch’de commit id’si **7639a730f5c7** olanı işaret
ettiğini görürsünüz. Haydi yeni bir şey daha...

## COMMIT ID

GIT, mutlaka her commit’e dünyada eşi benzeri olmayan bir **ID** verir.
Aslında **7639a730f5c7** diye gördüğümüz şey; **7639a730f5c7979ca8a5ecaed3731e0e360f280a**
sayısının ilk 12 karakteridir. Bu kısa haline **Short-SHA1** (*Kısa SHA1*) 
denir. Kısa SHA1’in uzun halini bulmak için;

```bash
$ git rev-parse 7639a730f5c7 # 12 karater
$ git rev-parse 7639a7       # 6 karakter
```

yapmak yeterlidir. Uzun SHA1’in ilk 6 ya da 7 karakteri de iş görür... COMMIT
ID aynı zamanda o anı ifade ettiği için ilgili revizyonu da ifade eder.

Her commit’in tekil olması zorunluluğu, GIT’in dağıtık çalışması için
zorunludur. Bir takımda **N tane kişi** aynı dosyalarla çalışacak ve hepsinde
projenin bir kopyası olacak. 

Keza hiçbiri de internete bağlı olma zorunluluğu olmadan çalışacak. Bu
bakımdan her yapılan commit’in **başka commit’lerle karışmaması** ve unique olması
gerekiyor. 

İşte GIT’in en ayrıştırıcı özelliği de bu.

---

Tekrar örneğe dönelim. GIT bize bilgi verdi ya, eğer istersek `git reset`
yaparız. İleriki bölümlerde daha detaylı değineceğim ama şimdi yeri gelmişken
hızlıca açıklamaya çalışayım. `git reset REVİZYON DOSYA` kullanım
şekillerinden biridir. `HEAD` neyi işaret ediyordu? **7639a730f5c7** numaralı
commit’i. Bu revizyonda `README.md` diye bir dosya var mıydı?

```bash
$ git reset HEAD README.md
$ git status

On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
  
	README.md
    
nothing added to commit but untracked files present (use "git add" to track)
```

Hayır, takip altında böyle bir dosya yoktu. Tekrar başladığımız yere döndük...
Şimdi tekrar ekleme işini yapalım ve ardından da ilk commit’i yapalım:

```bash
$ git add README.md
$ git commit -m 'Added: readme file'

[master 6601df828690] Added: readme file
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
```

Commit başarıyla gerçekleşti. GIT yeni **unique** (*benzersiz*) bir ID verdi,
**6601df828690** ek olarak 1 dosyanın eklendiğini, dosya içinde metinsel
herhangi bir değişiklik olmadığını söyledi. `0 insertions(+), 0 deletions(-)`

Peki şimdi durum ne?

```bash
$ git status

On branch master
nothing to commit, working tree clean
```

**master** branch’deyiz, her şey yolunda!. `git add` kullanırken;

```bash
# git add <DOSYA>
$ git add README.md

# git add <DİZİN>
$ git add images/

# git add .
# bulunduğun dizindeki her şeyi
# . unix ifadesidir ve current working directory’i ifade eder.
$ git add .

# git add *.py
# foo.py import.py run.py gibi sonu .py ile biten dosyaları ekler
$ git add *.py

# git add test-*.txt
# test-foo1.txt test-foo2.txt test-hello-world.txt gibi
$ git add test-*.txt
```

yapmak mümkün. İşlem sırası olarak önce **add** sonra **commit** yaptık. Bu
süreci tek harekete indirmek mümkün:

```bash
$ git commit -a -m 'Added: all untracked files at once'
```


`commit -a` ile tüm **untracked** (*henüz takibe alınmamış*) olan dosya/dizin
ne varsa **staging**’e at diyoruz. `-m` de tabiki commit mesajı. Ben bu
yöntemi neredeyse hiç kullanmıyorum. Mutlaka ilgili dosyaları ekleyip daha
sonra commit ediyorum.
