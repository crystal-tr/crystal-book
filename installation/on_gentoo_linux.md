# Gentoo Linux'da

Gentoo Linux, ana katmanında Crystal derleyicisini içerir.

## Yapılandırma

Önce mevcut yapılandırma flaglarına göz atmak isteyebilirsiniz:

```
# equery u dev-lang/crystal
[ Legend : U - final flag setting for installation]
[        : I - package is installed with flag     ]
[ Colors : set, unset                             ]
 * Found these USE flags for dev-lang/crystal-0.18.7:
 U I
 - - doc      : Add extra documentation (API, Javadoc, etc). It is recommended to enable per package instead of globally
 - - examples : Install examples, usually source code
 + + xml      : Use the dev-libs/libxml2 library to enable Crystal xml module
 + - yaml     : Use the dev-libs/libyaml library to enable Crystal yaml module
```

## Kurulum

```
su -
emerge -a dev-lang/crystal
```
