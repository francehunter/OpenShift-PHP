PHP "Hello, World!" application for OpenShift.

OpenShift - облачный сервис для сборки и поставки приложений в контексте docker + kubernetes.

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

