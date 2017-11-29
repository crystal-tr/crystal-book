# new, initialize ve allocate

Bir sınıfın bir örneğini, o sınıfa `new` metodunu çağırarak oluşturabilirsiniz:

```
person = Person.new
```

Burada `person`, `Person` sınıfının bir örneğidir.

`person` ile pek fazla bir şey yapamayız, bu yüzden ona bazı kavramlar ekleyelim. Bir `Person`'ın bir `name`'i ve bir `age`'i vardır. "Her şey bir nesne" bölümünde, bir nesnenin bir tipe sahip olduğunu ve nesnelerle etkileşime girmenin tek yolu olan bazı metotlara yanıt verdiğini söyledik, bu yüzden hem `name` hem de `age` metotlarına ihtiyacımız olacak. Bu bilgiyi her zaman, bir *at*(@) karakteri öneki olan değişkenlere depolayacağız. Aynı zamanda, bir Person'ın, bizim seçeceğimiz bir isim ve sıfır yaşıyla var olmasını istiyoruz. Normalde * constructor(yapıcı) * olarak adlandırılan özel bir `initialize` metodu ile "var olmaya başlama" bölümünü kodlarız:

```crystal
class Person
  def initialize(name : String)
    @name = name
    @age = 0
  end

  def name
    @name
  end

  def age
    @age
  end
end
```

Artık bu şekilde Person nesneleri oluşturabiliriz:

```crystal
john = Person.new "John"
peter = Person.new "Peter"

john.name #=> "John"
john.age #=> 0

peter.name #=> "Peter"
```

(Eğer `name`'in bir `String` olduğunu belirtmemiz gerektiğini ve bunu `age` için yapmamız gerekmediğinin nedenini merak ediyorsanız, [Global tip çıkarım algoritmasını] kontrol ediniz. (type_inference.html))

Unutmayın ki `new` ile bir `Person` oluştururuz, ancak başlatmayı, `new` metodu ile değil bir `initialize` metodu ile tanımladık. Peki neden bu böyle?

Bunun cevabı, bir `initialize` metodu tanımladığımız zaman Crystal, bizim için şu gibi bir `new` metodu tanımladı:

```crystal
class Person
  def self.new(name : String)
    instance = Person.allocate
    instance.initialize(name)
    instance
  end
end
```

İlk olarak, `self.new` gösterimine dikkat edin. Bu, metodun o sınıfa ait belirli örneklere değil ** sınıfa ** yani `Person`'a ait olduğu anlamına gelir. Bu sebeple `Person.new` yapabiliriz.

İkincisi, `allocate`, verilen tipe ait başlatılmamış nesneyi yaratan düşük seviye bir sınıf metodur. Temelde nesne için gerekli belleği tahsis eder, daha sonra üzerinde `initialize` çağrılır ve nihayet örnek geri döndürülür. [Güvenliksiz] (unsafe.html) olduğu için genellikle `allocate` komutunu çağırmazsınız, fakat ` new` ve `initialize`'ın ilişkilendirilmesinin nedeni budur.
