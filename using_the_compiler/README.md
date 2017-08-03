# Derleyiciyi kullanma

Bir defa [kurduğunuz zaman](../installation/README.md) derleyici, elinizin altında `crystal` şeklinde bir binary olacak.

Önümüzdeki bölümlerde (`$`) işareti komut satırı anlamına gelmektedir.

## Derleme and bir defa çalıştırmak

Bir programı `crystal` ile dosya ismini yazarak çağırıp derleyip çalıştırabilirsiniz:

```
$ crystal some_program.cr
```

Crystal dosyaları `.cr` uzantısı ile biter.

Alternatif olarak `run` komutunu da kullanabilirsiniz:

```
$ crystal run some_program.cr
```

## Bir yürütülebilir(executable) oluşturma

Bir yürütülebilir(executable) oluşturmak için `build` komutu kullanılır:

```
$ crystal build some_program.cr
```

Bu işlem sonunda çalıştırabileceğiniz `some_program` dosyası oluşturulacak:

```
$ ./some_program
```

**Not:** Varsayılan olarak, oluşturulan yürütülebilir **tamamen optimize edilmemiştir**. Optimizasyonu etkinleştirmek için `--release` flagını kullanın:

```
$ crystal build some_program.cr --release
```

Kalite testi(benchmark) gerçekleştirirken ve üretime hazır(production-ready) yürütülebilir, her zaman `--release`'i kullandığınızdan emin olun.

Bunun nedeni, tam iyileştirmeler yapılmadan yapılan performansın hala oldukça iyi olması ve hızlı derleme zamanları sağlamasıdır, böylece `crystal` komutunu neredeyse bir yorumcu(interpreter) gibi kullanabilir.

## Proje veya kütüphane oluşturma

Standart dizin yapısıyla bir Crystal projesi oluşturmak için `init` komutunu kullanın:

```
$ crystal init lib my_cool_lib
      create  my_cool_lib/.gitignore
      create  my_cool_lib/LICENSE
      create  my_cool_lib/README.md
      create  my_cool_lib/.travis.yml
      create  my_cool_lib/shard.yml
      create  my_cool_lib/src/my_cool_lib.cr
      create  my_cool_lib/src/my_cool_lib/version.cr
      create  my_cool_lib/spec/spec_helper.cr
      create  my_cool_lib/spec/my_cool_lib_spec.cr
Initialized empty Git repository in ~/my_cool_lib/.git/
```

## Diğer komutlar ve seçenekler

Komut setinin tümünü görüntülemek için, argümanlar olmadan `crystal` komutunu çalıştırın:

```
$ crystal
Usage: crystal [command] [switches] [program file] [--] [arguments]

Command:
    init                     generate a new project
    build                    build an executable
    deps                     install project dependencies
    docs                     generate documentation
    env                      print Crystal environment information
    eval                     eval code from args or standard input
    play                     starts crystal playground server
    run (default)            compile and run program
    spec                     compile and run specs (in spec directory)
    tool                     run a tool
    help, --help, -h         show this help
    version, --version, -v   show version
```

Belirli bir komut için mevcut seçenekleri görmek için, bir komuttan sonra `--help`'i kullanın:

```
$ crystal build --help
Usage: crystal build [options] [programfile] [--] [arguments]

Options:
    --cross-compile                  cross-compile
    -d, --debug                      Add symbolic debug info
    -D FLAG, --define FLAG           Define a compile-time flag
    --emit [asm|llvm-bc|llvm-ir|obj] Comma separated list of types of output for the compiler to emit
    -f text|json, --format text|json Output format text (default) or json
    -h, --help                       Show this message
    --ll                             Dump ll to .crystal directory
    --link-flags FLAGS               Additional flags to pass to the linker
    --mcpu CPU                       Target specific cpu type
    --no-color                       Disable colored output
    --no-codegen                     Don't do code generation
    -o                               Output filename
    --prelude                        Use given file as prelude
    --release                        Compile in release mode
    -s, --stats                      Enable statistics output
    --single-module                  Generate a single LLVM module
    --threads                        Maximum number of threads to use
    --target TRIPLE                  Target triple
    --verbose                        Display executed commands
```
