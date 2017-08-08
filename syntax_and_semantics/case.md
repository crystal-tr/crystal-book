# case

Bir 'case', patern eşleştirmesi benzeri bir işlev gören bir denetim ifadesidir. If-else-if zincirinin semantik olarak küçük bir değişiklikle ve daha güçlü bazı yapılarla yazılmasına izin verir.

Temel formunda bir değeri diğer değerlerle eşleştirmeye izin verir:

```crystal
case exp
when value1, value2
  bir_şey_yap
when value3
  başka_bir_şey_yap
else
  başka_bir_şey_daha_yap
end

# Yukarıdaki ifade aşağıdakine eşdeğerdir:
tmp = exp
if value1 === tmp || value2 === tmp
  bir_şey_yap
elsif value3 === tmp
  başka_bir_şey_yap
else
  başka_bir_şey_daha_yap
end
```

Bir `case` değerini başka bir ifade ile karşılaştırmak için *case eşitlik operatörü* `===` kullanılır. Bir metod olarak [`Nesne`](https://crystal-lang.org/api/Object.html#%3D%3D%3D%28other%29-instance-method) üzerinde tanımlanmıştır ve `case` ifadelerinde anlamlı semantikler sağlamak için alt sınıflar tarafından üzerine yazılabilir. Örneğin, [`Sınıf`](https://crystal-lang.org/api/Class.html#%3D%3D%3D%28other%29-instance-method) `case` eşitliğini, bir nesne o sınıfın bir örneği(instance) olduğundaki gibi tanımlar, [`Düzenli İfadeler`](https://crystal-lang.org/api/Regex.html#%3D%3D%3D%28other%3AString%29-instance-method) değer düzenli ifade ile eşleştiği zamandaki gibi ve [`Aralık`](https://crystal-lang.org/api/Range.html#%3D%3D%3D%28value%29-instance-method) değer o aralıkta olduğundaki gibi.

Bir `when` ifadesi bir tip ise,`is_a?` kullanılır. Ayrıca, case ifadesi değişken veya değişken atama ise, değişkenin tipi kısıtlanır:

```crystal
case var
when String
  # var : String
  bir_şey_yap
when Int32
  # var : Int32
  başka_bir_şey_yap
else
  # burada var String de değil, Int32 de değil
  başka_bir_şey_daha_yap
end

# Yukarıdaki ifade aşağıdakine eşdeğerdir:
if var.is_a?(String)
  do_something
elsif var.is_a?(Int32)
  başka_bir_şey_yap
else
  başka_bir_şey_daha_yap
end
```

Örtülü nesne söz dizimini(implicit-object syntax) kullanarak bir `case` ifadesinde bulunan `when`'in içinde metod çağırabilirsiniz:

```crystal
case num
when .even?
  bir_şey_yap
when .odd?
  başka_bir_şey_yap
end

# Yukarıdaki ifade aşağıdakine eşdeğerdir:
tmp = num
if tmp.even?
  bir_şey_yap
elsif tmp.odd?
  başka_bir_şey_yap
end
```

Sonunda, `case`'in değerini atlayabilirsiniz:

```crystal
case
when cond1, cond2
  bir_şey_yap
when cond3
  başka_bir_şey_yap
end

# Yukarıdaki ifade aşağıdakine eşdeğerdir:
if cond1 || cond2
  bir_şey_yap
elsif cond3
  başka_bir_şey_yap
end
```

Bazen okunması daha doğal olan kodlara yol açar.

## Tuple literal

Hem case ifadesinin bir tuple literali, hem de when koşulunun bir tuple literali olması durumunda, birkaç semantik farklılık vardır.

### Tuple boyutu eşleşmeli

```crystal
case {value1, value2}
when {0, 0} # 2 elemanlı olduğu için hata yok
  # ...
when {1, 2, 3} # Derleme hatası, çünkü asla eşlenemez
  # ...
end
```

### Altçizgi(_) kullanılabilir

```crystal
case {value1, value2}
when {0, _}
  # eğer 0 === value1 ise eşlenir, value2 için bir kontrol yapılmaz
when {_, 0}
  # eğer 0 === value2 ise eşlenir, value1 için bir kontrol yapılmaz
end
```

### Örtülü nesne(Implicit-object) kullanılabilir

```crystal
case {value1, value2}
when {.even?, .odd?}
  # Eğer value1.even? && value2.odd? ise eşlenir
end
```

### Bir tipe karşı karşılaştırmak, is_a? kontrolünü çalıştıracak

```crystal
case {value1, value2}
when {String, Int32}
  # eğer value1.is_a?(String) && value2.is_a?(Int32) ise eşler
  # value1'in tipi derleyici tarafından String
  # ve value2'nin tipi Int32 olarak biliniyor
end
```
