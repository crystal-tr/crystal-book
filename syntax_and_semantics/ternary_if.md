# Üç terimli if

Ternary bir `if`'i daha kısa bir yoldan yazmamıza olanak sağlar.

```crystal
a = 1 > 2 ? 3 : 4

# Yukarıdaki ifade aşağıdakine eşdeğerdir:
a = if 1 > 2
      3
    else
      4
    end
```
