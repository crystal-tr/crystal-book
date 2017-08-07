# Çoklu değer atama

Aynı anda birden fazla çoklu tanımlama/atama'yı virgül (`,`) ile ifadeleri birbirinden ayırarak yapabilirsiniz.

```crystal
name, age = "Crystal", 1

# Yukarıdaki kullanım şu şekilde de yazılabilir:
temp1 = "Crystal"
temp2 = 1
name  = temp1
age   = temp2
```

Unutmayın ki, ifadelerin geçici değişkenlere atanması nedeniyle değişkenlerin içeriğini tek bir satıra aktarmanız mümkündür:

```crystal
a = 1
b = 2
a, b = b, a
a #=> 2
b #=> 1
```

Sağ taraftaki sadece bir ifade içeriyorsa, bir dizinli tip olarak kabul edilir ve aşağıdaki sözdizimi kolaylığını uygular:

```crystal
name, age, source = "Crystal,1,github".split(",")

# Yukarıdaki kullanım şu şekilde de yazılabilir:
temp = "Crystal,1,github".split(",")
name   = temp[0]
age    = temp[1]
source = temp[2]
```

Sol tarafta sadece bir değişken varsa, sağ taraf bir array olarak değerlendirilir:

```crystal
names = "John", "Peter", "Jack"

# Yukarıdaki kullanım şu şekilde de yazılabilir:
names = ["John", "Peter", "Jack"]
```

`=` Ile biten metotlar için de çoklu atama da mevcuttur:

```crystal
person.name, person.age = "John", 32

# Yukarıdaki kullanım şu şekilde de yazılabilir:
temp1 = "John"
temp2 = 32
person.name = temp1
person.age = temp2
```

Aynı zamanda sıralayıcılar için de mevcuttur (`[]=`):

```crystal
objects[1], objects[2] = 3, 4

# Same as:
temp1 = 3
temp2 = 4
objects[1] = temp1
objects[2] = temp2
```
