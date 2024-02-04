---
reviewers:
- brendandburns
- erictune
- mikedanese
title: Початок роботи
main_menu: true
weight: 20
content_type: concept
no_list: true
card:
  name: setup
  weight: 20
  anchors:
  - anchor: "#навчальне-середовище"
    title: Навчальне середовище
  - anchor: "#прод-оточення"
    title: Прод оточення  
---

<!-- overview -->

<!--This section covers different options to set up and run Kubernetes.
-->
У цьому розділі розглянуто різні варіанти налаштування і запуску Kubernetes.

<!--Different Kubernetes solutions meet different requirements: ease of maintenance, security, control, available resources, and expertise required to operate and manage a cluster.
-->
Різні рішення Kubernetes відповідають різним вимогам: легкість в експлуатації, безпека, система контролю, наявні ресурси та досвід, необхідний для управління кластером.

<!--You can deploy a Kubernetes cluster on a local machine, cloud, on-prem datacenter; or choose a managed Kubernetes cluster. You can also create custom solutions across a wide range of cloud providers, or bare metal environments.
-->
Ви можете розгорнути Kubernetes кластер на робочому комп'ютері, у хмарі чи в локальному дата-центрі, або обрати керований Kubernetes кластер. Також можна створити індивідуальні рішення на базі різних провайдерів хмарних сервісів або на звичайних серверах.

<!--More simply, you can create a Kubernetes cluster in learning and production environments.
-->
Простіше кажучи, ви можете створити Kubernetes кластер у навчальному і в прод оточеннях.



<!-- body -->

<!--## Learning environment
-->

Навчальне оточення {#навчальне-оточення}

<!--If you're learning Kubernetes, use the Docker-based solutions: tools supported by the Kubernetes community, or tools in the ecosystem to set up a Kubernetes cluster on a local machine.
-->
Для вивчення Kubernetes використовуйте рішення на базі Docker: інструменти, підтримувані спільнотою Kubernetes, або інші інструменти з сімейства проектів для налаштування Kubernetes кластера на локальному комп'ютері.

{{< table caption="Таблиця інструментів для локального розгортання Kubernetes, які підтримуються спільнотою або входять до сімейства проектів Kubernetes." >}}

Спільнота

## Сімейство проектів

[Minikube](/docs/setup/learning-environment/minikube/)

## [CDK on LXD](https://www.ubuntu.com/kubernetes/docs/install-local)

[kind (Kubernetes IN Docker)](https://github.com/kubernetes-sigs/kind)

[Docker Desktop](https://www.docker.com/products/docker-desktop)

## [Minishift](https://docs.okd.io/latest/minishift/)

- [MicroK8s](https://microk8s.io/)
- [IBM Cloud Private-CE (Community Edition)](https://github.com/IBM/deploy-ibm-cloud-private)
- [IBM Cloud Private-CE (Community Edition) on Linux Containers](https://github.com/HSBawa/icp-ce-on-linux-containers)
- [k3s](https://k3s.io)

{{< /table >}}

- Прод оточення {#прод-оточення}
