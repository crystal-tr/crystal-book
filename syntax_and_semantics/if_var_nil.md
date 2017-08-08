# if var.nil?

Bir `if` koşulu `var.nil?` olduğu zaman `then` bölümündeki değişken tipi  derleyici tarafından `Nil` olarak bilinir ve `else` bölümünde de `Nil` olmadığı bilinir.

```crystal
a = bir_koşul ? nil : 3
if a.nil?
  # burada a Nil
else
  # burada a Int32
end
```
