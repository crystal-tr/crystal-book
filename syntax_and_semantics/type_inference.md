# Tip çıkarımı

Crystal'in felsefesi, mümkün olduğunca az sayıda tip açıklaması yapmaktır. Bununla birlikte, bazen tip açıklamaları gereklidir.

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

## Açık bir tip açıklaması kullanın

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

## Açık bir tip açıklaması kullanmayın

Açık bir tip açıklamasını atlarsanız, derleyici bir dizi sözdizimsel kurallar kullanarak örnek ve sınıf değişkenlerini türetmeye çalışacaktır.

Verilen bir örnek/sınıf değişkeni için, bir kural uygulanabilir ve bir tip tahmin edilebilir olduğunda, tip bir gruba eklenir. Başka hiçbir kural uygulanamadığında, çıkarım yapılan tipi bu tiplerin [birleşimi(union)] (union_types.html) olacaktır. Ayrıca, derleyici, bir örnek değişkeni her zaman başlatılamadığını bildirirse, [Nil] (literal / nil.html) tipini de içerecektir.

Kurallar çoktur, ancak genellikle en çok kullanılan ilk üçüdür. Ayrıca hepsini hatırlamaya hiç gerek yok. Derleyici, bir örnek değişkeni tipinin çıkarılamadığını söyleyen bir hata verirse, her zaman açık bir tip açıklaması ekleyebilirsiniz.

Aşağıdaki kurallar yalnızca örnek değişkenlerden bahsetmekle birlikte, sınıf değişkenleri için de geçerlidir. Onlar:

### 1.Gerçek değer atama

Bir örnek değişkene bir değişmez tayin edildiğinde, değişmezin tipi kümeye eklenir. Tüm [literaller] (literals.html) ilişkili bir tipe sahiptir.

Aşağıdaki örnekte `@name`,`String` ve `@age` öğeleri `Int32` olarak çıkarımı yapılacaktır.

```crystal
class Person
  def initialize
    @name = "John Doe"
    @age = 0
  end
end
```

Bu kural ve takip eden her kural, `initialize` da dahil olmak üzere her metot için uygulanacaktır. Örneğin:

```crystal
class SomeObject
  def lucky_number
    @lucky_number = 42
  end
end
```

Yukarıdaki durumda `@lucky_number`'ın `Int32 | Nil`: `Int32` olduğu varsayılacaktır, çünkü ona atanmış 42 ve `Nil`, çünkü sınıflarının hiçbirinde başlangıç metodunda atanmamıştı.

### 2. `new` sınıf metodunun çağırılması sonucu atama

Bir örnek değişkene `Type.new(...)` gibi bir ifade atandığı zaman, o tip kümeye eklenir.

Aşağıdaki örnekte, `@address`, `Address` olarak çıkarımı yapılacaktır.

```crystal
class Person
  def initialize
    @address = Address.new("Herhangi bir yer")
  end
end
```
Bu, jenerik tiplere de uygulanır. Burada `@values`, `Array (Int32)` olarak çıkarımı yapılır.

```crystal
class Something
  def initialize
    @values = Array(Int32).new
  end
end
```

**Not**: bir `new` metodu bir tipe göre yeniden tanımlanabilir. Bu gibi bir durumda; daha sonraki kurallardan bazıları kullanılarak çıkarımlanmış tip, `new` tarafından geri dönen tip olacaktır.

### 3. Bir tip kısıtlamalı metot argümanı olan değişkeni atama

Aşağıdaki örnekte, `name` `String` tipi bir kısıtlamaya sahip olduğu için `name` öğesinin `String` olduğu varsayılmaktadır ve bu argüman `@name` olarak atanmaktadır.

```crystal
class Person
  def initialize(name : String)
    @name = name
  end
end
```
Metot argümanının adının önemli olmadığını unutmayın; bu şekilde de çalışacaktır:

```crystal
class Person
  def initialize(obje : String)
    @name = obje
  end
end
```

Bir örnek değişkeni daha kısa bir sözdizimi kullanarak metot argümanından atayamak da aynı etkiyi yapacaktır:

```crystal
class Person
  def initialize(@name : String)
  end
end
```
Ayrıca, derleyici, bir metot argümanının farklı bir değere yeniden atanıp atanmadığını denetlemediğine dikkat edin:

