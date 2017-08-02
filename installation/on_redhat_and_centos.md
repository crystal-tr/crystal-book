# RedHat ve CentOS'da

RedHat kaynaklı dağıtımlarda resmi Crystal reposu kullanabilirsiniz.

## Reponun kurulumu

İlk olarak repoyu YUM yapılandırmasına eklemeniz gerekmektedir. Kolay bir kurulum için komut satırında çalıştırın:

```
curl https://dist.crystal-lang.org/rpm/setup.sh | sudo bash
```

Bu işlem imzalama anahtarı ve repo yapılandırmasını ekleyecektir. Eğer elle yapmayı tercih ederseniz aşağıdaki komutları çalıştırın:

```
rpm --import https://dist.crystal-lang.org/rpm/RPM-GPG-KEY

cat > /etc/yum.repos.d/crystal.repo <<END
[crystal]
name = Crystal
baseurl = https://dist.crystal-lang.org/rpm/
END
```

## Kurulum
Depo yapılandırıldıktan sonra Crystal'ı yüklemeye hazırsınız:

```
sudo yum install crystal
```

## Yükseltme

Yeni bir Crystal versiyonu yayınlandığında, sisteminizi yeni sürüme yükseltebilirsiniz:

```
sudo yum update crystal
```
