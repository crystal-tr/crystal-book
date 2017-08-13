# || - Mantıksal OR Opetatörü

Bir `||`(veya) sol tarafını değerlendirir. *yanlışlık* ise, sağ tarafını değerlendirir ve bu değeri taşır. Aksi halde sol tarafın değerini alır. Tipi her iki tarafın da birleşimidir.

Bir `||`'u `if` ifadesi için sözdizimi kolaylığı olarak düşünebilirsiniz:

```crystal
some_exp1 || some_exp2

# Yukarıdaki ifade aşağıdakine eşdeğerdir:
tmp = some_exp1
if tmp
  tmp
else
  some_exp2
end
```
