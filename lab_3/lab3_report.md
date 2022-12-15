University: ITMO University

Faculty: FICT

Course: Introduction to distributed technologies

Year: 2022/2023

Group: K4111c

Author: Maltseva Arina Sergeevna

Lab: Lab3

Date of create: 08.12.2022

Date of finished: 15.12.2022

# Лабораторная работа №3 "Сертификаты и "секреты" в Minikube, безопасное хранение данных."

### Цель работы:
Познакомиться с сертификатами и "секретами" в Minikube, правилами безопасного хранения данных в Minikube.

### Ход работы:

1 Создать манифесты
configMap 
переменные: 
- REACT_APP_USERNAME
- REACT_APP_COMPANY_NAME
(ConfigMap — это объект API, используемый для хранения неконфиденциальных данных в парах ключ-значение.)

replicaSet 
(Цель ReplicaSet — поддерживать стабильный набор подов реплик, работающих в любой момент времени.)
использовать:
- контейнер - ifilyaninitmo/itdt-contained-frontend:master
- реплики - 2
- используя переменные среды configMap передаать переменные REACT_APP_USERNAME, REACT_APP_COMPANY_NAME




### далее 
Включить minikube addons enable ingress и сгенерировать TLS сертификат, импортировать сертификат в minikube.

Создать ingress в minikube, где указан ранее импортированный сертификат, FQDN по которому вы будете заходить и имя сервиса который вы создали ранее.

В hosts пропишите FQDN и IP адрес вашего ingress и попробуйте перейти в браузере по FQDN имени.

Войдите в веб приложение по вашему FQDN используя HTTPS и проверьте наличие сертификата
