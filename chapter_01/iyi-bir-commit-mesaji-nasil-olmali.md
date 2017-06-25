## İyi Bir Commit Mesajı Nasıl Olmalı?

Bence temel kurallar;

1. İlk satırda (*50 karakteri geçmeden*) özet bilgi vermek
1. Detayları **bir boş satır bırakıp** alta yazmak
1. Mutlaka yapılan değişiklileri iyi izah etmek

Şu mesaj örneğine bakalım:

    Sitemizin yeni bölümü için index sayfası oluşturuldu.

    Yaptığımız projede, ABCD bölümü için yeni statik bir html sayfası
    gerekiyordu, bunun için index.html dosyasını oluşturdum ve
    front-end’i yazacak arkadaşlara gerekli bilgiyi verdim.

    Yeni bir paragraftaı aynı markdown kullanır gibi kullandım.

        - Bu şekilde list item yaptım,
        - Listeye devam ettim
    
    Bu konu ile ilgili ticket’lar:
    
    - http://example.com/ticket/1
    - http://example.com/ticket/2
    
    # Please enter the commit message for your changes. Lines starting
    # with '#' will be ignored, and an empty message aborts the commit.
    # On branch master
    #
    # Initial commit
    #
    # Changes to be committed:
    #   new file:   index.html
    #

Kısa log’a bakan kullanıcı;

    $ git log --oneline
    
    8833c9cfc Sitemizin yeni bölümü için index sayfası oluşturuldu.
    :
    :

şeklinde görecek. Gayet açıklayıcı olduğunu düşünüyorum. Detayları merak eden
olursa yukarıda yazan hikayeyi okuyabilir, hangi issue/ticket ile alakalı
olduğunu görebilir.

Mesajı içinde `#` ile başlayan satırlar yorum satırlarıdır. Mesaja dahil
olmazlar. `git commit` dedikten sonra, gelen ekranda hiçbir şey yazmadan
çıkarsanız **commit yapmaktan vazgeçmiş** olursunuz:

    Aborting commit due to empty commit message.

mesajını alırsınız. Yani **boş mesaj** olamaz! (*Bazı özel durumlar dışında...*)
