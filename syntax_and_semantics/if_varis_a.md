# if var.is_a?(...)

Eğer bir `if` koşulu `is_a?` kontrolüyse, `then` bölümündeki tip tarafından değişkenin tipi kısıtlanır:

```crystal
if a.is_a?(String)
  # burada a String
end

if b.is_a?(Number)
  # burada b Number
end
```

Ayrıca, `else` bölümündeki tip tarafından değişkenin tipi kısıtlanamaz.

```crystal
a = bir_koşul ? 1 : "hello"
# a : Int32 | String

if a.is_a?(Number)
  # a : Int32
else
  # a : String
end
```

Unutmayın ki, `is_a?` kontrolünü tıpkı soyut sınıflar(abstract class) veya modüller gibi herhangi bir tip için kullanabilirsiniz.

Eğer koşulda ve(`&&`) bulunuyorsa bile yukarıdaki şekilde çalıştırılabilir:

```crystal
if a.is_a?(String) && b.is_a?(Number)
  # Burada a String ve b Number
end
```

Yukarıdaki ifade örnek ve sınıf değişkenleriyle **çalışmaz**. Bunlarla çalıştırmak için ilk önce bir değişkene atanması gereklidir.

```crystal
if @a.is_a?(String)
  # @a 'nın String olması kesin değildir
end

a = @a
if a.is_a?(String)
  # a 'nın String olması kesindir
end

# Biraz daha kısası:
if (a = @a).is_a?(String)
  # a 'nın String olması kesindir
end
```
