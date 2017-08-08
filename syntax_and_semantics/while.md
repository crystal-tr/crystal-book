# while

Bir `while`, koşulunun *doğruluğu* sağlandığı sürece gövdesi(body) çalıştırılır.

```crystal
while bir_koşul
  bunu_yap
end
```

İlk olarak koşul kontrol edilir ve eğer *doğruysa*, gövdesi  çalıştırılır. Yani, gövdesi hiç çalıştırılamayabilir.

Bir `while`'ın tipi her zaman `Nil`'dir.

`if`'e benzer bir şekilde, eğer bir `while`'ın koşulu bir değişkense, o değişken gövdenin içindeyken `nil` olamaz. Eğer koşul bir `var.is_a?(Type)` kontrolüyse, `var` gövdenin içinde is Type'ın tipinde olur. Eğer if koşul bir `var.responds_to?(:method)` kontrolü ise, `var` o metod'a yanıt veren tipte olur.

`while`'dan sonraki bir değişkenin tipi, `while`'dan önceki sahip olduğu ve `while`'ın gövdesini terk etmeden önceki tipine bağlıdır:

```crystal
a = 1
while bir_koşul
  # a : Int32 | String
  a = "hello"
  # a : String
  a.size
end
# a : Int32 | String
```

## Bir döngünün sonunda durumun kontrol edilmesi

Eğer içerisini en az bir kere çalıştırıp sonra da döngüyü kıracak bir koşulla kontrolü sağlamak için aşağıdaki gibi kullanabilirsiniz:

```crystal
while true
  bir_şey_yap
  break if bir_koşul
end
```

Veya standart kütüphanede bulunan `loop`'u kullanın:

```crystal
loop do
  bir_şey_yap
  break if bir_koşul
end
```
