University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)

Year: 2022/2023

Group: K4111c

Author: Maltseva Arina Sergeevna

Lab: Lab2

Date of create: 28.10.2022

Date of finished: 08.12.2022

---
# Лабораторная работа №2 "Развертывание веб сервиса в Minikube, доступ к веб интерфейсу сервиса. Мониторинг сервиса."


## Ход работы

- Вам необходимо создать deployment с 2 репликами контейнера ifilyaninitmo/itdt-contained-frontend:master и передать переменные в эти реплики: REACT_APP_USERNAME, REACT_APP_COMPANY_NAME.

- Создать сервис через который у вас будет доступ на эти "поды". Выбор типа сервиса остается на ваше усмотрение.

- Запустить в minikube режим проброса портов и подключитесь к вашим контейнерам через веб браузер.

- Проверьте на странице в веб браузере переменные REACT_APP_USERNAME, REACT_APP_COMPANY_NAME и Container name. Изменяются ли они? Если да то почему?

- Проверьте логи контейнеров, приложите логи в отчёт.

---
Для развертывания deployment используем следующую команду:

 ```
minikube kubectl -- apply -f deployment.yaml
 ```
 
### Создание сервиса типа NodePort

Для предоставления доступа к подам деплоймента lab2 был создан манифест service.yaml для создания сервиса типа NodePort.

Сервисы в Kubernetes позволяют определить набор подов и правила доступа к ним. С помощью сервисов разные части приложения могут "общаться" друг с другом (например, фронтенд с бэкендом).

Для создания описанного в манифесте сервиса была использована следующая команда:
 ```
 minikube kubectl -- apply -f service.yaml
  ```
  
### Проброс портов и результаты работы
С помощью комманды
 ```
 minikube kubectl -- port-forward service/lab2 8888:8080
  ```
  Открываем порт для доступа к сервису и заходим через браузер в приложение:
  
  picture
  
  Имя и IP контейнера не меняются т.к. в качестве сервиса был выбран NodePort.
