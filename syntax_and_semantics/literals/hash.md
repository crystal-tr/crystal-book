# Hash

Bir [Hash] (http://crystal-lang.org/api/Hash.html), 'K' türündeki anahtarların bir eşlemesini 'V' türündeki değerlere dönüştürmeyi temsil eder. Genellikle bir hash literali ile oluşturulur:

```crystal
{1 => 2, 3 => 4}     # Hash(Int32, Int32)
{1 => 2, 'a' => 3}   # Hash(Int32 | Char, Int32)
```

Bir Hash, anahtarlar ve değerler için karışık türlere sahip olabilir, yani `K` /` V` birleşim türleri olacaktır. Bu türler, hash oluşturulduğunda veya `K` ve` V` 'belirtilerek veya karma bir harf kullanarak belirlenir. İkinci durumda, `K`, hash literal anahtarların birleşimine ayarlanır ve `V`, hash literal değerlerin birleşimine ayarlanır.

Boş bir hash oluştururken her zaman `K` ve` V`leri belirtmelisiniz:

```crystal
{} of Int32 => Int32 # Hash(Int32, Int32).new ile aynı
{}                   # sözdizimi hatası(syntax error)
```

## Hash benzeri tipler

Argümansız `new` metodu tanımlayıp, `[]=` metodu ile diğer tiplerle de özel bir hash literal sözdizimi, kullanabilirsiniz.

```crystal
MyType{"foo" => "bar"}
```

Eğer `MyType` jenerik değilse, yukarıdaki ifade aşağıdakine eşdeğerdir:

```crystal
tmp = MyType.new
tmp["foo"] = "bar"
tmp
```

Eğer `MyType` jenerik ise, yukarıdaki ifade aşağıdakine eşdeğerdir:

```crystal
tmp = MyType(typeof("foo"), typeof("bar")).new
tmp["foo"] = "bar"
tmp
```

Jenerik olması durumunda, argüman tipleri şu şekilde de belirtilebilir:

```crystal
MyType(String, String) {"foo" => "bar"}
```
