---
title: Привіт Minikube
content_type: tutorial
weight: 5
menu:
  main:
    title: Початок роботи
    weight: 10
    post: >
<p>Готові попрацювати? Створимо простий Kubernetes кластер для запуску Node.js застосунку "Hello World".</p>
card:
  name: навчальні матеріали
  weight: 10
---

<!-- overview -->

<!--This tutorial shows you how to run a simple Hello World Node.js app
on Kubernetes using [Minikube](/docs/setup/learning-environment/minikube) and Katacoda.
Katacoda provides a free, in-browser Kubernetes environment.
-->
З цього навчального матеріалу ви дізнаєтесь, як запустити у Kubernetes простий Hello World застосунок на Node.js за допомогою [Minikube](/docs/setup/learning-environment/minikube) і Katacoda. Katacoda надає безплатне Kubernetes середовище, що доступне у вашому браузері.

<!--{{< note >}}
You can also follow this tutorial if you've installed [Minikube locally](/docs/tasks/tools/install-minikube/).
{{< /note >}}
-->
{{< note >}}
Також ви можете навчатись за цим матеріалом, якщо встановили [Minikube локально](/docs/tasks/tools/install-minikube/).
{{< /note >}}



## {{% heading "objectives" %}}


<!--* Deploy a hello world application to Minikube.
-->
* Розгорнути Hello World застосунок у Minikube.
<!--* Run the app.
-->
* Запустити застосунок.
<!--* View application logs.
-->
* Переглянути логи застосунку.



## {{% heading "prerequisites" %}}


<!--This tutorial provides a container image built from the following files:
-->
У цьому навчальному матеріалі ми використовуємо образ контейнера, зібраний із наступних файлів:

{{% codenew language="js" file="minikube/server.js" %}}

{{% codenew language="conf" file="minikube/Dockerfile" %}}

