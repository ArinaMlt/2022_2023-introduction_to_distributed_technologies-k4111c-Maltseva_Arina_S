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

(ConfigMap — это объект API, используемый для хранения неконфиденциальных данных в парах ключ-значение)

<img width="165" alt="Снимок экрана 2022-12-15 в 07 28 18" src="https://user-images.githubusercontent.com/79594454/207772606-4a3d779f-603e-44a3-a1af-8a18f37d5fdf.png">

 ```
minikube kubectl -- apply -f configMap.yaml
  ```
  
  
replicaSet 
(Цель ReplicaSet — поддерживать стабильный набор подов реплик, работающих в любой момент времени)
использовать:
- контейнер - ifilyaninitmo/itdt-contained-frontend:master
- реплики - 2
- используя переменные среды configMap передаать переменные REACT_APP_USERNAME, REACT_APP_COMPANY_NAME
```
minikube kubectl -- apply -f replicaSet.yaml
  ```
<img width="464" alt="Снимок экрана 2022-12-15 в 07 28 43" src="https://user-images.githubusercontent.com/79594454/207772648-8ab006a3-18ae-45cc-9698-b7d913d5d7eb.png">

  
service 
```
minikube kubectl -- apply -f service.yaml
  ```
<img width="597" alt="Снимок экрана 2022-12-15 в 06 19 22" src="https://user-images.githubusercontent.com/79594454/207764629-dcc3570b-5055-43a0-8728-abd04e92588a.png">

<img width="781" alt="Снимок экрана 2022-12-15 в 06 24 27" src="https://user-images.githubusercontent.com/79594454/207765200-596d68cb-c815-4f79-9859-8d267298658c.png">

<img width="776" alt="Снимок экрана 2022-12-15 в 06 29 45" src="https://user-images.githubusercontent.com/79594454/207765827-10ff0805-f81d-4eb9-b61d-db9c1bc512be.png">


<img width="688" alt="Снимок экрана 2022-12-15 в 06 31 21" src="https://user-images.githubusercontent.com/79594454/207766047-a70f8015-a4af-42ef-beec-f743fd5a423b.png">

```
minikube addons enable ingress
minikube addons enable ingress-dns
  ```
  
<img width="778" alt="Снимок экрана 2022-12-15 в 06 33 43" src="https://user-images.githubusercontent.com/79594454/207766328-bfb1ecc7-1ce8-46c0-ae9b-4fdafda26ad2.png">




