# Range

Bir [Range](http://crystal-lang.org/api/Range.html) genellikle range literali kullanılarak oluşturulur:

```crystal
x..y  # matematikte kullanılan kapsayan bir range: [x, y]
x...y # matematikte kullanılan kapsamayan bir range: [x, y)
```

Hangisinin kapsayan olduğunu ve hangisinin kapsamayan olduğunu hatırlamanın kolay bir yolu, ekstra noktayı *y* uzağa iterek sanki aralık dışında bırakılmış gibi düşünmesini sağlamaktır.
