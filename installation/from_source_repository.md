# Kaynak kod üzerinden

Katkıda bulunmak istiyorsanız, Crystal'i kaynak kod üzerinden yüklemek isteyebilirsiniz.

1. [En son Crystal sürümünü yükleyin](https://crystal-lang.org/docs/installation). Crystal'i derlemek için, Crystal'e ihtiyacınız olacak :).

2. Desteklenen bir LLVM sürümünün o dizinde bulunduğundan emin olun. Şu anda, Crystal LLVM 3.8, 3.9 and 4.0 destekliyor. Mümkün olduğunca en son sürümü kullanın. Eğer Mac ve Homebrew formülünü kullanıyorsanız, Crystal'i kurarken --with-llvm` flagını eklerseniz, sizin için otomatik olarak yapılandırılmış gelecektir.

3. [Gerekli tüm kütüphaneleri](https://github.com/crystal-lang/crystal/wiki/All-required-libraries) yüklemiş olduğunuzdan emin olun. Ayrıca [katkıda bulunma kılavuzunu](https://github.com/crystal-lang/crystal/blob/master/CONTRIBUTING.md) okumak isteyebilirsiniz.

4. Repoyu klonlayın:

```
git clone https://github.com/crystal-lang/crystal.git
```

5. Derleyiciyi kendi versiyonunuzda build etmek için `make` komutunu çalıştırın.
6. Tümünü doğru yüklediğinizden ve bütün speclerin geçtiğinden emin olmak için `make spec` komutunu çalıştırın.
7. Crystal dosyalarınızı çalıştırmak için `bin/crystal`'i kullanın

Yeni `bin/crystal` hakkında daha fazla bilgi edinmek isterseniz, [derleyiciyi kullanmak](https://crystal-lang.org/docs/using_the_compiler/) dokümantasyonuna göz atın.

Not: Asıl binary `.build/crystal` içine kurulmuştur, ancak `bin/crystal` wrapper betiği Crystal'i çalıştırmak için kullanmanız gereken şeydir.
