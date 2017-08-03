# HTTP Sunucusu

Biraz daha ilginç bir örnek, bir HTTP sunucusudur:

```crystal
require "http/server"

server = HTTP::Server.new(8080) do |context|
  context.response.content_type = "text/plain"
  context.response.print "Hello world! The time is #{Time.now}"
end

puts "Listening on http://127.0.0.1:8080"
server.listen
```

Bütün dokümantasyonu okuduktan sonra yukarıdaki kod anlamlı olacaktır, ancak biz zaten bazı şeyler öğrenebiliriz.

* Dosyada [require](../syntax_and_semantics/requiring_files.html) kullanarak  başka dosyalarda tanımlanmış kodları dahil edebilirsiniz:

    ```ruby
    require "http/server"
    ```
* Tipini belirtmek zorunda kalmadan, [yerel değişkenler](../syntax_and_semantics/local_variables.html) tanımlayabilirsiniz:

    ```ruby
    server = HTTP::Server.new ...
    ```

* [Methodlar](../syntax_and_semantics/classes_and_methods.html)'ı objelere çalıştırarak (yada mesaj göndererek) programlarsınız:

    ```ruby
    HTTP::Server.new(8080) ...
    ...
    Time.now
    ...
    puts "Listening on http://127.0.0.1:8080"
    ...
    server.listen
    ```

* Kodun tekrar kullanmasını ve fonksiyonel alemden bazı özellikleri kullanılmasının çok uygun bir yolu olan, kod bloklarını veya yalnızca [blokları](../syntax_and_semantics/blocks_and_procs.html) kullanabilirsiniz:

    ```ruby
    HTTP::Server.new(8080) do |context|
      ...
    end
    ```

* Dize ara değerlemesi(string interpolation) olarak da bilinen gömülü içeriğe sahip dizeleri kolayca oluşturabilirsiniz. Dil'in [syntax](../syntax_and_semantics/literals.html)'ı arrayler, hashler, rangeler, tuplelar ve daha fazlası ile birlikte gelir:

    ```ruby
    "Hello world! The time is #{Time.now}"
    ```


