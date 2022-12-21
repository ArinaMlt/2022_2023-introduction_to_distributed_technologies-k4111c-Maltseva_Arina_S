University: ITMO University

Faculty: FICT

Course: Introduction to distributed technologies

Year: 2022/2023

Group: K4111c

Author: Maltseva Arina Sergeevna

Lab: Lab4

Date of create: 28.10.2022

Date of finished: is in development

---


### Цель работы

Познакомиться с CNI Calico и функцией IPAM Plugin, изучить особенности работы CNI и CoreDNS.

### Ход рааботы

1. Создать кластера
- Создать кластера с двумя нодами:

```
minikube start --nodes 2 --cni calico --kubernetes-version=v1.24.3
  ```
- проверка состояния nodes:
```
kubectl get nodes

NAME           STATUS   ROLES           AGE     VERSION
minikube       Ready    control-plane   11m     v1.24.3
minikube-m02   Ready    <none>          9m45s   v1.24.3
  ```
  <img width="692" alt="Снимок экрана 2022-12-21 в 18 45 39" src="https://user-images.githubusercontent.com/79594454/208945357-927b6824-2309-4294-80fc-9c236e6d2a85.png">

- проверить установку Calico в кластере, выполнив следующую команду:
```
arina@MacBook-Pro-Arina ~ % kubectl get pods -l k8s-app=calico-node -A 
NAMESPACE     NAME                READY   STATUS    RESTARTS   AGE
kube-system   calico-node-6l9lb   1/1     Running   0          22m
kube-system   calico-node-dlkbf   1/1     Running   0          23m
  ```

- проверить статус узлов:

```
arina@MacBook-Pro-Arina ~ % minikube status -p minikube
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

minikube-m02
type: Worker
host: Running
kubelet: Running
  ```

- Создать Calico pod
(позволяет управлять параметрами сети)

```
kubectl apply -f calico_ctl.yaml
```
<img width="459" alt="Снимок экрана 2022-12-21 в 19 14 25" src="https://user-images.githubusercontent.com/79594454/208951462-406df513-5486-4e78-9ff8-6e97b03add5b.png">

2. Создать ip-pools

<img width="241" alt="Снимок экрана 2022-12-21 в 19 38 19" src="https://user-images.githubusercontent.com/79594454/208957529-12683226-03bc-405d-b5f4-d13f5ed83580.png">

```
kubectl exec -i -n kube-system calicoctl -- /calicoctl create -f - < ip-pools.yaml
```
- Проверить созданные ippools

```
kubectl exec -i -n kube-system calicoctl -- /calicoctl get ippools -o wide
```
<img width="747" alt="Снимок экрана 2022-12-21 в 19 42 26" src="https://user-images.githubusercontent.com/79594454/208958360-e9bd0277-09f5-4b95-82af-0732b6478c8f.png">

<img width="369" alt="Снимок экрана 2022-12-21 в 19 44 40" src="https://user-images.githubusercontent.com/79594454/208958784-428f1cda-e4b7-49bd-aa1c-ccca058167d6.png">

-Удалить пул IP-адресов по умолчанию.
(Поскольку default-ipv4-ippoolресурс пула IP-адресов уже существует и учитывает весь /16 блок, нам придется сначала удалить это:)


```
kubectl delete ippools default-ipv4-ippool
```
<!-- kubectl exec -i -n kube-system calicoctl -- /calicoctl delete ippools default-ipv4-ippool -->

<img width="657" alt="Снимок экрана 2022-12-21 в 19 51 59" src="https://user-images.githubusercontent.com/79594454/208960315-46b20a32-482d-4342-9196-1f0cd7282847.png">

- Создать
  - configMap
  - replicaset
  - service

<img width="444" alt="Снимок экрана 2022-12-21 в 21 04 12" src="https://user-images.githubusercontent.com/79594454/208973635-9612afdd-cfec-445e-b708-3cf905b0ab4c.png">


3. Проверка на странице в веб браузере переменных Container name и Container IP

<img width="446" alt="Снимок экрана 2022-12-21 в 21 39 14" src="https://user-images.githubusercontent.com/79594454/208979304-7a16ef73-bc86-4e0a-8c83-d6ba972f47e7.png">

<img width="642" alt="Снимок экрана 2022-12-21 в 21 43 22" src="https://user-images.githubusercontent.com/79594454/208980038-871d65c5-5d7c-490a-b426-a4c0efe13e1c.png">



Обновив страницу не произошло изменение полей "Container name" и "Container IP".

4. Результаты пингов

```
minikube kubectl -- get pods -o wide
```

<img width="833" alt="Снимок экрана 2022-12-21 в 22 24 53" src="https://user-images.githubusercontent.com/79594454/208986930-844d923a-11a0-402c-bc38-fe7383ca13bd.png">


