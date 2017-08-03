# Char

Bir [Char](http://crystal-lang.org/api/Char.html), bir [Unicode](http://en.wikipedia.org/wiki/Unicode) [kod noktası](http://en.wikipedia.org/wiki/Code_point)'nı temsil eder.
32 bitlik yer kaplar.

Bir UTF-8 karakterini tek tırnak içine alınca oluşturulur.

```crystal
'a'
'z'
'0'
'_'
'あ'
```

Bazı özel karakterleri belirtmek için ters eğik çizgi(`\`) kullanabilirsiniz:

```crystal
'\'' # tek tırnak(single quote)
'\\' # ters eğik çizgi(backslash)
'\e' # kaçış(escape)
'\f' # sayfa ilerletme(form feed)
'\n' # yeni satır(newline)
'\r' # satırbaşı(carriage return)
'\t' # sekme(tab)
'\v' # dikey sekme(vertical tab)
```


Yazılmış bir unicode kod noktasını belirtmek için bir ters eğik çizgi ile ardından bir *u* ve dört onaltılık karakter kullanabilirsiniz:

```crystal
'\u0041' # == 'A'
```

Veya açıkça belirtmek için süslü parantez ile birlikte 6 onaltılık sayıya kadar kullanabilirsiniz (0'dan 10FFFF'e kadar):

```crystal
'\u{41}'    # == 'A'
'\u{1F52E}' # == '🔮'
```
