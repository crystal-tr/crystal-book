# next

Bir `while` döngüsünün bir sonraki tekrarını yürütebilmesi için `next`'i kullanabilirsiniz. `next` çalıştıktan sonra, `while`'ın koşulu kontrol edilir ve eğer *doğruluk* ise, gövdesi çalıştırılır.

```crystal
a = 1
while a < 5
  a += 1
  if a == 3
    next
  end
  puts a
end
# The above prints the numbers 2, 4 and 5
```
