# GIT Püf Noktaları

Revizyon kontrol sistemi olarak son yıllara damgasını vurmuş bir araç GIT.
Bu kitapta gündelik geliştirme rutinlerinde sıkça karşınıza çıkabilecek
konulara değineceğim.

Ek olarak, zaman içinde topladığım, notlarımdan derlediğim püf noktalarını da
paylaşacağım.


## [Bölüm 01](bolum-01/)

* [GIT Nedir?](bolum-01/git-nedir.md)
* [GIT’in Hikayesi](bolum-01/gitin-kisa-hikayesi.md)
* [Repository Nedir?](bolum-01/repository-nedir.md)
* [Branch Nedir?](bolum-01/branch-nedir.md)
* [Konfigürasyon Nedir?](bolum-01/konfigurasyon-nedir.md)
* [Konfigürasyon İşlemleri](bolum-01/konfigurasyon-islemleri.md)
* [Konfigürasyon Dosyası](bolum-01/konfigurasyon-dosyasi.md)
* [Temel Konfigürasyon Öğeleri](bolum-01/temel-konfigurasyon-ogeleri.md)
* [Örnek Konfigürasyon Dosyası](bolum-01/ornek-konfigurasyon-dosyasi.md)
* [Kısa Yollar: `git alias`](bolum-01/kisa-yollar-alias.md)
* [Commit Nedir?](bolum-01/commit-nedir.md)
* [İlk Commit](bolum-01/ilk-commit.md)
* [Commit Mesajı Nedir?](bolum-01/commit-mesaji-nedir.md)
* [İyi Bir Commit Mesajı Nasıl Olmalı?](bolum-01/iyi-bir-commit-mesaji-nasil-olmali.md)
* [Basit Kullanım Örneği](bolum-01/basit-kullanim-ornegi.md)
* [Üç Aşamalı Dosya Sistemi](bolum-01/uc-asamali-dosya-sistemi.md)
* [İnteraktif Ekleme: `git add -i`](bolum-01/interaktif-git-add.md)
* [Patch Mode’da Ekleme: `git add -p`](bolum-01/patch-mod-git-add.md)
* [Repo’nun Durumu: `git status`](bolum-01/reponun-durumu-git-status.md)
* [Log’a Bakış](bolum-01/git-log.md)
* [Bazı Dosyaları Takip Etmemek: `.gitignore`](bolum-01/bazi-dosyalari-takip-etmemek-gitignore.md)
* [Dosya Silmek, Değiştirmek](bolum-01/dosya-silmek-degistirmek.md)

## [Bölüm 02](bolum-02/)

* [Branch’lerle Çalışmak](bolum-02/branch-ler-ile-calismak.md)
* [Branch’leri Birleştirmek](bolum-02/branch-leri-birlestirmek.md)
* [Branch’lerin Çakışması: Conflict](bolum-02/branch-lerin-cakismasi-conflict.md)
* [Branch’leri Birleştirmek: `rebasing`](bolum-02/branch-leri-birlestirmek-rebasing.md)
* [Branch Rebase Sırasında Çakışma: **Rebase Conflict**](bolum-02/branch-rebase-sirasinda-conflict.md)
* [Değişiklikleri Görüntülemek: `git diff`](bolum-02/degisiklikleri-goruntulemek-git-diff.md)
* [Etiketlemek Nedir?: `git tag`](bolum-02/etiketlemek-nedir-git-tag.md)

## [Bölüm 03](bolum-03/)

* [Commit’leri Birleştirmek: **Interactive Rebasing**](bolum-03/commit-leri-birlestirmek-interactive-rebasing.md)
* [Commit’leri Bölmek](bolum-03/commit-leri-bolmek.md)
* [Cımbızla Commit’i Almak: **Cherry Picking**](bolum-03/cimbizla-commit-i-almak-cherry-picking.md)
* [Hataları İşlemleri Geri Almak ya da Vazgeçmek: `reset revert amend`](bolum-03/hatalari-islemleri-geri-almak-ya-da-vazgecmek.md)
* [Commit’e Not Eklemek](bolum-03/commit-notu.md)
* [Her şey Kayıt Altında! En az 90 gün: `git reflog`](bolum-03/hersey-kayit-altinda-git-reflog.md)

## [Bölüm 04](bolum-04/)

* [Remote Kavramı Nedir? Remote’larla Çalışmak](bolum-04/remote-nedir.md)
* [Kendi GIT Reponuzu Yapın!](bolum-04/kendi-git-reponuzu-yapin.md)
* [GitHub, BitBucket ve GitLab ile Çalışmak](bolum-04/cloud-git-sunucu-platformları.md)
* [Repo içinde Repo: `git submodule`](bolum-04/repo-icinde-repo-git-submodule.md)

## [Bölüm 05](bolum-05/)

* [Commit Öncesi ya da Sonrası Otomasyonu: **GIT Hook’ları**](bolum-05/git-hook-lari.md)
* [Bundle Nedir?](bolum-05/bundle-nedir.md)
* [Commit’inizi İmzalayın](bolum-05/git-gpg-ile-imza.md)
* [Revizyonları Sorgulamak](bolum-05/revizyonlari-sorgulamak.md)
* [Commit’leri Sorgulamak: `blame`](bolum-05/commit-leri-sorgulamak.md)
* [Bisect Nedir?](bolum-05/git-bisect-nedir.md)
* [Yardımcı Araçlar](bolum-05/git-araclari.md)
* [Faydalı İpuçları](bolum-05/faydali-ipculari.md)


---


## Hatırlatmalar

- Neticede ben yazar değilim. Yüksek ihtimal çok sayıda imla ve yazım hatası
  yapacağım. Bu kitap açık-kaynak olarak [GitHub][2]’da bulunuyor. Yardım edip
  hataları düzeltmeme yardımcı olursanız süper olur.
- Biliyorum çok kızan olacak ama bu kitapta pek çok yerde yarı İngilizce yarı
  Türkçe kelimeler olacak. Çevirebildiklerimi çevireceğim. Bazı durumlarda
  çevirmek ve doğru anlamı bulmak zor oluyor. İdare edin :)
- [Kitabı online olarak okumak için tıklayın][1].

[1]: http://vigo.gitbooks.io/git-puf-noktalari/
[2]: https://github.com/vigo/git-puf-noktalari
