# if !

The `!` operatörü, bir değerin [doğruluğunun](truthy_and_falsey_values.html) olumsuzunu alarak bir `Bool` döner.

Bir `if`'de bir değişken ile birlikte `is_a?`, `respond_to?` veya `nil?` beraber kullanıldığı zaman, derleyici, tipleri buna göre kısıtlar:

```crystal
a = bir_koşul ? nil : 3
if !a
  # burada a is Nil, çünkü bu bölümde bir *yanlışlık*'tır.
else
  # burada a is Int32, çünkü bu bölümde bir *doğruluk*'tır.
end
```

```crystal
b = bir_koşul ? 1 : "x"
if !b.is_a?(Int32)
  # burada b String çünkü bir Int32 değil
end
```
