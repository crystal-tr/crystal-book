# NamedTuple


Bir [NamedTuple](http://crystal-lang.org/api/NamedTuple.html) genellikle bir tuple literaliyle oluşturulur:

```crystal
tuple = {name: "Crystal", year: 2011} # NamedTuple(name: String, year: Int32)
tuple[:name] # => "Crystal" (String)
tuple[:year] # => 2011      (Int32)
```

Bir named tuple tipini belirtmek için aşağıdakini yazabilirsiniz:

```crystal
# Bir x: Int32, y: String 'den oluşan named tuple'ın gösterimi 
NamedTuple(x: Int32, y: String)
```

Tip kısıtlamalarında, jenerik tipteki argümanlar ve bir tipin beklendiği diğer yerlerde, [tip grameri](../type_grammar.html)'nde açıklandığı gibi, daha kısa bir sözdizimi kullanabilirsiniz:

```crystal
# Bir x: Int32, y: String 'den oluşan named tuple arrayi 
Array({x: Int32, y: String})
```

Bir name tuple anahtarı aynı zamanda string literali de olabilir:

```crystal
{"this is a key": 1}
```
