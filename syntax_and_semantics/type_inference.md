# Tip çıkarımı

Crystal'in felsefesi, mümkün olduğunca az sayıda tip notasyonu yapmaktır. Bununla birlikte, bazen tip notasyonları gereklidir.

Böyle bir sınıf tanımı düşünün:

```crystal
class Person
  def initialize(@name)
    @age = 0
  end
end
```
Kolayca `@age`'in bir tamsayı olduğunu görebiliriz, ancak` @name`'in tipinin ne olduğunu bilmiyoruz. Derleyici, onun tipini 'Person' sınıfının tüm kullanımlarından çıkarabilir. Bununla birlikte, bunu yaparken birkaç sorun ile karşılaşabiliriz:

* Kodu okuyan birisi için tip açık değildir ve okuyan kişi bunu bulmak için bütün "Person" kullanımlarını da kontrol etmesi gerekir.

* Bir metodu yalnızca bir kez analiz etmek zorunda kalmak gibi bazı derleyici optimizasyonlarının yapılması neredeyse imkansızdır.

Bir kod tabanı büyüdükçe, bu konular daha fazla önem kazanır: Bir projeyi anlamanız zorlaşır ve derleme zamanları katlanılmaz hale gelir.

Bu nedenle, Crystal, açık bir şekilde(bir insanın anlayabileceği kadar açık) örnek ve [sınıf](class_variables.html) değişkenlerinin tiplerini bilmelidir.

Crystal'ın bunu bilmesinin birkaç yolu vardır.

## Açık bir tip notasyonu kullanın

En kolay, ancak muhtemelen en sıkıcı yolu, açık açıklama ek açıklamalar kullanmaktır.

```crystal
class Person
  @name : String
  @age : Int32

  def initialize(@name)
    @age = 0
  end
end
```

## Açık bir tip notasyonu kullanmayın

Açık bir tip notasyonunu atlarsanız, derleyici bir dizi sözdizimsel kurallar kullanarak örnek ve sınıf değişkenlerini türetmeye çalışacaktır.

Verilen bir örnek/sınıf değişkeni için, bir kural uygulanabilir ve bir tip tahmin edilebilir olduğunda, tip bir gruba eklenir. Başka hiçbir kural uygulanamadığında, çıkarım yapılan tipi bu tiplerin [birleşimi(union)] (union_types.html) olacaktır. Ayrıca, derleyici, bir örnek değişkeni her zaman başlatılamadığını bildirirse, [Nil] (literal / nil.html) tipini de içerecektir.

Kurallar çoktur, ancak genellikle ilk üçü en çok kullanılır. Ayrıca hepsini hatırlamaya hiç gerek yok. Derleyici, bir örnek değişkeni türünün çıkarılmadığını söyleyen bir hata verirse, her zaman açık bir tip notasyonu ekleyebilirsiniz.

Aşağıdaki kurallar yalnızca örnek değişkenlerden bahsetmekle birlikte, sınıf değişkenleri için de geçerlidir. Onlar:

### 1.Gerçek değer atama

Bir örnek değişkene bir değişmez tayin edildiğinde, değişmezin türü kümeye eklenir. Tüm [literaller] (literals.html) ilişkili bir tipe sahiptir.

Aşağıdaki örnekte `@name`,`String` ve `@age` öğeleri `Int32` olarak çıkarımı yapılacaktır.

```crystal
class Person
  def initialize
    @name = "John Doe"
    @age = 0
  end
end
```

Bu kural ve takip eden her kural, `initialize` da dahil olmak üzere her metod için uygulanacaktır. Örneğin:

```crystal
class SomeObject
  def lucky_number
    @lucky_number = 42
  end
end
```

Yukarıdaki durumda `@lucky_number`'ın `Int32 | Nil`: `Int32` olduğu varsayılacaktır, çünkü ona atanmış 42 ve `Nil`, çünkü sınıflarının hiçbirinde başlangıç metodunda atanmamıştı.

### 2. Assigning the result of invoking the class method `new`

When an expression like `Type.new(...)` is assigned to an instance variable, the type `Type` is added to the set.

In the following example, `@address` is inferred to be `Address`.

```crystal
class Person
  def initialize
    @address = Address.new("somewhere")
  end
end
```

This also is applied to generic types. Here `@values` is inferred to be `Array(Int32)`.

```crystal
class Something
  def initialize
    @values = Array(Int32).new
  end
end
```

