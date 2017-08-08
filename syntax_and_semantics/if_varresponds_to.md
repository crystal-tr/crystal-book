# if var.responds_to?(...)

Bir `if` koşulu bir `respond_to?` kontrolüyse, `then` bölümünde o metoda yanıt veren tipler tarafından değişkenin tipi kısıtlanır:

```crystal
if a.responds_to?(:abs)
  # a 'nın tipi 'abs' metoduna yanıt verenlere düşürülür
end
```

Ayrıca, `else` bölümünde o metoda yanıt vermeyen tipler tarafından değişkenin tipi kısıtlanamaz.

```crystal
a = bir_koşul ? 1 : "hello"
# a : Int32 | String

if a.responds_to?(:abs)
  # burada a Int32, çünkü Int32#abs bulunuyor fakat String#abs bulunmuyor
else
  # burada a String 
end
```

Yukarıdaki ifade örnek ve sınıf değişkenleriyle **çalışmaz**. Bunlarla çalıştırmak için ilk önce bir değişkene atanması gereklidir.

```crystal
if @a.responds_to?(:abs)
  # @a 'nın String olması kesin değildir
end

a = @a
if a.responds_to?(:abs)
  # a 'nın `abs`'ye cevap vereceği kesindir
end

# Biraz daha kısası:
if (a = @a).responds_to?(:abs)
  # a 'nın `abs`'ye cevap vereceği kesindir
end
```

