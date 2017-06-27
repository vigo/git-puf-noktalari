# Commit Mesajı nedir?

GIT’in resmi dokümantasyon sitesinde commit’in açıklamasını yaparken, mesaj
ile ilgili kısımda;

> ... with a log message from the user describing the changes.

der. Yani kullanıcının yaptığı değişiklikleri tarif ettiği, anlattığı kayıttır
bu aslında. Çünkü GIT değişiklikleri takip eden bir araçtır. Teknik olarak
GIT deşikliğin ne olduğunu biliyor ama sonuç olarak kodu yazan insan
olduğu için, insanın anlayacağı şekilde açıklamak gerekiyor nelerin değiştiğini.

En hızlı şekilde commit mesajı yazmak için günlük hayatta;

    git commit -m "MESAJ"

kullanırız. Bu aslında kısa mesaj kullanımıdır. Örneğin `git log --oneline`
kullanımında aldığımız çıktı:

    a58834812b45 (HEAD -> master, origin/master, origin/HEAD) Merge pull request #1295 from ninoseki/master
    875f36f963dd Change relative URLs to absolute URLS
    a1b0de7b45a7 Fixed broken links in rack-protection/README.md
    ec08e37bf8b4 Linkify protection docs
    ea1a21c0734e Update homepages for sinatra-contrib and rack-protection

gibidir. `COMMIT_ID` ve `COMMIT_MESSAGE` şeklinde görürüz. Bu kısa mesaj,
aslında commit mesajının ilk satırıdır ve bu ilk satır **50 karakter**dir.
ID’si a58834812b45 olan commit’e bakalım:

    git show a58834812b45
    
    Merge pull request #1295 from ninoseki/master
    
    Fixed broken links in rack-protection/README.md

İlk satırda kısa açıklama, bir satır boşluk ve mesajın devamı bulunur. Ben de
dahil olmak üzere, pek çok geliştirici, yaptığı değişiklikleri uzun uzun
yazmak yerine ışık hızıyla;

    git commit -m 'up'
    git commit -m 'update'
    git commit -m 'wip'

gibi, aslında kavgada bile yapılmayacak hareketleri yapmışızdır. Neden? kim
onca değişikliği oturup yazacak şimdi? İşte en azından bu durumları minimal
düzeye indirmek için tavsiye edilen ilk yöntem: `git commit` ile commit
yapmak, `git commit -m 'MESAJ'` kullanmamak!

Bu yöntemle karşımıza `git config core.editor` ile belirlenmiş text editörü
çıkar ve ferah ferah mesaj yazacak bir alanla karşı karşıya kalırız. Böyle bir 
durumda otomatikleştirilmiş 
[şablon mesaj](temel-konfigurasyon-ogeleri.md#commit-template) çok işimize 
yarayabilir.
