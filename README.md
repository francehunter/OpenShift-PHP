PHP "Hello, World!" application for OpenShift.

OpenShift - облачный сервис для сборки и поставки приложений в контексте docker + kubernetes.
Во вкладке topology есть все доступные апликейшены. Для приложения можно выбрать кол-во подов. Можно балансировать поды горизонтально на основании проб процессора и оперативной памяти.

Пишем простое приложение.
1) Регистрируем триал, заходим https://console-openshift-console.apps.sandbox.x8i5.p1.openshiftapps.com/add/ns/francehunter-dev
2) Во владке add добавляем ссылку на репозиторий гит
3) Во вкладке topology Нажимаем build, ждем, кликаем на open url.
4) В новой вкладке браузера открывается стрваничка как результат работы php

Забираем из облака:
1) В ubuntu устанавливаем docker: sudo apt-get install docker
2) Клонируем образ из облака docker pull registry.access.redhat.com/ubi8/php-74:1-24
3)  sudo docker images говорит, что репозиторий присутствует
REPOSITORY                               TAG       IMAGE ID       CREATED       SIZE
registry.access.redhat.com/ubi8/php-74   1-24      576cf8beb829   7 weeks ago   742MB

Глоссарий:

Pod - докер контейнер, в котором выполяется образ.

S2I - source-to-image - конвертор исходников в образ докера.

Liveness Probe - регулярные проверки контейнера на жизнедеятельность. Провал проверки приводит к реализиции политики рестарта. Конфигурятся как команда, выполняемая внутри контейнера (можно написать парсер статуса демона в стиле systemctl status myDaemonName | grep "ready").

Readiness Probe - регулярные проверки контейнера на выполнение реквестов. Провал проверки приводит к исключению ip контейнера из балансировки round robin dns. Конфигурятся как урл, порт и таймаут; либо сокет+порт.

Job - объект для запуска подов по шаблону. Конфигурится количество подов, время из жизни и политика рестартов.

Cron Job - планировщик запуска джобов.

Build - изготовление и размещение образов для подов. Источниками постороения билдов могут быть: git (сырцы из гита), Dockefile, image и binary (все из указанного пути). Можно писать обработчики (запускать тесты, собирать артефакты). Упарвляется конфигом. Стратегия билда может быть: forcepull - все переделать с нуля; incremental - ? (ничего не понятно, но очень интересно).

Rolling Deployment - стратегия развертки новых версий.

Route - проброс трафика. Между сервисом и заданным хостом+портом.

A/B testing - запуск двух версий приложения для определения лучшей.

Secret - хранилище приватных данных, которое можно поставлять на поды, примаунтив их. Маунтинг в фолдер прописывается в билд конфиге.

Testing - тестирование билдов после сборки. Хорошей практикой счиатется прописывать в конфигах пост хуки - команды, вызываемые после успешного завершения билда, запускающие автотесты (1.TTD 2... 3.PROFIT).
