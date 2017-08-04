# String

Bir [String](http://crystal-lang.org/api/String.html) değişmez bir UTF-8 karakterler dizisini temsil eder.

Bir string genellikle string literali ve UTF-8 karakterlerinin çift tırnak içine alınmasıyla oluşturulur.

```crystal
"hello world"
```

Ters eğik çizgi string içinde çeşitli özel karakterleri belirtmek için kullanılabilir:

```crystal
"\"" # çift tırnak(double quote)
"\\" # ters eğik çizgi(backslash)
"\e" # kaçış(escape)
"\f" # sayfa ilerletme(form feed)
"\n" # yeni satır(newline)
"\r" # satırbaşı(carriage return)
"\t" # sekme(tab)
"\v" # dikey sekme(vertical tab)
```

Ters eğik çizgiden (`\`) sonra en çok üç haneli bir sekizlik(octal) yazılmış bir kod noktası belirtmek için kullanabilirsiniz:

```crystal
"\101" # == "A"
"\123" # == "S"
"\12"  # == "\n"
"\1"   # kod noktası 1 olan bir karakterlik string
```

Unicode kod noktasını belirtmek için bir ters eğik çizgi ile ardından bir *u* ve dört onaltılık(hexadecimal) karakter kullanabilirsiniz:

```crystal
"\u0041" # == "A"
```

Veya açıkça belirtmek için süslü parantez ile birlikte 6 onaltılık(hexadecimal) sayıya kadar kullanabilirsiniz (0'dan 10FFFF'e kadar):

```crystal
"\u{41}"    # == "A"
"\u{1F52E}" # == "🔮"
```

A string can span multiple lines:

```crystal
"hello
      world" # same as "hello\n      world"
```

Yukarıdaki örnekte olduğu gibi başta ve sonra bulunan boşlukların yanı sıra yeni satırlar da neticede yine string oluşturur. Bundan kaçınmak için stringi bir çok satıra parçalayabilir ve ters eğik çizgi ile birbiriyle birleştirebilirsiniz:

```crystal
"hello " \
"world, " \
"no newlines" # "hello world, no newlines" ile aynı
```

Alternatif olarak, ters eğik çizgi ile string literalinin içine yeni bir satır eklenebilir:

```crystal
"hello \
     world, \
     no newlines" # "hello world, no newlines" ile aynı
```

Bu durumda, öndeki boşluk, sonuç stringinde bulunmaz.

Bir çok çift tırnak, parantez veya benzeri karakterler içeren bir string yazma gereksiniminiz var ise, alternatif literalleri aşağıdakiler gibi kullanabilirsiniz:

```crystal
# Çift tırnakları ve iç içe parantezleri destekler 
%(hello ("world")) # "hello (\"world\")" ile aynı

# Çift tırnakları ve iç içe köşeli parantezleri destekler 
%[hello ["world"]] # "hello [\"world\"]" ile aynı

# Çift tırnakları ve iç içe süslü parantezleri destekler 
%{hello {"world"}} # "hello {\"world\"}" ile aynı

# Çift tırnakları ve iç içe açılı parantezleri destekler 
%<hello <"world">> # "hello <\"world\">" ile aynı
```

## Heredoc

String oluşturmak için ayrıca "heredoc" da kullanabilirsiniz:

```crystal
<<-XML
<parent>
  <child />
</parent>
XML
```

Bir heredoc `<<-IDENT` ile başlar, `IDENT`, harfle başlamak zorunluluğu olan harflerden ve sayılardan oluşan bir dizi ve belirteçtir. Bu heredoc `IDENT` ile başlayan bir satırla biter, önce gelen beyaz boşlukları yoksayar ve ignoring leading whitespace ve ister yeni bir satır, ister alfanümerik olmayan bir karakter ardından gelebilir:

Sondaki nokta, heredoc'larda yöntem çağırmayı veya parantez içinde kullanmayı mümkün kılar:

```crystal
<<-SOME
hello
SOME.upcase # => "HELLO"

def upcase(string)
  string.upcase
end

upcase(<<-SOME
  hello
  SOME) # => "HELLO"
```

Öndeki beyaz boşluk, sondaki `IDENT`'teki beyaz boşluk sayısına göre  heredocun içeriğinden kaldırılır. Örneğin:

```crystal
# Same as "Hello\n  world"
<<-STRING
  Hello
    world
  STRING

# Same as "  Hello\n    world"
<<-STRING
    Hello
      world
  STRING
```

## Ara Değerleme(Interpolation)

Gömülü ifadeli bir string oluşturmak için ara değerleme kullanabilirsiniz:

```crystal
a = 1
b = 2
"sum = #{a + b}"        # "sum = 3"
```

`#{...}` ile kapatılmış her ifadede `Object#to_s(IO)` çalıştırılmış olur.

##  Ara değerleme(interpolation) veya kaçışlar(escape) olmadan

Ara değerleme veya kaçış olmadan string oluşturmak için `%q` kullanılır:

```crystal
%q(hello \n #{world}) # => "hello \\n \#{world}"
```

`%q(...)` için `{}`, `[]` ve `<>` sınır belirleyici olabilir.

Aynı özellikler heredocda da mevcuttur ve basitçe herodoc sınır belirleyicisini aşağıdaki gibi tek tırnak içine alarak kullanabiliriz.

```crystal
<<-'HERE'
hello \n #{world}
HERE
```
