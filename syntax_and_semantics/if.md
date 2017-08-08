# if

Bir `if` koşulunun *doğruluk* olması durumunda kendisine ayrılan bölümü hesaplar. Aksi takdirde, eğer bulunuyorsa `else` bölümünü hesaplar.

```crystal
a = 1
if a > 0
  a = 10
end
a #=> 10

b = 1
if b > 2
  b = 10
else
  b = 20
end
b #=> 20
```

If-else-if bağı yazmak isterseniz `elsif` kullanabilirsiniz:

```crystal
if bir_koşul
  bir_şey_yap
elsif başka_bir_koşul
  başka_bir_şey_yap
else
  bunu_yap
end
```

`If` den sonra, bir değişkenin tipi, her iki bölümde de kullanılan ifadelerin tipine bağlıdır.

```crystal
a = 1
if bir_koşul
  a = "hello"
else
  a = true
end
# a : String | Bool

b = 1
if bir_koşul
  b = "hello"
end
# b : Int32 | String

if bir_koşul
  c = 1
else
  c = "hello"
end
# c : Int32 | String

if bir_koşul
  d = 1
end
# d : Int32 | Nil
```

Unutmayın ki, eğer bir değişken bu bölümlerin birinde tanımlanır ve diğerinde tanımlanmaz ise, `if`'in sonunda o da `Nil` tipinde olur.

Bir `if` bölümünün içinde bir değerin tipi, o bölümde atanmış veya yeniden atanmamışsa, bölümden önce sahip olduğu değişken tipidir:

```crystal
a = 1
if bir_koşul
  a = "hello"
  # a : String
  a.size
end
# a : String | Int32
```

Diğer bir deyişle, bir değişkene ait tip, ona atanan son ifade(ler) tipini belirtir.

Eğer bölümlerden biri `if` bölümünün bitimine asla ulaşamazsa, yani `return`,`next`, `break` veya `raise` varsa, oluşacak olan bu tip `if`'in bitiminde hesaba katılamaz:

```crystal
if bir_koşul
  e = 1
else
  e = "hello"
  # e : String
  return
end
# e : Int32
```
