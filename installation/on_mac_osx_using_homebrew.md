# Mac OSX'de Homebrew kullanarak

Crystal'ı Mac'de kolayca kurmak için [Homebrew](http://brew.sh/) kullanabilirsiniz.

```
brew update
brew install crystal-lang
```

Dilin kendisine katkıda bulunmayı planlıyorsanız, LLVM'i de kurmanız yararlı olabilir. Son satırı aşağıdaki ile değiştirin:

```
brew install crystal-lang --with-llvm
```

## OSX 10.11 üzerinde sorun giderme (El Capitan)

Eğer aşağıdaki gibi bir hata alıyorsanız:

```
ld: library not found for -levent
```

Komut satırı araçlarını yeniden yüklemeniz ve ardından varsayılan etkin araç zincirini seçmeniz gerekir:

```
$ xcode-select --install
$ xcode-select --switch /Library/Developer/CommandLineTools
```
