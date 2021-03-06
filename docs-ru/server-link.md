# Соединение с сервером

## Введение

Некоторые функции, такие как отображение игроков онлайн или
выполнение команды, требуют, чтобы Вы связали свой сервер с вашим
сайтом. На Azuriom это можно сделать тремя разными способами:

* By Ping - **Этото самое простое, но и самое ограниченное решение**, которое позволяет получить 
лить информацию об игроках на сервере. _(но не позволяет выполнять команды)_

* By Rcon - **Это решение является чем-то средним**, это позволяет Вам получить информацию
о вашем сервере и выполнять команды.

* By Plugin - **Наиболее оптимальное решение**, оно позволит Вам иметь функционал Rcon 
но на более продвинутом уровне _(пример: усовершенствованная система статистики)_

## Соединение через Ping

Чтобы иметь возможность связать ваш сервер с вашим сайтом в Azuriom с помощью пинга,
Вам просто нужно добавить новый сервер с «Ping» в качестве типа ссылки.
и заполнить запрашиваемую информацию_(дефолтный порт Minecraft-`25565`)_.

## Соединение через Rcon

Чтобы иметь возможность связать ваш сервер с вашим сайтом в Azuriom через Rcon, 
Вы должны:

1. Перейти на файл `server.properties` вашего сервера

2. Настроить файл следующим образом:
    * Задать `enable-rcon` зачение `true`.
    * Установить `rcon.password` на `your-password`.
    * Установить `rcon.port` на `your-port` _(default `25575`)_
    * Сделать бэкап и перезагрузить сервер
   
3. Перейдите на ваш сайт и добавьте новый сервер с типом ссылки "Rcon"
и заполните требуемую информацию. _(дефолтный Rcon порт-`25575`)_.

## Соединение через Plugin 

### Что такое AzLink ?

AzLink - это плагин для связи сайтов с серверами, разработанный специально для Azuriom,
позволяющий просто, быстро и безопасно связать свой сервер с сайтом.

В настоящее время AzLink поддерживает Bukkit, BungeeCord, Sponge и Velocity в одном плагине. Версия "legacy" доступна
для Bukkit 1.7.10.

### Установка

1. Скачайте AzLink по ссылке [our site](https://azuriom.com/azlink)

2. Установите его в папке`plugin/` и перезапустите сервер.

3. Перейдите на ваш сайт и добавьте новый сервер с типом ссылки "AzLink", 
следуйте указаниям по ссылке и заполните необходимую информацию.
