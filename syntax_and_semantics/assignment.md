# Değer Atama

Atama eşittir (`=`) karakteri ile yapılır.

```crystal
# Lokal bir değişkene değer atama
local = 1

# Örnek bir değişkene değer atama
@instance = 2

# Sınıf değişkenine değer atama
@@class = 3
```

Yukarıdaki değişkenlerin her biri daha sonra açıklanacaktır.

`=` Karakterini içeren bazı sözdizimi kolaylıkları(syntax sugar) aşağıdaki gibi mevcuttur:

```crystal
local += 1  # local = local + 1 ile aynı

# Yukarıdaki ifade aşağıdakilerle de geçerlidir:
# +, -, *, /, %, |, &, ^, **, <<, >>

local ||= 1 # same as: local || (local = 1)
local &&= 1 # same as: local && (local = 1)
```

`=` Ile biten bir metot çağrısı sözdizimi kolaylığına sahiptir:

```crystal
# Bir belirleyici(setter)
person.name=("John")

# Yukarıdaki kullanım şu şekilde de yazılabilir:
person.name = "John"

# Bir sıralı atama
objects.[]=(2, 3)

# Yukarıdaki kullanım şu şekilde de yazılabilir:
objects[2] = 3

# Değer atama ile alakalı değil fakat bir söz dizimi kolaylığıdır:
objects.[](2, 3)

# Yukarıdaki kullanım şu şekilde de yazılabilir:
objects[2, 3]
```

`=` operatörü sözdizimi kolaylığı Belirleyiciler(setter) ve sıralayıcılar(indexer) için de kullanılabilir. Unutmayın ki `||` ve `&&` operatörleri tarafından `[]?` metodu kullanılarak anahtarın varlığı kontrol edilir.

```crystal
person.age += 1        # person.age = person.age + 1 ile aynı

person.name ||= "John" # person.name || (person.name = "John") ile aynı
person.name &&= "John" # person.name && (person.name = "John") ile aynı

objects[1] += 2        # objects[1] = objects[1] + 2 ile aynı

objects[1] ||= 2       # objects[1]? || (objects[1] = 2) ile aynı
objects[1] &&= 2       # objects[1]? && (objects[1] = 2) ile aynı
```