```crystal
class Person
  def initialize(name : String)
    name = 1
    @name = name
  end
end
```
Yukarıdaki durumda, derleyici yine de `@name` öğesini `String` olarak çıkaracak ve daha sonra bu metodu tam olarak yazarken `Int32`'nin `String` tipinde bir değişkene atanamayacağını söyleyerek derleme zamanı hatası verecektir. `@name` bir `String` olması gerekmiyorsa, açık bir tip açıklaması kullanın.

### 4. Dönüş tipi açıklamasına sahip bir sınıf metodunun sonucunu atama

Aşağıdaki örnekte, `Address.unknown` sınıf metodu `Address` öğesinin dönüş tipi açıklamasına sahip olduğu için `@address` öğesinin `Address` olduğu söylenebilir.

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

Aslında, yukarıdaki kod `self.unknown`'da dönüş tipi açıklamasına ihtiyaç duymaz. Bunun nedeni, derleyicinin bir sınıf metodunun gövdesine de bakması ve önceki kurallardan birini uygulayabilmesi (yeni bir metot veya bir constant, vb.), bu ifadenin türünü çıkaracağıdır. Yani, yukarıdaki gibi basitçe yazılabilir:

```crystal
class Person
  def initialize
    @address = Address.unknown
  end
end

class Address
  # Burada bir dönüş tipi açıklamasına gerek yok
  def self.unknown
    new("unknown")
  end

  def initialize(@name : String)
  end
end
```

Bu fazladan kural çok uygundur çünkü `new`'e ek olarak "constructor benzeri" sınıf metotlarına sahip olmak çok yaygındır.

### 5. Bir metot argümanı olan bir değişkeni varsayılan değerle atama

Aşağıdaki örnekte, `name` varsayılan değeri bir string literalidir ve daha sonra `@name`'ye atandığından, çıkarılmış tipler kümesine `String` eklenecektir.

```crystal
class Person
  def initialize(name = "John Doe")
    @name = name
  end
end
```

Bu elbette kısa sözdizimi ile de çalışır:

```crystal
class Person
  def initialize(@name = "John Doe")
  end
end
```

Varsayılan değer ayrıca, `Type.new(...)` metodu veya dönüş tipi açıklaması olan bir sınıf metodu olabilir.

### 6. Bir `lib` fonksiyonunun çağrılması sonucu atama

Bir [lib fonksiyonu](c_bindings/fun.html) açık tiplere sahip olması gerektiği için, derleyici onu bir örnek değişkene atarken kullanabilir.

Aşağıdaki örnekte `@age`, `Int32` olarak çıkarımı yapılmıştır.

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

### 7. Bir `out` lib ifadesi kullanma

Bir [lib fonksiyonu](c_bindings/fun.html) açık tiplere sahip olması gerektiği için, derleyici pointer(işaretçi) tipinde olması gereken `out` argümanının tipini kullanabilir ve referansından ayrılmış tipi tahmini şekilde kullanabilir.

Aşağıdaki örnekte `@age`, `Int32` olarak çıkarılmıştır.

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

### Diğer kurallar

Derleyici, daha az açıklama gerektirecek kadar akıllı olmaya çalışacaktır. Örneğin, bir `if` ifadesi atanırken, `then` ve `else` dallarından tipini çıkaracaktır:

```crystal
class Person
  def initialize
    @age = some_condition ? 1 : 2
  end
end
```

Yukarıdaki `if` (aslında teknik yönden bu bir ternary operatör, ancak bir `if`'e benzemektedir) integer literaline sahip olduğu için, `@age`, gereksiz bir tip açıklaması gerektirmeden başarılı bir şekilde `Int32` olduğu çıkarılır.

Başka bir durum ise `||` ve `|| =`:

```crystal
class SomeObject
  def lucky_number
    @lucky_number ||= 42
  end
end
```
Yukarıdaki örnekte `@lucky_number`'ın `Int32 | Nil` olduğu varsayılacaktır. Bu, tembel şekilde başlatılan değişkenler için çok yararlıdır.

Constantlar(değişmezler) de derleyici (ve bir insan) tarafından kolay bir şekilde takip edilecektir.

```crystal
class SomeObject
  DEFAULT_LUCKY_NUMBER = 42

  def initialize(@lucky_number = DEFAULT_LUCKY_NUMBER)
  end
end
```

Burada kural 5 (argümanın varsayılan değeri) kullanılır ve constant(değişmez) integer literali olarak çözümlediğinden, `@lucky_number`, `Int32` olarak çıkarım yapılır.