<!--For more information on the `docker build` command, read the [Docker documentation](https://docs.docker.com/engine/reference/commandline/build/).
-->
Більше інформації про команду `docker build` ви знайдете у [документації Docker](https://docs.docker.com/engine/reference/commandline/build/).



<!-- lessoncontent -->

## <!--## Create a Minikube cluster
-->

* Створення Minikube кластера
* <!--1. Click **Launch Terminal** 
-->
* Натисніть кнопку **Запуск термінала** 

##  {{< kat-button >}}


 <!--{{< note >}}If you installed Minikube locally, run `minikube start`.{{< /note >}}

 -->


 {{< note >}}Якщо Minikube встановлений локально, виконайте команду `minikube start`.{{< /note >}}

## <!--2. Open the Kubernetes dashboard in a browser:
-->

Відкрийте Kubernetes дашборд у браузері:

## <!--3. Katacoda environment only: At the top of the terminal pane, click the plus sign, and then click **Select port to view on Host 1**.
-->

Тільки для Katacoda: у верхній частині вікна термінала натисніть знак плюс, а потім -- **Select port to view on Host 1**.

<!--4. Katacoda environment only: Type `30000`, and then click **Display Port**.
-->
Тільки для Katacoda: введіть `30000`, а потім натисніть **Display Port**. 

<!--## Create a Deployment
-->

Створення Deployment

<!--A Kubernetes [*Pod*](/docs/concepts/workloads/pods/pod/) is a group of one or more Containers,
tied together for the purposes of administration and networking. The Pod in this
tutorial has only one Container. A Kubernetes
[*Deployment*](/docs/concepts/workloads/controllers/deployment/) checks on the health of your
Pod and restarts the Pod's Container if it terminates. Deployments are the
recommended way to manage the creation and scaling of Pods.
-->
[*Pod*](/docs/concepts/workloads/pods/pod/) у Kubernetes -- це група з одного або декількох контейнерів, що об'єднані разом з метою адміністрування і роботи у мережі. У цьому навчальному матеріалі Pod має лише один контейнер. Kubernetes [*Deployment*](/docs/concepts/workloads/controllers/deployment/) перевіряє стан Pod'а і перезапускає контейнер Pod'а, якщо контейнер перестає працювати. Створювати і масштабувати Pod'и рекомендується за допомогою Deployment'ів.

<!--1. Use the `kubectl create` command to create a Deployment that manages a Pod. The
Pod runs a Container based on the provided Docker image.
-->

За допомогою команди `kubectl create` створіть Deployment, який керуватиме Pod'ом. Pod запускає контейнер на основі наданого Docker образу.

<!--2. View the Deployment:
-->

Перегляньте інформацію про запущений Deployment:

 <!--The output is similar to:
 -->

 У виводі ви побачите подібну інформацію:

<!--3. View the Pod:
-->

## Перегляньте інформацію про запущені Pod'и:

 <!--The output is similar to:

1.  -->
    У виводі ви побачите подібну інформацію:

    ```shell
    # Run a test container image that includes a webserver
    kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
    ```

1. <!--4. View cluster events:
-->

    ```shell
    kubectl get deployments
    ```

   Перегляньте події кластера:

    ```
    NAME         READY   UP-TO-DATE   AVAILABLE   AGE
    hello-node   1/1     1            1           1m
    ```

1. <!--5. View the `kubectl` configuration:
-->

    ```shell
    kubectl get pods
    ```

   Перегляньте конфігурацію `kubectl`:

    ```
    NAME                          READY     STATUS    RESTARTS   AGE
    hello-node-5f76cf6ccf-br9b5   1/1       Running   0          1m
    ```

1.  <!--{{< note >}}For more information about `kubectl`commands, see the [kubectl overview](/docs/user-guide/kubectl-overview/).{{< /note >}}

    ```shell
    kubectl get events
    ```

1.  -->

    ```shell
    kubectl config view
    ```

1.  {{< note >}}Більше про команди `kubectl` ви можете дізнатися зі статті [Загальна інформація про kubectl](/docs/user-guide/kubectl-overview/).{{< /note >}}

   ```shell
   kubectl logs hello-node-5f76cf6ccf-br9b5
   ```

   <!--## Create a Service
-->

   ```
   I0911 09:19:26.677397       1 log.go:195] Started HTTP server on port 8080
   I0911 09:19:26.677586       1 log.go:195] Started UDP server on port  8081
   ```


Створення Service

## <!--By default, the Pod is only accessible by its internal IP address within the
Kubernetes cluster. To make the `hello-node` Container accessible from outside the
Kubernetes virtual network, you have to expose the Pod as a
Kubernetes [*Service*](/docs/concepts/services-networking/service/).
-->
За умовчанням, Pod доступний лише за внутрішньою IP-адресою у межах Kubernetes кластера. Для того, щоб контейнер `hello-node` став доступний за межами віртуальної мережі Kubernetes, Pod необхідно відкрити як Kubernetes [*Service*](/docs/concepts/services-networking/service/).

<!--1. Expose the Pod to the public internet using the `kubectl expose` command:
-->

1. Відкрийте Pod для публічного доступу з інтернету за допомогою команди `kubectl expose`:

    ```shell
    kubectl expose deployment hello-node --type=LoadBalancer --port=8080
    ```

    <!--The `--type=LoadBalancer` flag indicates that you want to expose your Service
    outside of the cluster.

    -->
    Прапорець `--type=LoadBalancer` вказує, що ви хочете відкрити доступ до Service за межами кластера.

2. <!--2. View the Service you just created:
-->

    ```shell
    kubectl get services
    ```

   Перегляньте інформацію про Service, який ви щойно створили:

    ```
    NAME         TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
    hello-node   LoadBalancer   10.108.144.78   <pending>     8080:30369/TCP   21s
    kubernetes   ClusterIP      10.96.0.1       <none>        443/TCP          23m
    ```

    <!--The output is similar to:
    -->
    У виводі ви побачите подібну інформацію:
    <!--On cloud providers that support load balancers,

3.  an external IP address would be provisioned to access the Service. On Minikube,

    ```shell
    minikube service hello-node
    ```

    the `LoadBalancer` type makes the Service accessible through the `minikube service`

##  command.

 -->

1.  Для хмарних провайдерів, що підтримують балансування навантаження, доступ до Service надається через зовнішню IP-адресу. Для Minikube, тип `LoadBalancer` робить Service доступним ззовні за допомогою команди `minikube service`.

    ```shell
    minikube addons list
    ```

   <!--3. Run the following command:
-->

    ```
    addon-manager: enabled
    dashboard: enabled
    default-storageclass: enabled
    efk: disabled
    freshpod: disabled
    gvisor: disabled
    helm-tiller: disabled
    ingress: disabled
    ingress-dns: disabled
    logviewer: disabled
    metrics-server: disabled
    nvidia-driver-installer: disabled
    nvidia-gpu-device-plugin: disabled
    registry: disabled
    registry-creds: disabled
    storage-provisioner: enabled
    storage-provisioner-gluster: disabled
    ```

1. Виконайте наступну команду:

    ```shell
    minikube addons enable metrics-server
    ```

   <!--4. Katacoda environment only: Click the plus sign, and then click **Select port to view on Host 1**.
-->

    ```
    The 'metrics-server' addon is enabled
    ```

1. Тільки для Katacoda: натисніть знак плюс, а потім -- **Select port to view on Host 1**.

    ```shell
    kubectl get pod,svc -n kube-system
    ```

   <!--5. Katacoda environment only: Note the 5 digit port number displayed opposite to `8080` in services output. This port number is randomly generated and it can be different for you. Type your number in the port number text box, then click Display Port. Using the example from earlier, you would type `30369`.
-->

    ```
    NAME                                        READY     STATUS    RESTARTS   AGE
    pod/coredns-5644d7b6d9-mh9ll                1/1       Running   0          34m
    pod/coredns-5644d7b6d9-pqd2t                1/1       Running   0          34m
    pod/metrics-server-67fb648c5                1/1       Running   0          26s
    pod/etcd-minikube                           1/1       Running   0          34m
    pod/influxdb-grafana-b29w8                  2/2       Running   0          26s
    pod/kube-addon-manager-minikube             1/1       Running   0          34m
    pod/kube-apiserver-minikube                 1/1       Running   0          34m
    pod/kube-controller-manager-minikube        1/1       Running   0          34m
    pod/kube-proxy-rnlps                        1/1       Running   0          34m
    pod/kube-scheduler-minikube                 1/1       Running   0          34m
    pod/storage-provisioner                     1/1       Running   0          34m

    NAME                           TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)             AGE
    service/metrics-server         ClusterIP   10.96.241.45    <none>        80/TCP              26s
    service/kube-dns               ClusterIP   10.96.0.10      <none>        53/UDP,53/TCP       34m
    service/monitoring-grafana     NodePort    10.99.24.54     <none>        80:30002/TCP        26s
    service/monitoring-influxdb    ClusterIP   10.111.169.94   <none>        8083/TCP,8086/TCP   26s
    ```

1. Тільки для Katacoda: запишіть п'ятизначний номер порту, що відображається напроти `8080` у виводі сервісу. Номер цього порту генерується довільно і тому може бути іншим у вашому випадку. Введіть номер порту у призначене для цього текстове поле і натисніть Display Port. У нашому прикладі номер порту `30369`.

    ```shell
    kubectl top pods
    ```

    <!--This opens up a browser window that serves your app and shows the "Hello World" message.

    ```
    NAME                         CPU(cores)   MEMORY(bytes)   
    hello-node-ccf4b9788-4jn97   1m           6Mi             
    ```

    -->

    ```
    error: Metrics API not available
    ```

1.  Це відкриє вікно браузера, в якому запущений ваш застосунок, і покаже повідомлення "Hello World".

    ```shell
    minikube addons disable metrics-server
    ```

   <!--## Enable addons
-->

    ```
    metrics-server was successfully disabled
    ```

## Увімкнення розширень

<!--Minikube has a set of built-in {{< glossary_tooltip text="addons" term_id="addons" >}} that can be enabled, disabled and opened in the local Kubernetes environment.
-->
Minikube має ряд вбудованих {{< glossary_tooltip text="розширень" term_id="addons" >}}, які можна увімкнути, вимкнути і відкрити у локальному Kubernetes оточенні.

<!--1. List the currently supported addons:
-->

Перегляньте перелік підтримуваних розширень:

 <!--The output is similar to:

 -->

 У виводі ви побачите подібну інформацію:

<!--2. Enable an addon, for example, `metrics-server`:
-->

## Увімкніть розширення, наприклад `metrics-server`:

 <!--The output is similar to:

##  -->


*  У виводі ви побачите подібну інформацію:
* <!--3. View the Pod and Service you just created:
-->
* Перегляньте інформацію про Pod і Service, які ви щойно створили:
*  <!--The output is similar to:

