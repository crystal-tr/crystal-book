# Windows'taki Ubuntu'da Bash'de

Crystal _henüz_ Windows'u desteklemiyor, lakin eğer Windows 10 kullanıyorsanız, Crystal'i [Windows'taki Ubuntu'da Bash'de](https://msdn.microsoft.com/en-us/commandline/wsl/about) kullanarak deneyebilirsiniz(deneysel olarak). Deneysel bir Bash ortamı Windows'ta çalışmakta. Kurulum talimatları [Debian/Ubuntu](on_debian_and_ubuntu.md) ile aynı, ama dikkat edilmesi gereken birkaç pürüzlü noktalar bulunmaktadır.

Unutmayın - **bu son derece deneysel**.

## Reponun kurulumu

İlk olarak repoyu APT yapılandırmasına eklemeniz gerekmektedir. Kolay bir kurulum için komut satırında çalıştırın:

```
curl -sSL https://dist.crystal-lang.org/apt/setup.sh | sudo bash
```


Bu işlem imzalama anahtarı ve repo yapılandırmasını ekleyecektir. Eğer elle yapmayı tercih ederseniz aşağıdaki komutları çalıştırın:

```
sudo apt-key adv --keyserver keys.gnupg.net --recv-keys 09617FD37CC06B54
echo "deb https://dist.crystal-lang.org/apt crystal main" | sudo tee /etc/apt/sources.list.d/crystal.list
sudo apt-get update
```

## Bağımlılıklar
Crystal, Crystal programlarını derleyebilmek için bir C derleyicisine (`cc`) ve bağlayıcısına (`ld`) ihtiyaç duyar, bu yüzden bunları yüklemelisiniz:

```
sudo apt-get install clang binutils
```

## Kurulum
Depo yapılandırıldıktan ve bağımlılıkları halledildikten sonra, Crystal'i yüklemeye hazırsınızdır:

```
sudo apt-get install crystal
```

## Yükseltme

Yeni bir Crystal versiyonu yayınlandığında, sisteminizi yeni sürüme yükseltebilirsiniz:

```
sudo apt-get update
sudo apt-get install crystal
```
