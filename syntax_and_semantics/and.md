# && - Mantıksal AND Operatörü

Bir `&&`(ve) sol tarafını değerlendirir. Eğer *doğruluksa*, sağ tarafını değerlendirir ve bu değeri alır. Aksi halde sol tarafın değerini alır. Tipi her iki tarafın da birleşimidir.

Bir `&&`'i `if` ifadesi için sözdizimi kolaylığı olarak düşünebilirsiniz:


```crystal
some_exp1 && some_exp2

# Yukarıdaki ifade aşağıdakine eşdeğerdir:
tmp = some_exp1
if tmp
  some_exp2
else
  tmp
end
```
