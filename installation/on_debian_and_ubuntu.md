# Debian ve Ubuntu'da

Debian kaynaklı dağıtımlarda resmi Crystal reposu kullanabilirsiniz.

## Reponun kurulumu

İlk olarak repoyu APT yapılandırmasına eklemeniz gerekmektedir. Kolay bir kurulum için komut satırında çalıştırın:

```
curl https://dist.crystal-lang.org/apt/setup.sh | sudo bash
```

Bu işlem imzalama anahtarı ve repo yapılandırmasını ekleyecektir. Eğer elle yapmayı tercih ederseniz, aşağıdaki komutları *root* olarak çalıştırın:

```
apt-key adv --keyserver keys.gnupg.net --recv-keys 09617FD37CC06B54
echo "deb https://dist.crystal-lang.org/apt crystal main" > /etc/apt/sources.list.d/crystal.list
apt-get update
```

## Kurulum

Depo yapılandırıldıktan sonra Crystal'ı yüklemeye hazırsınız:

```
sudo apt-get install crystal
```

Bazen Crystal programlarını çalıştırmak/derlemek için `build-essential` paketine [ihtiyacınız olacak](https://github.com/crystal-lang/crystal/issues/4342). Buradaki komut ile kurabilirsiniz:

```
sudo apt-get install build-essential
```


## Yükseltme

Yeni bir Crystal versiyonu yayınlandığında, sisteminizi yeni sürüme yükseltebilirsiniz:

```
sudo apt-get update
sudo apt-get install crystal
```
