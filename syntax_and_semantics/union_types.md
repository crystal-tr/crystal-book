# Birleşme(Union) tipleri

Bir değişkenin veya ifadenin tipi, birden fazla tipten oluşabilir. Buna bir birleşme tipi denir. Örneğin, farklı [if] (if.html) dallarında aynı değişkene atandığında:

```crystal
if 1 + 2 == 3
  a = 1
else
  a = "hello"
end

a # : Int32 | String
```

`if`'in sonunda, `a` nın `Int32 | String` tipi, "Int32 ve String'in birleşimini" okuyun. Bu birleşme tipi otomatik olarak derleyici tarafından oluşturulur. Çalışma zamanında, `a` tabii ki yalnızca bir tip olacaktır. Bu durum `class` methodunun çağırılmasıyla görülebilir:

```crystal
# The runtime type
a.class # => Int32
```

Derleme zamanı tipi, [typeof](typeof.html) kullanılarak görülebilir:

```crystal
# The compile-time type
typeof(a) # => Int32 | String
```

Bir birleşme, çok sayıda birleşik tipten oluşabilir. Tipi birleşik bir ifade üzerinde bir metod çağrılırken, birleşikteki tüm tipler metoda cevap vermelidir aksi takdirde derleme zamanı hatası verilir. Metot çağrısı tipi, bu metotların geri dönüş tiplerinin birleşim tipidir.

```crystal
# to_s is defined for Int32 and String, it returns String
a.to_s # => String

a + 1 # Error, because String#+(Int32) isn't defined
```

Eğer gerekliyse bir değişken derleme zamanında birleşme tipinde tanımlanabilir.

```
# set the compile-time type
a = 0.as(Int32|Nil|String)
typeof(a) # => Int32 | Nil | String
```

## Birleşme tipi kuralları

Genel bir durumda, ne zaman iki tür 'T1' ve 'T2' birleştiğinde, sonuç bir birleşim olur 'T1 | T2`. Bununla birlikte, ortaya çıkan türün farklı olduğu birkaç durum vardır.

### Aynı hiyerarşi altındaki sınıfların ve yapıların birliği

`T1` ve` T2` aynı hiyerarşinin altında ve en yakın ortak atası `Parent`,` Reference`, `Struct`,` Int`, `Float` ya da` Value` değilse, sonuç türü `Parent + `'dır. Buna sanal bir tür denir, bu da temelde derleyicinin tipini veya herhangi bir alt tipini  `Parent ` olarak göreceği anlamına gelir.

Örneğin:

```crystal
class Foo
end

class Bar < Foo
end

class Baz < Foo
end

bar = Bar.new
baz = Baz.new

# burada foo'nun tipi Bar | Baz olacak,
# çünkü Bar ve Baz'ın ikisi de Foo'dan miras alır
# sonuç tipi Foo+ olur.
foo = rand < 0.5 ? bar : baz
typeof(foo) # => Foo+
```

### Aynı boyuttaki tupleların birleşimi

Aynı boyuttaki iki tuple birleşimi, her konumda tiplerin birleşimini içeren bir tuple tipi ile sonuçlanır.

Örneğin:

```crystal
t1 = {1, "hi"}   # Tuple(Int32, String)
t2 = {true, nil} # Tuple(Bool, Nil)

t3 = rand < 0.5 ? t1 : t2
typeof(t3) # Tuple(Int32 | Bool, String | Nil)
```

### Aynı anahtarlı iki named tupleın birleşimi

Aynı anahtarlarla (sıralarına bakılmaksızın) iki adlandırılmış tuple birleşimi, her anahtar tipinin birleşimini içeren adlandırılmış bir tuple tipini verir. Anahtarların sırası, sol taraftaki tuple olan sırayla olacaktır.

Örneğin:

```crystal
t1 = {x: 1, y: "hi"}   # Tuple(x: Int32, y: String)
t2 = {y: true, x: nil} # Tuple(y: Bool, x: Nil)

t3 = rand < 0.5 ? t1 : t2
typeof(t3) # NamedTuple(x: Int32 | Nil, y: String | Bool)
```
