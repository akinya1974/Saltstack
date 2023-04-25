# Saltstack Акиньшин С.Г.




## Выполнение Задания -1

1. `Создал три тачки с OS Astra Linux (Community Edition).`

2. `Установил Saltstack(master) на одну машину и Saltstack minion на две других машины`

3. `Натроил подключение между ними`


![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG/Создал%20машины-1.jpg)

![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG/Создал%20машины-2.jpg)

![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG/IP.jpg)

![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG/Статус%20Master.jpg)

![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG/Статус%20Minion.jpg)

![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG/Статус%20ключей.jpg)

![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG/Ping%20minions.jpg)



## Выполнение Задание-2

1. `Скачал Nginx на мастер и скопировал его на миньоны.`

2. `Установил Nginx на миньоны.`

3. `Подменил текс старотовой страницы Nginx.`

4. `См. Комманды Bash ниже.`

![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG2/Установка%20NGINX.jpg)

![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG2/Установка%20NGINX-2.jpg)

![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG2/NGINX%20Status.jpg)

![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG2/Nginx%20run-1.jpg)

![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG2/Nginx%20run-2.jpg)

![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG2/Стартовая%20страница!.jpg)

![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG2/Nginx%20finish-1.jpg)

![Link](https://github.com/akinya1974/Saltstack/blob/main/JPG2/Nginx%20finish-2.jpg)


### СКРИПТЫ:

```
#Все комманды выполняются на мастере!

#Копируем архив с Nginx на миньоны

salt-cp '*' nginx-1.24.0.tar.gz /root/tmp

#Загружаем ключ для подписи Nginx на миньоны

salt '*' cmd.run 'sudo wget https://nginx.org/keys/nginx_signing.key'

#Устанавливаем утилиту gnupg2 что бы в дальнейшем добавить скаченный ключ на миньоны

salt '*' cmd.run 'sudo apt update'
salt '*' cmd.run 'sudo apt install -y gnupg2'

#Добавляем загруженный ключ в список программных ключей на миньонах

salt '*' cmd.run 'sudo apt-key add nginx_signing.key'

#Устанавливаем Nginx на миньоны

salt '*' cmd.run 'sudo apt update'
salt '*' cmd.run 'sudo apt install -y nginx'

#Запускаем Nginx и добавляем его в автозагрузку на миньонах

salt '*' cmd.run 'sudo systemctl start nginx'
salt '*' cmd.run 'sudo systemctl enable nginx'

#Проверяем статус сервиса на миньонах

salt '*' cmd.run 'sudo systemctl status nginx'

#Считываю и копирую содержимое файла стартотовой страницы на миньонах!

salt '*' cmd.run 'cat /var/www/html/index.nginx-debian.html'

#Создал файл начальной странички на мастере и вставил туда нужную и измененную информаацию скопированную из файла стартовой странички миньона! 

nano index.nginx-debian.html

#Скопировал файл начальной страницы из мастера на миньоны!

salt-cp '*' index.nginx-debian.html /var/www/html

#Получил нужный результат!)

#Понимаю, что все это можно сделать с помощью файлов состояний Salt master с расширением .sls, но пока не хватает практики, поскольку не изучал ранее данную технологию, а времени мало, к сожалению((!

```
