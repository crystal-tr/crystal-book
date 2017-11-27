# Array

Bir [Array](http://crystal-lang.org/api/Array.html) `T` tipinde elemanlar içeren jenerik bir tiptir. Genellikle array literali ile oluşturulur:

```crystal
[1, 2, 3]         # Array(Int32)
[1, "hello", 'x'] # Array(Int32 | String | Char)
```

Bir Array karışık tiplere sahip olabilir, yani `T`, bir tip birleşimi olacaktır; ancak bunlar, dizi oluşturulduğunda T belirterek veya bir array literali kullanarak belirlenir. İkinci durumda, T array literal elemanlarının birleşimine ayarlanır.

Boş bir array oluştururken her zaman T'yi belirtmemiz gerekir::

```crystal
[] of Int32 # Array(Int32).new ile aynı
[]          # sözdizimi hatası(syntax error)
```

## String Array'i

String arrayleri özel bir sözdizimi kullanılarak oluşturulabilir:

```crystal
%w(one two three) # ["one", "two", "three"]
```

## Symbol Array'i

Symbol arrayleri özel bir sözdizimi kullanılarak oluşturulabilir:

```crystal
%i(one two three) # [:one, :two, :three]
```

## Array benzeri tipler

Argüman almayan bir `new` metodu tanımlayıp, `<<` metodu ile diğer tiplerle de özel bir array literal sözdizimi, kullanabilirsiniz.

```crystal
MyType{1, 2, 3}
```

Eğer `MyType` jenerik değilse, yukarıdaki ifade aşağıdakine eşdeğerdir:

```crystal
tmp = MyType.new
tmp << 1
tmp << 2
tmp << 3
tmp
```

Eğer `MyType` jenerik ise, yukarıdaki ifade aşağıdakine eşdeğerdir:

```crystal
tmp = MyType(typeof(1, 2, 3)).new
tmp << 1
tmp << 2
tmp << 3
tmp
```

Jenerik olması durumunda, argüman tipleri şu şekilde de belirtilebilir:

```crystal
MyType(Int32 | String) {1, 2, "foo"}
```
