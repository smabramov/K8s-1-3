# «Запуск приложений в K8S»  - Абрамов Сергей

### Цель задания

В тестовой среде для работы с Kubernetes, установленной в предыдущем ДЗ, необходимо развернуть Deployment с приложением, состоящим из нескольких контейнеров, и масштабировать его.

------

### Чеклист готовности к домашнему заданию

1. Установленное k8s-решение (например, MicroK8S).
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключённым git-репозиторием.

------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. [Описание](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) Deployment и примеры манифестов.
2. [Описание](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/) Init-контейнеров.
3. [Описание](https://github.com/wbitt/Network-MultiTool) Multitool.

------

### Задание 1. Создать Deployment и обеспечить доступ к репликам приложения из другого Pod

1. Создать Deployment приложения, состоящего из двух контейнеров — nginx и multitool. Решить возникшую ошибку.

[deployment.yaml](https://github.com/smabramov/K8s-1-3/blob/5a33bec59de21e309d5aecc5cfb72aa62a906f1a/pod_yaml/deployment.yaml)

![k1](https://github.com/smabramov/K8s-1-3/blob/5a33bec59de21e309d5aecc5cfb72aa62a906f1a/png/k1.png)

  Ошибка при развертывании multitool.

![k2](https://github.com/smabramov/K8s-1-3/blob/5a33bec59de21e309d5aecc5cfb72aa62a906f1a/png/k2.png)

  Не может занять порт 80, т.к. он уже занят nginx. Изменим порт 80 на 81 у multitool.

[new_deployment.yaml](https://github.com/smabramov/K8s-1-3/blob/5a33bec59de21e309d5aecc5cfb72aa62a906f1a/pod_yaml/new_deployment.yaml)

![k3](https://github.com/smabramov/K8s-1-3/blob/5a33bec59de21e309d5aecc5cfb72aa62a906f1a/png/k3.png)

Все работает.

2. После запуска увеличить количество реплик работающего приложения до 2.

[2_deployment.yaml](https://github.com/smabramov/K8s-1-3/blob/5a33bec59de21e309d5aecc5cfb72aa62a906f1a/pod_yaml/2_deployment.yaml)

3. Продемонстрировать количество подов до и после масштабирования.

![k3](https://github.com/smabramov/K8s-1-3/blob/5a33bec59de21e309d5aecc5cfb72aa62a906f1a/png/k3.png)
![k4](https://github.com/smabramov/K8s-1-3/blob/5a33bec59de21e309d5aecc5cfb72aa62a906f1a/png/k4.png)

4. Создать Service, который обеспечит доступ до реплик приложений из п.1.

[svc_n_m.yaml](https://github.com/smabramov/K8s-1-3/blob/5a33bec59de21e309d5aecc5cfb72aa62a906f1a/pod_yaml/svc_n_m.yaml)

![k5](https://github.com/smabramov/K8s-1-3/blob/5a33bec59de21e309d5aecc5cfb72aa62a906f1a/png/k5.png)

5. Создать отдельный Pod с приложением multitool и убедиться с помощью `curl`, что из пода есть доступ до приложений из п.1.

[new_multitool.yaml](https://github.com/smabramov/K8s-1-3/blob/5a33bec59de21e309d5aecc5cfb72aa62a906f1a/pod_yaml/new_multitool.yaml)

![k6](https://github.com/smabramov/K8s-1-3/blob/5a33bec59de21e309d5aecc5cfb72aa62a906f1a/png/k6.png)

![k7](https://github.com/smabramov/K8s-1-3/blob/5a33bec59de21e309d5aecc5cfb72aa62a906f1a/png/k7.png)

------

### Задание 2. Создать Deployment и обеспечить старт основного контейнера при выполнении условий

1. Создать Deployment приложения nginx и обеспечить старт контейнера только после того, как будет запущен сервис этого приложения.
2. Убедиться, что nginx не стартует. В качестве Init-контейнера взять busybox.
3. Создать и запустить Service. Убедиться, что Init запустился.
4. Продемонстрировать состояние пода до и после запуска сервиса.

------

### Правила приема работы

1. Домашняя работа оформляется в своем Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд `kubectl` и скриншоты результатов.
3. Репозиторий должен содержать файлы манифестов и ссылки на них в файле README.md.

------
