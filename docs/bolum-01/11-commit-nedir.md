# Commit Nedir?

GIT, kendi içinde özel bir [GRAPH][1] yapısı kullanıyor. Bunun adı: 
**Directed Acyclic Graph**. Bence biraz korkutucu :) Bu nedir diyen varsa 
detayları [linkten][2] öğrenebilir. Kabaca ortada bir ağaç yapısı var.
Ağacın kolları var, dalları var. Kendi özel yapısı içinde GIT değişiklikleri
kendi yöntemleriyle saklar.

Akla gelebilecek en basit yöntem *delta-diff* yani sadece değişen şeyleri
saklamak yerine GIT komple o anın fotoğrafını çeker. Bu aslında o an’ın
**snapshot**’ı dır ve GIT buna **Commit** der.

Commit yaptığınız zaman GIT, adı **commit-object** olan bir taşıyıcı saklar.
Bu taşıyıcı içinde **stage** edilmiş içerik, commit’i yapan kişi bilgileri,
varsa bağlı olduğu bir üst commit ya da **branch**’lerin **merge** edilmesi
(*birleştirilmesi*) sonunda oluşmuş bir commit ise birden fazla branch 
bilgisi saklar. Bunlar aslında birer işaretçi yani **pointer**’dır.

Commit, içinde hangi **tree** yapısına dahil olduğu bilgisini de saklar. İlk
commit dışındaki tüm commit’lerin bir **parent-commit**’i bulunur. Sıfır bir
repo içinde yapılan ilk commit aslında o repo’nun **root-commit**’idir. Hiçbir
commit’ten türememiştir.

Örnek bir log çıktısına bakalım:

```bash
$ git log --graph --decorate --oneline --all
* b72ce45cafdc (HEAD -> master) fixed grammar at license section
* 504714498c31 hooks folder deleted
* 49261317ef93 Release: v0.1.0
* c0672c7d5be6 Ready for v0.1.0
* 71ff5c9dfac2 Added installation feature.
* 9bf387240b22 Changed message storage file.
* 1e7071c6e6fe Ready to release. Need to finish README.
* c3fd828979bc added: README file
* b1d90b39ba10 [root] initial commit
```

Son yapılan commit: **b72ce45cafdc**. Bu commit’in parent’ı **504714498c31**
ve 504714498c31 commit’in parent’ı **49261317ef93**. Parent’ı olmayan tek
commit: **b1d90b39ba10**

Genelde şematik olarak gösterilirken;

                                     master
                                        |
    49261317ef93 <- 504714498c31 <- b72ce45cafdc (son commit)

zaman çizelgesi soldan-sağa akarken commit’lerin ilişkisi tam ters şekildedir.
Her zaman kim kimin üstü altı (*parent/child*) durumu önemlidir.

[1]: https://en.wikipedia.org/wiki/Directed_acyclic_graph
[2]: http://eagain.net/articles/git-for-computer-scientists/

