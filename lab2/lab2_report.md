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


 <img width="568" alt="Снимок экрана 2022-12-08 в 15 38 17" src="https://user-images.githubusercontent.com/79594454/206474395-c23233a5-8eb9-4cdb-a6b8-f503c4a50818.png">
 
 <img width="485" alt="Снимок экрана 2022-12-08 в 17 47 25" src="https://user-images.githubusercontent.com/79594454/206476810-fd04dc2b-360f-4129-85aa-56113a006a2b.png">
 
Для развертывания deployment используем следующую команду:

 ```
minikube kubectl -- apply -f Deployment.yaml
 ```

Для предоставления доступа к подам деплоймента lab2 был создан манифест service.yaml для создания сервиса типа NodePort.

<!-- Сервисы в Kubernetes позволяют определить набор подов и правила доступа к ним. С помощью сервисов разные части приложения могут "общаться" друг с другом (например, фронтенд с бэкендом). -->

<img width="222" alt="Снимок экрана 2022-12-08 в 17 48 26" src="https://user-images.githubusercontent.com/79594454/206477037-52d0ce44-120d-4f33-85fd-5989a4c453dc.png">

Для создания описанного в манифесте сервиса была использована следующая команда:
 ```
 minikube kubectl -- apply -f service.yaml
  ```
  
  <img width="478" alt="Снимок экрана 2022-12-08 в 17 24 54" src="https://user-images.githubusercontent.com/79594454/206474641-d3e27caf-e2b7-48cf-9111-be2505c6fe25.png">

<img width="403" alt="Снимок экрана 2022-12-08 в 17 29 49" src="https://user-images.githubusercontent.com/79594454/206474678-3291628a-b3f8-4692-a406-898de2e02aef.png">


<img width="551" alt="Снимок экрана 2022-12-08 в 17 56 02" src="https://user-images.githubusercontent.com/79594454/206478871-7df4d64f-2d5b-42c0-9b47-f1c15cb50734.png">

  
### Проброс портов и результаты работы
С помощью комманды
 ```
 minikube kubectl -- port-forward service/lab2-service 8888:8080
  ```
 
  
  <img width="918" alt="Снимок экрана 2022-12-08 в 17 34 13" src="https://user-images.githubusercontent.com/79594454/206474194-a7effe86-97db-40ce-b5e8-004e4241cff5.png">

  
<!--   Имя и IP контейнера не меняются т.к. в качестве сервиса был выбран NodePort. -->

<img width="556" alt="Снимок экрана 2022-12-08 в 17 44 06" src="https://user-images.githubusercontent.com/79594454/206476184-d8819f69-6a55-455c-b7b0-58a47f5c1fc9.png">

