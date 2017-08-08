# Düzenli İfadeler(Regex)

Düzenli ifadeler genellikle bir literal ile oluşturulmuş [Regex](http://crystal-lang.org/api/Regex.html) sınıfıyla temsil edilir:

```crystal
foo_or_bar = /foo|bar/
heeello    = /h(e+)llo/
integer    = /\d+/
```

Bir düzenli ifade literali `/` ile sınırlandrılmıştır ve [PCRE](http://pcre.org/pcre.txt) sözdizimini kullanır.

Aşağıdaki düzenleyiciler de eklenebilir:

* i: yoksayma durumu(ignore case) (PCRE_CASELESS)
* m: çok satırlı(multiline) (PCRE_MULTILINE)
* x: genişletilmiş(extended) (PCRE_EXTENDED)

Örneğin

```crystal
r = /foo/imx
```

Slash(`/`)'ta her zaman kaçış uygulanmalı

```crystal
slash = /\//
```

Alternatif bir sözdizimi bulunmaktadır:

```crystal
r = %r(regex with slash: /)
```
