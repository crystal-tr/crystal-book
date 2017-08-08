# unless

Bir `unless`, `then` bölümünü koşulu *yanlışlık* ise hesaplar. Aksi takdirde,  eğer bulunuyorsa `else` bölümünü hesaplar. Yani `if`'in tersi şeklinde davranır:

```crystal
unless bir_koşul
  then_ifadesi
else
  else_ifadesi
end

# Yukarıdaki ifade aşağıdakine eşdeğerdir:
if bir_koşul
  else_ifadesi
else
  then_ifadesi
end

# Ayrıca son ek olarak da yazılabilir
close_door unless door_closed?
```
