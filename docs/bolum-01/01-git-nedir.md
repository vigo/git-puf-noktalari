# GIT Nedir?

Eğer komut satırından `man git` derseniz, karşınıza çıkacak olan man page’de:

    NAME
       git - the stupid content tracker

ifadesini görürsünüz. **the stupid content tracker** yani: aptal içerik
takipçisi. Biraz ilginç değil mi? Yazılım dünyasında Microsoft’undan Apple’ına
Google’ına kadar neredeyse 7’den 70’e kullandığımız bir araç var ve adı: aptal
içerik takipçisi...

GIT aslında, dağıtık çalışan sürüm kontrol sistemi (*DVCS*) ve kaynak kod
yönetim (*SCM*) aracıdır. DVCS: **D**istributed **V**ersion **C**ontrol
**S**ystem, SCM: **S**ource **C**ode **M**anagement anlamına gelir. Eşdeğer
diğer araçlardan öne çıkan farkları ise;

* Herhangi bir merkez sunucuya ihtiyaç duymadan, offline olarak çalışabilmesi
* Güvenilirlik, **commit**’lerin tekil olması [^1]
* Hızlı olması [^2]
* Az yer tutması
* Sıfır maliyetle **branching** (*dallanma*) yapabilmek ve **merge** etmek (*birleştirebilmek*)
* **Deployment** ve benzeri işler için de kullanılması.

Bu güzel tool, Linux’un çekirdeğini yazan [Linus Torvalds][4] tarafından
geliştirilmiş ve açık-kaynak şeklinde dağıtılmıştır. Tüm kaynak kod [GitHub][5]’da
durmaktadır. Bu kitabı yazdığım an itibariyle aktüel olan versiyon: **2.13.1**


[^1]: Mart 2017 itibariyle [biraz can sıkıcı bir durumla][1] karşılaştı GIT kullanıcıları.
[^2]: [Facebook][2] / [Google][3] ve benzeri ölçeklerde projelerde (*gigabyte’larca*) bazı işlemler çok yavaşlıyormuş.

[1]: https://github.com/blog/2338-sha-1-collision-detection-on-github-com
[2]: https://code.facebook.com/posts/218678814984400/scaling-mercurial-at-facebook/
[3]: http://www.primordia.com/blog/2010/01/23/why-google-uses-mercurial-over-git/
[4]: https://en.wikipedia.org/wiki/Linus_Torvalds
[5]: https://github.com/git/
