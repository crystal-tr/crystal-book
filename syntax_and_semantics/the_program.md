# Program

Program nesnesi, içinde tipler, metodlar ile dosya ve yerel değişkenleri tanımlayabileceğiniz global bir nesnedir.

```crystal
# Programda bir metod tanımlanıyor.
def add(x, y)
  x + y
end

# Programda add metodu çağırılıyor.
add(1, 2) #=> 3
```

Bir metodun değeri, son ifadesinin değeridir; açık olarak bir `return` ifadesine gerek yoktur. Bununla birlikte, açık olarak`return` ifadesi kullanmak mümkündür.

```crystal
def even?(num)
  if num % 2 == 0
    return true
  end

  return false
end
```

`add(1, 2)` gibi bir alıcısı(receiver) olmayan bir metod çağırılırken, geçerli tipe veya atasına rastlanmazsa programın içinde aranır.

```crystal
def add(x, y)
  x + y
end

class Foo
  def bar
    # Programın add metodu çağırılıyor.
    add(1, 2)

    # Foo's baz metodu çağırılıyor.
    baz(1, 2)
  end

  def baz(x, y)
    x * y
  end
end
```

Programın metodunu çağırmak isterseniz, geçerli tipin aynı isimde bir metodu tanımlanmış olsa bile, çağrıyı `::` önekiyle yapmalıdır:

```crystal
def baz(x, y)
  x + y
end

class Foo
  def bar
    baz(4, 2) #=> 2
    ::baz(4, 2) #=> 6
  end

  def baz(x, y)
    x - y
  end
end
```

Bir programda bildirilen değişkenler metotlarda görünmez:

```crystal
x = 1

def add(y)
  x + y # error: undefined local variable or method 'x'
end

add(2)
```

Metod çağrılarında parantezler isteğe bağlıdır:

```crystal
add 1, 2 # add(1, 2) ile aynı
```

## Ana kod

Bir program derlenip ve çalıştırıldığında çalışan kod olan ana kod, doğrudan bir kaynak dosyasına "main" bir metod koymaya gerek kalmadan doğrudan yazılabilir:

```crystal
# Ekrana "Hello Crystal!" yazdıran bir program
puts "Hello Crystal!"
```

Ana kod tip tanımlamalarının içinde de olabilir:

```crystal
# Ekrana "Hello" yazdıran bir proram
class Hello
  # 'self' burada bir Hello sınıfı
  puts self
end
```
