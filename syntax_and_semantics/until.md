# until

Bir `until`, koşulu *doğruluk* olana kadar gövdesini çalıştırır. Bir `until` ifadesi, koşulu negatif olan bir `while` için sözdizimi kolaylığıdır:

```crystal
until bir_koşul
  bir_şey_yap
end

# Yukarıdaki ifade aşağıdakine eşdeğerdir:
while !bir_koşul
  bir_şey_yap
end
```

`break` ve` next` ayrıca `until` içinde de kullanılabilir.
