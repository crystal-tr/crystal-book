# Metotlar ve örnek değişkenler

Örnek değişkene bir metot argümanı atamak için daha kısa bir sözdizimi(syntax) kullanarak yapıcımızı(constructor) basitleştirebiliriz:

```crystal
class Person
  def initialize(@name : String)
    @age = 0
  end

  def age
    @age
  end
end
```

Şimdilik, bir kişi ile birlikte bir isim oluşturmaktan fazlasını yapamayız. Yaşı daima sıfır olacak. Bu sebeple, hadi bir kişinin büyüdüğü bir metot ekleyelim:

```crystal
class Person
  def initialize(@name : String)
    @age = 0
  end

  def age
    @age
  end

  def become_older
    @age += 1
  end
end

john = Person.new "John"
peter = Person.new "Peter"

john.age #=> 0

john.become_older
john.age #=> 1

peter.age #=> 0
```

Metot isimleri küçük harfle başlar ve kural olarak sadece küçük harf, alt çizgi ve rakamları kullanırlar.

# Getter ve setter

Crystal Standart Kütüphanesi, getter ve setter metotlarının tanımını basitleştiren makrolar sağlar:

```crystal
class Person
  property age
  getter name : String

  def initialize(@name)
    @age = 0
  end
end

john = Person.new "John"
john.age = 32
john.age #=> 32
```

Getter ve setter makroları hakkında daha fazla bilgi için, Object#getter, Object#setter ve Object#property için standart kitaplık belgelerine bakın.

Yan not olarak, orijinal `Person` tanımının içinde `become_older` veya ayrı bir yerde de tanımlayabiliriz: Crystal, tüm tanımları tek bir sınıfa birleştirir. Aşağıdaki ifade sorunsuz bir şekilde çalışır:

```crystal
class Person
  def initialize(@name : String)
    @age = 0
  end
end

class Person
  def become_older
    @age += 1
  end
end
```

## Tanımlama metotları, ve previos_def

Bir metodu yeniden tanımlarsanız, son tanımlama öncelik taşır.

```crystal
class Person
  def become_older
    @age += 1
  end
end

class Person
  def become_older
    @age += 2
  end
end

person = Person.new "John"
person.become_older
person.age #=> 2
```

Daha önce yeniden tanımlanan metodu `previous_def` ile çağırabilirsiniz:

```crystal
class Person
  def become_older
    @age += 1
  end
end

class Person
  def become_older
    previous_def
    @age += 2
  end
end

person = Person.new "John"
person.become_older
person.age #=> 3
```

Argümanı veya parantezi olmadan, `previous_def` metodun argümanları ile aynılarını alır. Aksi takdirde, bizim vereceğimiz argümanları alır.

## Catch-all initialization

Örnek değişkenler `initialize` metotlarının dışarısında da başlatılabilirler:

```crystal
class Person
  @age = 0

  def initialize(@name : String)
  end
end
```

Bu, her contructorda `@age` değerini sıfıra başlatacaktır. Bu, tekrarı önlemek için kullanışlıdır. Dahası bir sınıfı yeniden açarken ve ona örnek değişkenleri eklerken `Nil` tipinden kaçınmak için de yararlıdır.
