[![Documentation Status](https://readthedocs.org/projects/git-puf-noktalar/badge/?version=latest)](https://git-puf-noktalar.readthedocs.io/tr/latest/?badge=latest)

# GIT Püf Noktaları

https://vigo.github.io/git-puf-noktalari/

<a target="_blank" href="https://www.patreon.com/vigoo"><img src="https://c5.patreon.com/external/logo/become_a_patron_button@2x.png" width="160"></a>

Dağıtık çalışan revizyon kontrol sistemi `git`’i herkes için anlatmaya
çalıştığım açık-kaynak kitabım.

Neticede ben yazar değilim. Yüksek ihtimalle çok sayıda imla ve yazım hatası
yapacağım. Yardım edip hataları düzeltmeme yardımcı olursanız sevinirim.

Biliyorum çok kızan olacak ama bu kitapta pek çok yerde yarı İngilizce yarı
Türkçe kelimeler olacak. Çevirebildiklerimi çevireceğim. Bazı durumlarda
çevirmek ve doğru anlamı bulmak zor oluyor. İdare edin :)

---

## Katkı Yapanlar (İmla Düzeltmeler)

İsimler alfabetik olarak sıraya göre dizilmiştir.

- [Anıl İyidoğan](https://github.com/aniliyidogan)
- [Ekrem Candemir](https://github.com/EkremC)
- [Kağan Utku Kılıçlı](https://github.com/kaganuk)
- [Mustafa Enes Güneruz](https://github.com/menesdev)
- [Pınar Tekir Doğan](https://github.com/pnrtkr)
- [Zafer Çelenk](https://github.com/zafer06)

---

## Katkı Yapın

1. `fork` (https://github.com/vigo/git-puf-noktalari/fork)
1. Yeni bir `branch` açın (`git checkout -b duzeltmeler`)
1. `commit` edin (`git commit -am 'imla hataları'`)
1. `branch`’inizi `push` edin (`git push origin duzeltmeler`)
1. ve **Pull Request** açın!

---

## Notlar

**19 Ağustos 2021**

- Bölüm 3,4,5 komple eksikmiş. Yeni farkettim
- `mkdocs` entegre ettim

---

## Lisans

Bu proje MIT lisansı kullanmaktadır.

Bu proje, işbirliği için güvenli ve davetkar bir alan olarak tasarlanmıştır ve
katkıda bulunanların [davranış kurallarına][coc] uymaları beklenir.

---

## Rakefile

```bash
$ rake -T

rake build   # Build docs
rake deploy  # Deploy to github
rake serve   # Run docs server
```

---

[coc]: https://github.com/vigo/git-puf-noktalari/blob/main/CODE_OF_CONDUCT.md
