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

 <img width="568" alt="Снимок экрана 2022-12-08 в 15 38 17" src="https://user-images.githubusercontent.com/79594454/206474395-c23233a5-8eb9-4cdb-a6b8-f503c4a50818.png">

Для развертывания deployment используем следующую команду:

 ```
minikube kubectl -- apply -f Deployment.yaml
 ```
 
### Создание сервиса типа NodePort

Для предоставления доступа к подам деплоймента lab2 был создан манифест service.yaml для создания сервиса типа NodePort.

Сервисы в Kubernetes позволяют определить набор подов и правила доступа к ним. С помощью сервисов разные части приложения могут "общаться" друг с другом (например, фронтенд с бэкендом).

Для создания описанного в манифесте сервиса была использована следующая команда:
 ```
 minikube kubectl -- apply -f service.yaml
  ```
  
  <img width="478" alt="Снимок экрана 2022-12-08 в 17 24 54" src="https://user-images.githubusercontent.com/79594454/206474641-d3e27caf-e2b7-48cf-9111-be2505c6fe25.png">

<img width="403" alt="Снимок экрана 2022-12-08 в 17 29 49" src="https://user-images.githubusercontent.com/79594454/206474678-3291628a-b3f8-4692-a406-898de2e02aef.png">

  
### Проброс портов и результаты работы
С помощью комманды
 ```
 minikube kubectl -- port-forward service/lab2-service 8888:8080
  ```
 
  
  <img width="918" alt="Снимок экрана 2022-12-08 в 17 34 13" src="https://user-images.githubusercontent.com/79594454/206474194-a7effe86-97db-40ce-b5e8-004e4241cff5.png">

  
  Имя и IP контейнера не меняются т.к. в качестве сервиса был выбран NodePort.
