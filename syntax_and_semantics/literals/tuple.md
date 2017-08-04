# Tuple

Bir [Tuple](http://crystal-lang.org/api/Tuple.html) genellikle bir tuple literali ile oluşturulur:

```crystal
tuple = {1, "hello", 'x'} # Tuple(Int32, String, Char)
tuple[0]                  #=> 1       (Int32)
tuple[1]                  #=> "hello" (String)
tuple[2]                  #=> 'x'     (Char)
```

Boş bir tuple oluşturmak için [Tuple.new](http://crystal-lang.org/api/Tuple.html#new%28%2Aargs%29-class-method) kullanabilirsiniz.

Bir tuple tipi belirtmek için aşağıdakini yazabilirsiniz:

```crystal
# The type denoting a tuple of Int32, String and Char
Tuple(Int32, String, Char)
```

Tip kısıtlamalarında, jenerik tipteki argümanlar ve bir tipin beklendiği diğer yerlerde, [tip grameri](../type_grammar.html)'nde açıklandığı gibi, daha kısa bir sözdizimi kullanabilirsiniz:

```crystal
# An array of tuples of Int32, String and Char
Array({Int32, String, Char})
```
