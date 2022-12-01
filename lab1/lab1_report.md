University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)

Year: 2022/2023

Group: K4111c

Author: Maltseva Arina Sergeevna

Lab: Lab1

Date of create: 28.10.2022

Date of finished: 01.12.2022

---
# Лабораторная работа №1 "Установка Docker и Minikube, мой первый манифест."

1. Docker and minikube installed successfully.
 
```
minikube start
```
запуск minikube
 
 
создание ресурсов kuberntes из манифеста

apply управляет приложениями с помощью файлов, которые определяют ресурсы Kubernetes. 
 
<img width="572" alt="Снимок экрана 2022-12-01 в 14 38 19" src="https://user-images.githubusercontent.com/79594454/205071748-3d753691-4a2b-4b03-8592-da8131a47393.png">

Вывести все поды в пространстве имён

<img width="572" alt="Снимок экрана 2022-12-01 в 14 36 38" src="https://user-images.githubusercontent.com/79594454/205071770-e4a45e90-3981-4a8b-adb7-92e5ff3079d2.png">


По логам нужно получить токен для входа на сервис. Токен можно найти, используя команду
```
minikube kubectl -- logs service/vault 
```  

Далее нужно перенаправить локальный порт на порт в поде
```
minikube kubectl -- port-forward service/vault 8200:8200
```
Теперь приложение становится доступным по адресу http://localhost:8200 

#Результат работы
<img width="1440" alt="Снимок экрана 2022-12-01 в 14 56 55" src="https://user-images.githubusercontent.com/79594454/205072270-696087f0-52f7-4220-8c4f-0ba1e8329361.png">




