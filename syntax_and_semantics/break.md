# break

Bir `while` döngüsünü kırmak için `break` kullanabilirsiniz:

```crystal
a = 2
while (a += 1) < 20
  if a == 10
    # 'puts a'ya gidecek
    break
  end
end
puts a #=> 10
```
