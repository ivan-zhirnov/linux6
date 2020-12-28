# linux6

## Задание  
1) Создать свой RPM пакет (можно взять свое приложение, либо собрать, например, nginx с определенными опциями);
2) Создать свой репозиторий и разместить там ранее собранный RPM.

## Выполнение  
1. Для примера возьмем пакет NGINX и соберем его с поддержкой openssl  
* Для данного задания нам понадобятся следующие установленные пакеты:  
![](https://sun9-69.userapi.com/impg/zr4MceeyOwrFyn5GPpc7PcgjRQY6jbVUsfw3fA/GfPpxeqOLZs.jpg?size=389x131&quality=96&proxy=1&sign=e31de6961001ae94f90d50cd5c94cb81&type=album)  
* Загрузим SRPM пакет NGINX для дальнейшей работы над ним:  
![](https://sun9-44.userapi.com/impg/WOmuJM3IZwEDWWWx6h6RQhGBclM_lgRYhUC5cA/G1Gs9T2KfYE.jpg?size=902x356&quality=96&proxy=1&sign=c7f3e4158d1fa04c0b57c5b5c423efac&type=album)  
* При установке такого пакета в домашней директории создается древо каталогов для сборки:  
![](https://sun9-22.userapi.com/impg/3RTG37EVSdwIwtp4n4SwMWlcKJ--lM_2kyhgHA/GnymcPWf5mg.jpg?size=905x72&quality=96&proxy=1&sign=d2848a8d505ff06128fae984b68efd8a&type=album)  
* Также нужно скачать и разархивировать последние исходники для openssl, т.к. они потребуется при сборке:  
![](https://sun9-33.userapi.com/impg/huoHJr5e6JoQSKVthF0KqSxTNzmXFQuzOrmT6Q/OQoG_x9J7zg.jpg?size=912x470&quality=96&proxy=1&sign=824dd076d2ccbfd831a6be3f4f16e7e9&type=album)  
* Заранее поставим все зависимости чтобы в процессе сборки не было ошибок:  
![](https://sun9-75.userapi.com/impg/07jRfWwrRvAzyF_0AB9OrYG7lQuanZ8D9-eBWw/W4PA_9aS7Uk.jpg?size=897x253&quality=96&proxy=1&sign=6ef2451f4a8599ff574438c9f6176a42&type=album)  
* Ну и собственно поправить сам spec файл чтобы NGINX собирался с необходимыми нам опциями:  
![](https://sun9-66.userapi.com/impg/FVNpePyi7RNKtMTjUVwbPiO3HeruMmxbt2a3IA/D4SGKC2immc.jpg?size=917x623&quality=96&proxy=1&sign=7c1660852ce3bd4fd4ec0279cf252fc4&type=album)  
* Теперь можно приступить к сборке RPM пакета:  
![](https://sun9-73.userapi.com/impg/BTCDCeastQ-UOduJOgG0rV8kmj2OMuwoFzjiyw/TjPb7AlbkJs.jpg?size=909x235&quality=96&proxy=1&sign=eff457460913b161e8c12ad9c0317cf7&type=album)  
* Убедимся что пакеты создались:  
![](https://sun9-35.userapi.com/impg/P-j4s8v0905rAsdfVrMCQ-zJG3UETUaWEfeowA/_5rXwKXUvgM.jpg?size=908x158&quality=96&proxy=1&sign=11a06a1e70195849745f8edfd7c39192&type=album)  
* Теперь можно установить наш пакет и убедиться что nginx работает:  
![](https://sun1-83.userapi.com/impg/nwJgLRLSodMUNrAyI5tnimfXVW81Z6xsTa-1cg/9sUgQLkgVXA.jpg?size=1122x343&quality=96&proxy=1&sign=76bf0c526105e8b53083c89c690f54a0&type=album)  
Далее мы будем использовать его для доступа к своему репозиторию  
2. Теперь приступим к созданию своего репозитория.  
Директория для статики у NGINX по умолчанию /usr/share/nginx/html  
* Создадим там каталог repo:  
`mkdir /usr/share/nginx/html/repo`  
* Копируем туда наш собранный RPM и, например, RPM для установки репозитория Percona-Server:  
![](https://sun9-12.userapi.com/impg/R2BY1KQqFS3BUucPmr6GDKUUcz4-7lz6xSBP_w/Mq5fKtrRL_k.jpg?size=1271x444&quality=96&proxy=1&sign=cd3e5c42f148926b04af020600723f95&type=album)  
* Инициализируем репозиторий командой:  
![](https://sun9-45.userapi.com/impg/lqMD-avJZojeU5lA9HetPlXPqg7OQHmaWHDY8A/RcmI4VSggYg.jpg?size=743x165&quality=96&proxy=1&sign=1873eeb6b4b0cee105a2bb78a1da47bc&type=album)  
* Для прозрачности настроим в NGINX доступ к листингу каталога:
В location / в файле /etc/nginx/conf.d/default.conf добавим директиву autoindex on. В результате location будет выглядеть так:
![](https://sun9-52.userapi.com/impg/Im_d4C2epvW9tEmCzyRI3y33ZS8nZ7We1N3p0w/8WTwgsim7zk.jpg?size=809x553&quality=96&proxy=1&sign=30594c32adbd9d78b51ddbe546c4beca&type=album)  
* Проверяем синтаксис и перезапускаем NGINX:  
![](https://sun9-55.userapi.com/impg/4wrqJ9GoLwYIn0fre7MsyLBp0SGhfcdcmuaZNA/GHqVnTW-sKA.jpg?size=796x100&quality=96&proxy=1&sign=16b5e1769cd96ba289a68326191d6996&type=album)  
* Теперь ради интереса можно посмотреть в браузере или curl-ануть:  
![](https://sun9-19.userapi.com/impg/z-37U-xXr-VQguekv0hNrqYkmFsiUQEcKFs_7Q/qMFWd3h0SWw.jpg?size=1039x300&quality=96&proxy=1&sign=48951eec2cc7ec65456e78b2a80210ee&type=album)  
* Все готово для того, чтобы протестировать репозиторий! Добавим его в /etc/yum.repos.d:  
![](https://sun9-45.userapi.com/impg/QBHkMYaoq0C9cswLNf3V1JACJABaafBCCo86ZQ/CI6fqq-8mW0.jpg?size=705x159&quality=96&proxy=1&sign=0b997d2856381f240ee09f0cd45c0b63&type=album)  
* Убедимся что репозиторий подключился и посмотрим что в нем есть:  
![](https://sun9-18.userapi.com/impg/IxZP6spaMg19Le9bFaTjZ-J5S1nDFP83EH5B9g/sugo-ERzZYA.jpg?size=597x52&quality=96&proxy=1&sign=7757b89871ad5c77904b52faccdc9ff6&type=album)  
* Переустановим nginx из нашего репозитория:  
![](https://sun9-16.userapi.com/impg/s72prbIyBWqJn8TXir8i7TUWRKlqvzYiuLFsYQ/0HcGIfdlUjI.jpg?size=566x226&quality=96&proxy=1&sign=ae18c5edbba471072ff3e7fec76867c1&type=album)  
* Посмотрим список всех пакетов, отфильтровав их:  
![](https://sun9-4.userapi.com/impg/bJt6rCjIdIgrf7rbQZXjVyMId8SvOGnc17OqEg/DB8GF9nDIIQ.jpg?size=1037x439&quality=96&proxy=1&sign=c7b2ca4253aae31a60f691b0b731ceef&type=album)  
* Установим репозиторий percona-release из нашего репозитория:  
![](https://sun9-62.userapi.com/impg/9r-RPthfByq-NncZo90HXRqqH-k8kt3siSAzwg/ShKBzrA6XAE.jpg?size=809x278&quality=96&proxy=1&sign=a3b2892bb6e057fdbdfff9459e45a2b0&type=album)  

