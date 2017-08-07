# Local değişkenler

Lokal değişkenler küçük harfle başlar ve kendilerine bir değerin atamasının yapıldığı zaman tanımlanmış olurlar.

```crystal
name = "Crystal"
age = 1
```

Tipleri, yalnızca başlatıcılarından(initializer) değil, kullanımlarından da çıkartılır. Genellikle, programcının beklediği tipte, programdaki konumlarına ve kullanımlarına göre değer tutuculardır.

Örneğin, bir değişkeni farklı bir ifade ile yeniden atamak, o ifadenin tipine sahip bir şekilde oluşturur:

```crystal
flower = "Tulip"
# burada 'flower' String

flower = 1
# burada ise 'flower' Int32
```

Bir değişken adının başında alt çizgi izni verilir, ancak bu adlar derleyici için ayrılmıştır, bu nedenle bunların kullanılması önerilmez (ve kodun daha okunaksız olmasına yol açar).
