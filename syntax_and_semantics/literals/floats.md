# Float'lar

[Float32](http://crystal-lang.org/api/Float32.html) ve [Float64](http://crystal-lang.org/api/Float64.html) olmak üzere iki floating point(kayan noktalı sayı) tip vardır. Bunlar sırasıyla IEEE tarafından tanımlanmış [binary32](http://en.wikipedia.org/wiki/Single_precision_floating-point_format)
ve [binary64](http://en.wikipedia.org/wiki/Double_precision_floating-point_format)'e denk gelir

Bir floating point literali opsiyonel olarak `+` veya `-` işareti ile bunun ardından sayılar veya altçizgilerden oluşan bir dizi, ardından nokta, ardından sayılar veya altçizgiler, ardından opsiyonel üstel sonek ve ardından opsiyonel tip sonekinden oluşabilir. Eğer herhangi bir son ek bulunmuyorsa, bu literalin tipi `Float64`'tür.

```crystal
1.0      # Float64
1.0_f32  # Float32
1_f32    # Float32

1e10     # Float64
1.5e10   # Float64
1.5e-7   # Float64

+1.3     # Float64
-0.5     # Float64
```

Sonekten önce altçizgi `_` opsiyoneldir.

Bazı sayıları daha okunabilir hale getirmek için alt çizgiler kullanılabilir:

```crystal
1_000_000.111_111 # a lot more readable than 1000000.111111, yet functionally the same
```
