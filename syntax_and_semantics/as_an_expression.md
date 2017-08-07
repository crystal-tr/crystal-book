# İfade olarak if

Bir `if`'in değeri, her bir bölümünün içinde bulunan en son ifadenin değeridir.

```crystal
a = if 2 > 1
      3
    else
      4
    end
a #=> 3
```

Eğer bir `if`'in bölümü boş ise veya kayıpsa içinde sanki `nil` varmış gibi hesaba katılır.

```crystal
if 1 > 2
  3
end

# Yukarıdaki ifade aşağıdakine eşdeğerdir:
if 1 > 2
  3
else
  nil
end

# Başka bir örnek:
if 1 > 2
else
  3
end

# Yukarıdaki ifade aşağıdakine eşdeğerdir:
if 1 > 2
  nil
else
  3
end
```
