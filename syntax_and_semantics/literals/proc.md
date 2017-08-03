# Proc

Bir [Proc](http://crystal-lang.org/api/Proc.html) opsiyonel içerik(the closure data) ile beraber bir fonksiyon işaretçisini(pointer) temsil eder. Genellikle proc literali ile beraber oluşturulur:

```crystal
# Argümanı olmayan bir proc:
->{ 1 } # Proc(Int32)

# Bir argümanı olan bir proc:
->(x : Int32) { x.to_s } # Proc(Int32, String)

# İki argümanı olan bir proc:
->(x : Int32, y : Int32) { x + y } # Proc(Int32, Int32, Int32)
```

Argümanların tipleri zorunludur. Ancak C bağlamlarındaki(bindings) 'fun' kütüphanesine doğrudan bir proc literali gönderirken zorunlu değildir.

Geri dönüş tipi o procun gövdesinden(body) dönen tipinden anlamlandırılır.

Özel `new` metodu da bulunmaktadır:

```crystal
Proc(Int32, String).new { |x| x.to_s } # Proc(Int32, String)
```

Bu form, dönüş tipini belirtmenize ve procun gövdesine karşı kontrol etmenize izin verir.

## The Proc tipi

Proc tipini belirtmek için aşağıdakini yazabilirsiniz:

```crystal
# Tek argüman (Int32) kabul eden ve String dönen bir proc: 
Proc(Int32, String)

# Argüman kabul etmeyen ve Void dönen bir proc:
Proc(Void)

# İki argüman (bir Int32 ve bir String) kabul eden ve Char dönen bir proc:
Proc(Int32, String, Char)
```

Tip kısıtlamalarında, jenerik tipteki argümanlar ve bir tipin beklendiği diğer yerlerde, [tip grameri](../type_grammar.html)'nde açıklandığı gibi, daha kısa bir sözdizimi kullanabilirsiniz:

```crystal
# Bir Proc(Int32, String, Char) arrayi:
Array(Int32, String -> Char)
```

## Çalıştırma

Bir procu çalıştırmak için `call` metodu o procun üstünde çalıştırılır. Argümanların sayısı procun tipi ile eşleşmelidir:

```crystal
proc = ->(x : Int32, y : Int32) { x + y }
proc.call(1, 2) #=> 3
```

## Metotlardan

Var olan metotlardan bir proc yaratılabilir.

```crystal
def one
  1
end

proc = ->one
proc.call #=> 1
```

Eğer metodun argümanları varsa, hepsinin tipleri belirtilmelidir:

```crystal
def plus_one(x)
  x + 1
end

proc = ->plus_one(Int32)
proc.call(41) #=> 42
```

Bir proc opsiyonel olarak bir alıcı(receiver) belirleyebilir:

```crystal
str = "hello"
proc = ->str.count(Char)
proc.call('e') #=> 1
proc.call('l') #=> 2
```
