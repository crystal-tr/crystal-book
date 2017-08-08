# responds_to?

'respond_to?' bir sözde metod(pseudo-method)'dur ve bir tipin belirli bir isme sahip bir metodu olup olmadığını belirler. Örneğin:

```crystal
a = 1
a.responds_to?(:abs)    #=> true
a.responds_to?(:size)   #=> false
```

'respond_to?' bir pseudo-method'dur çünkü argüman olarak sadece symbol literali alabilir ve ayrıca burada anlatıldığı şekilde [if var.responds_to?(...)](if_varresponds_to.html) derleyici tarafından özel olarak işlenir.
