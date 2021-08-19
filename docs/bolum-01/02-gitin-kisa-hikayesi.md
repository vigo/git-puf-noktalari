# GIT’in Hikayesi

[Linus Torvalds][0], 2002 yılında, kernel’i geliştirirken [BitKeeper][1] adlı
revizyon kontrol sistemini kullanıyor. 2005 yılında Linux kernel geliştirici
topluluğu ile **BitKeeper** arasında bir sıkıntı oluyor. BitKeeper’ın ücretsiz
kullanım lisansı iptal oluyor ve [Linus’un sigorta bu noktada atıyor][2].

İzlediğim [Git Under the Hood][3] eğitiminde **Jeffrey Haemer**, Linus’un
GIT’i geliştirmeye bir pazartesi başlayıp, çarşamba gününden itibaren GIT’i
GIT ile versiyonlamaya başladığını söyledi. Bu kadar hızlı geliştirmesinin
sebebi olarak da zaten çok iyi bildiği kernel’i kopyalaması olduğunu söyledi.

Hatta [Ken Thompson][4]’ın da Unix’i **tam 1 ay**da yazdığını, Linus’un da
Unix’i örnek aldığını söyledi...

**Sonuç Olarak...**

Neticede GIT aslında bir **veritabanı**dır. Tanımlandığı dizin altında
çalışan, ilgili bilgilerini, ayarlarını ve benzeri bilgilerini `.git/` dizini
altında tutan, o dizindeki tüm dosyaların (*eğer izole edilmemişse*)
versiyonlarını yani dosyalardaki değişikliklerin tarihçesini, bu kendi şahsına
özel veritabanı mekanizması içinde saklar.

[0]: https://en.wikipedia.org/wiki/Linus_Torvalds
[1]: http://www.bitkeeper.com/
[2]: https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git
[3]: https://www.safaribooksonline.com/library/view/git-under-the/9780134133928/
[4]: https://en.wikipedia.org/wiki/Ken_Thompson
