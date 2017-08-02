# Crystal Programlama Dili

This is the documentation for the Crystal programming language.

Crsytal, aşağıdaki amaçlar doğrultusunda bir programlama dilidir:

* Ruby'ye yakın bir sözdizimine sahip olması (ancak Ruby ile uyumluluk bir amaç değildir).
* Statik tip kontrollü olması, fakat metot argümanlarının ya da değişkenlerin tiplerini belirlemek zorunda kalmadan.
* Crystal'in içinde bağlayıcılar yazarak C kodunun çağırılabilmesi.
* Basmakalıp kodlardan kaçınmak için derlenme zamanı ölçümü ve kod üretimine sahip olması.
* Verimli bir şekilde native koda derlenmesi.

## Dil Referansına Katkıda Bulunmak

Kendini yardımsever biri olarak mı görüyorsun? Eğer bug bulursan veya daha anlaşılır olması gerektiğini düşündüğün bölümler var ise bu dokümantasyona katkıda bulunmandan ötürü çok mutlu oluruz. Burada bulunan repoya pull request atabilirsin : https://github.com/crystal-lang/crystal-book

Çok teşekkür ederiz!

### Lokal Ortamda Sunmak ve Derlemek

```
$ git clone https://github.com/crystal-lang/crystal-book.git
$ cd crystal-book
$ npm install -g gitbook-cli@2.3.0
$ npm install
$ gitbook serve
Live reload server started on port: 35729
Press CTRL+C to quit ...

info: 8 plugins are installed
info: loading plugin "ga"... OK
...
Starting server ...
Serving book on http://localhost:4000

```

Html çıktısı _book dosyasının içinde olacak (bazı linkler eğer dosyaları lokalde açarsanız çalışmayabilir).

Bağımlılıkları global olarak yüklemekten kaçınmak için Docker ortamı da bulunmaktadır:

```
$ docker-compose up
...
gitbook_1  | Starting server ...
gitbook_1  | Serving book on http://localhost:4000
gitbook_1  | Restart after change in file node_modules/.bin
...
```

### Sayfa ekleme

Bir sayfa eklemek için, istediğiniz konuma bir markdown dosyası oluşturun. Örnek: `overview/hello_world.md` . Ardından belgeler için gezinme görevi gören `SUMMARY.md` dosyasına bir bağlantı ekleyin.