**Note**: a `new` method might be redefined by a type. In that case the inferred type will be the one returned by `new`, if it can be inferred using some of the next rules.

### 3. Assigning a variable that is a method argument with a type restriction

In the following example `@name` is inferred to be `String` because the method argument `name` has a type restriction of type `String`, and that argument is assigned to `@name`.

```crystal
class Person
  def initialize(name : String)
    @name = name
  end
end
```

Note that the name of the method argument is not important; this works as well:

```crystal
class Person
  def initialize(obj : String)
    @name = obj
  end
end
```

Using the shorter syntax to assign an instance variable from a method argument has the same effect:

```crystal
class Person
  def initialize(@name : String)
  end
end
```

Also note that the compiler doesn't check whether a method argument is reassigned a different value:

```crystal
class Person
  def initialize(name : String)
    name = 1
    @name = name
  end
end
```

In the above case, the compiler will still infer `@name` to be `String`, and later will give a compile time error, when fully typing that method, saying that `Int32` can't be assigned to a variable of type `String`. Use an explicit type annotation if `@name` isn't supposed to be a `String`.

### 4. Assigning the result of a class method that has a return type annotation

In the following example, `@address` is inferred to be `Address`, because the class method `Address.unknown` has a return type annotation of `Address`.

```crystal
class Person
  def initialize
    @address = Address.unknown
  end
end

class Address
  def self.unknown : Address
    new("unknown")
  end

  def initialize(@name : String)
  end
end
```

In fact, the above code doesn't need the return type annotation in `self.unknown`. The reason is that the compiler will also look at a class method's body and if it can apply one of the previous rules (it's a `new` method, or it's a literal, etc.) it will infer the type from that expression. So, the above can be simply written like this:

```crystal
class Person
  def initialize
    @address = Address.unknown
  end
end

class Address
  # No need for a return type annotation here
  def self.unknown
    new("unknown")
  end

  def initialize(@name : String)
  end
end
```

This extra rule is very convenient because it's very common to have "constructor-like" class methods in addition to `new`.

### 5. Assigning a variable that is a method argument with a default value

In the following example, because the default value of `name` is a string literal, and it's later assigned to `@name`, `String` will be added to the set of inferred types.

```crystal
class Person
  def initialize(name = "John Doe")
    @name = name
  end
end
```

This of course also works with the short syntax:

```crystal
class Person
  def initialize(@name = "John Doe")
  end
end
```

The default value can also be a `Type.new(...)` method or a class method with a return type annotation.

### 6. Assigning the result of invoking a `lib` function

Because a [lib function](c_bindings/fun.html) must have explicit types, the compiler can use the return type when assigning it to an instance variable.

In the following example `@age` is inferred to be `Int32`.

```crystal
class Person
  def initialize
    @age = LibPerson.compute_default_age
  end
end

lib LibPerson
  fun compute_default_age : Int32
end
```

### 7. Using an `out` lib expression

Because a [lib function](c_bindings/fun.html) must have explicit types, the compiler can use the `out` argument's type, which should be a pointer type, and use the dereferenced type as a guess.

In the following example `@age` is inferred to be `Int32`.

```crystal
class Person
  def initialize
    LibPerson.compute_default_age(out @age)
  end
end

lib LibPerson
  fun compute_default_age(age_ptr : Int32*)
end
```

### Other rules

The compiler will try to be as smart as possible to require less explicit type annotations. For example, if assigning an `if` expression, type will be inferred from the `then` and `else` branches:

```crystal
class Person
  def initialize
    @age = some_condition ? 1 : 2
  end
end
```

Because the `if` above (well, technically a ternary operator, but it's similar to an `if`) has integer literals, `@age` is successfully inferred to be `Int32` without requiring a redundant type annotation.

Another case is `||` and `||=`:

```crystal
class SomeObject
  def lucky_number
    @lucky_number ||= 42
  end
end
```

In the above example `@lucky_number` will be inferred to be `Int32 | Nil`. This is very useful for lazily initialized variables.

Constants will also be followed, as it's pretty simple for the compiler (and a human) to do so.

```crystal
class SomeObject
  DEFAULT_LUCKY_NUMBER = 42

  def initialize(@lucky_number = DEFAULT_LUCKY_NUMBER)
  end
end
```

Here rule 5 (argument's default value) is used, and because the constant resolves to an integer literal, `@lucky_number` is inferred to be `Int32`.
