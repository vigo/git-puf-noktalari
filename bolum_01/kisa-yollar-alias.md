# Kısa Yollar: alias

Günlük hayatta sık kullandığımız komutlar için kısa yollar oluşturabiliriz.
Buna `alias` deniyor. Örneğin;

    git status

çok kullanacağımız bir işlem olacak. Bu bakımdan her seferinde `git status`
yazmak yerine `git st` ya da `git s` gibi `alias` tanıtmak mümkün. Aynı diğer
konfigürasyon elementleri gibi:

    git config --global alias.st status

ya da `~/.gitconfig` dosyanızı açıp:

    [alias]
        st = status

gibi düzenleme yapabilirsiniz. Eğer alias’ın başında `!` işareti olursa bu
**shell komut**u çalıştırabileceğimiz anlamına gelir. Örneğin takip altında
olmayan dosyaları otomatik olarak takibe almak için komut satırından şu
işlemler serisini yapabiliriz:

    git status -s
    
    # iki tane yeni takip altında olmayan dosya olduğunu düşününelim, çıktısı
    # aşağıdaki gibi olsa;
    
     M index.html
    ?? test.jpg
    ?? global.js

`M` modified anlamında yani daha önce kontrol altına alınmış, `??` ise 
un-tracked anlamında, yani yeni dosya, hiçbir revizyon bilgisi yok. Şimdi;

    git status -s | grep -e "^??"
    
    # sonuç
    
    ?? test.jpg
    ?? global.js
    
    git status -s | grep -e "^??" | awk '{ print $2 }'
    
    # sonuç
    test.jpg
    global.js

ve mini Bash Script Crash-Course finalinde;

    git status -s | grep -e "^??" | awk '{ print $2 }' | xargs git add

yaparak sadece un-tracked olanları ekledik. Gördüğünüz gibi yaklaşık 4 komutu
zincirleme çağırdık. Bunu kolay yoldan yapmak için `alias` olarak ekleyebiliriz:

    git config --global alias.add-untracked '!git status -sb | grep -e "^??" | awk "{ print \$2 }" | xargs git add'

Bu işlemden sonra `git add-untracked` dediğimizde, yeni oluşan, revizyon
kontrol altında olmayan dosyalar otomatik olarak eklenecektir. Diğer örnek
kısa yollar için [Örnek Konfigürasyon Dosyası](bolum_01/ornek-konfigurasyon-dosyasi.md) incelenebilir.
