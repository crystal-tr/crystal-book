# Integer'lar

[Int8](http://crystal-lang.org/api/Int8.html), [Int16](http://crystal-lang.org/api/Int16.html), [Int32](http://crystal-lang.org/api/Int32.html) and [Int64](http://crystal-lang.org/api/Int64.html) olmak üzere dört işaretli tamsayı tipi var, sırasıyla 8, 16, 32 ve 64 bit şeklinde gösterilebilir.

4 tip işaretsiz tamsayı tipi var: [UInt8](http://crystal-lang.org/api/UInt8.html), [UInt16](http://crystal-lang.org/api/UInt16.html), [UInt32](http://crystal-lang.org/api/UInt32.html) ve [UInt64](http://crystal-lang.org/api/UInt64.html). 

Bir integer literali opsiyonel olarak `+` veya `-` işareti ile bunun ardından rakamlar veya altçizgilerden oluşan bir dizi, ardından opsiyonel olarak bir sonekten oluşabilir. Eğer bir sonek bulunmuyorsa, bu literalin tipi en az `Int32` ile sayının uyduğu aralıkta yani `Int64` ya da `UInt64` arasındadır:

```crystal
1      # Int32

1_i8   # Int8
1_i16  # Int16
1_i32  # Int32
1_i64  # Int64

1_u8   # UInt8
1_u16  # UInt16
1_u32  # UInt32
1_u64  # UInt64

+10    # Int32
-20    # Int32

2147483648          # Int64
9223372036854775808 # UInt64
```

Sonekten önce altçizgi `_` opsiyoneldir.

Bazı sayıları daha okunabilir hale getirmek için alt çizgiler kullanılabilir:

```crystal
1_000_000 # 1000000'den daha iyi
```

İkili(binary) sayılar `0b` ile başlar:

```crystal
0b1101 # == 13
```

Sekizli(octal) sayılar `0o` ile başlar:

```crystal
0o123 # == 83
```

Onaltılık(hexadecimal) sayılar `0x` ile başlar:

```crystal
0xFE012D # == 16646445
0xfe012d # == 16646445
```
