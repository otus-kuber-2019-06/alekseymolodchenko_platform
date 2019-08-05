[![Build Status](https://travis-ci.com/otus-kuber-2019-06/alekseymolodchenko__platform.svg?branch=master)](https://travis-ci.com/otus-kuber-2019-06/alekseymolodchenko_platform)
# Инфраструктурная платформа на основе Kubernetes

## HW #1 - Знакомство с Kubernetes

### kubectl

- Установка kubectl

  ```bash
  cd /tmp && curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.0/bin/darwin/amd64/kubectl
  chmod +x ./kubectl && sudo mv ./kubectl /usr/local/bin/kubectl
  ```

- Просмотр версии kubectl

  ```bash
  $ kubectl version --client -o json
  {
    "clientVersion": {
      "major": "1",
      "minor": "15",
      "gitVersion": "v1.15.0",
      "gitCommit": "e8462b5b5dc2584fdcd18e6bcfe9f1e4d970a529",
      "gitTreeState": "clean",
      "buildDate": "2019-06-19T16:40:16Z",
      "goVersion": "go1.12.5",
      "compiler": "gc",
      "platform": "darwin/amd64"
    }
  }
  ```

### minikube

- Установка minikube

  ```bash
  cd /tmp && curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64 \
  && chmod +x minikube
  sudo mv minikube /usr/local/bin
  ```

- Просмотр версии minikube

  ```bash
  $ minikube version
  minikube version: v1.2.0
  ```

- Запуск minikube

  ```bash
  $ minikube start
  😄  minikube v1.2.0 on darwin (amd64)
  💿  Downloading Minikube ISO ...
   129.33 MB / 129.33 MB [============================================] 100.00% 0s
  🔥  Creating virtualbox VM (CPUs=2, Memory=2048MB, Disk=20000MB) ...
  🐳  Configuring environment for Kubernetes v1.15.0 on Docker 18.09.6
  💾  Downloading kubelet v1.15.0
  💾  Downloading kubeadm v1.15.0
  🚜  Pulling images ...
  🚀  Launching Kubernetes ... 
  ⌛  Verifying: apiserver proxy etcd scheduler controller dns
  🏄  Done! kubectl is now configured to use "minikube"
  ```

- Проверка подключения к Kubernetes

  ```bash
  $ kubectl cluster-info
  Kubernetes master is running at https://192.168.99.109:8443
  KubeDNS is running at https://192.168.99.109:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
  
  To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
  ```

## Kubernetes	Dashboard

- Установка Kubernetes Dashboard Addon

  ```bash
  $ kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta1/aio/deploy/recommended.yaml
  kubectl proxy
  Starting to serve on 127.0.0.1:8001
  ```

  или

  ```bash
  $ minikube dashboard
  🔌  Enabling dashboard ...
  🤔  Verifying dashboard health ...
  🚀  Launching proxy ...
  🤔  Verifying proxy health ...
  🎉  Opening http://127.0.0.1:53603/api/v1/namespaces/kube-system/services/http:kubernetes-dashboard:/proxy/ in your default browser...
  ```

  ![Kubernetes Dashboard](https://i.imgur.com/sAZaMj9.png)

## k9s

 ![k9s](https://i.imgur.com/ijzbQBx.png)

## Работа с Kubernetes в minikube

- Просмотр запущенных контейнеров

  <details><summary>Подробнее</summary><p>

  ```bash
  $ minikube ssh
                           _             _            
              _         _ ( )           ( )           
    ___ ___  (_)  ___  (_)| |/')  _   _ | |_      __  
  /' _ ` _ `\| |/' _ `\| || , <  ( ) ( )| '_`\  /'__`\
  | ( ) ( ) || || ( ) || || |\`\ | (_) || |_) )(  ___/
  (_) (_) (_)(_)(_) (_)(_)(_) (_)`\___/'(_,__/'`\____)

  $ docker ps
  CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS               NAMES
  05b44f0482d3        amolodchenko/web-app           "nginx -g 'daemon of…"   About an hour ago   Up About an hour                          k8s_web_web-pod_default_772c14ec-f86a-4c6a-9bea-24dca15be
  60a_0
  cf56af929e1e        k8s.gcr.io/pause:3.1           "/pause"                 About an hour ago   Up About an hour                          k8s_POD_web-pod_default_772c14ec-f86a-4c6a-9bea-24dca15be
  60a_0
  c5448f0b209a        kubernetesui/metrics-scraper   "/metrics-sidecar"       About an hour ago   Up About an hour                          k8s_kubernetes-metrics-scraper_kubernetes-metrics-scraper
  -86456cdd8f-9bqrp_kubernetes-dashboard_d5cc976f-bd50-44e5-bc0e-24697700728c_0
  2b74845f8277        kubernetesui/dashboard         "/dashboard --insecu…"   About an hour ago   Up About an hour                          k8s_kubernetes-dashboard_kubernetes-dashboard-5c8f9556c4-47qwd_kubernetes-dashboard_251381b2-c87e-4c00-88d0-b64b8cb9d7df_0
  8ce8310b7f95        k8s.gcr.io/pause:3.1           "/pause"                 About an hour ago   Up About an hour                          k8s_POD_kubernetes-metrics-scraper-86456cdd8f-9bqrp_kubernetes-dashboard_d5cc976f-bd50-44e5-bc0e-24697700728c_0
  a7ea7928a12d        k8s.gcr.io/pause:3.1           "/pause"                 About an hour ago   Up About an hour                          k8s_POD_kubernetes-dashboard-5c8f9556c4-47qwd_kubernetes-dashboard_251381b2-c87e-4c00-88d0-b64b8cb9d7df_0
  8e66b014947f        eb516548c180                   "/coredns -conf /etc…"   About an hour ago   Up About an hour                          k8s_coredns_coredns-5c98db65d4-cklj7_kube-system_b48188bc-d619-4747-891d-1c95d569e76a_1
  b987d1ebfecb        eb516548c180                   "/coredns -conf /etc…"   About an hour ago   Up About an hour                          k8s_coredns_coredns-5c98db65d4-pcgcv_kube-system_d0cb146c-eb01-42a3-ba1b-655749ccc941_1
  51615888a954        4689081edb10                   "/storage-provisioner"   About an hour ago   Up About an hour                          k8s_storage-provisioner_storage-provisioner_kube-system_a547ca42-386b-415f-8514-ab8be27a1f65_0
  0fee30d0aea9        k8s.gcr.io/pause:3.1           "/pause"                 About an hour ago   Up About an hour                          k8s_POD_storage-provisioner_kube-system_a547ca42-386b-415f-8514-ab8be27a1f65_0
  a01145bed38b        d235b23c3570                   "/usr/local/bin/kube…"   About an hour ago   Up About an hour                          k8s_kube-proxy_kube-proxy-f58sv_kube-system_ef69284b-6fe0-4de2-a469-60163dba44d0_0
  253d5f27b7ef        k8s.gcr.io/pause:3.1           "/pause"                 About an hour ago   Up About an hour                          k8s_POD_kube-proxy-f58sv_kube-system_ef69284b-6fe0-4de2-a469-60163dba44d0_0
  0ece395a9121        k8s.gcr.io/pause:3.1           "/pause"                 About an hour ago   Up About an hour                          k8s_POD_coredns-5c98db65d4-pcgcv_kube-system_d0cb146c-eb01-42a3-ba1b-655749ccc941_0
  de91f4d90c46        k8s.gcr.io/pause:3.1           "/pause"                 About an hour ago   Up About an hour                          k8s_POD_coredns-5c98db65d4-cklj7_kube-system_b48188bc-d619-4747-891d-1c95d569e76a_0
  0bd4220ab8b5        201c7a840312                   "kube-apiserver --ad…"   About an hour ago   Up About an hour                          k8s_kube-apiserver_kube-apiserver-minikube_kube-system_a598478bb79fd320264d4bafd5c540f2_0
  222ddf76010a        8328bb49b652                   "kube-controller-man…"   About an hour ago   Up About an hour                          k8s_kube-controller-manager_kube-controller-manager-minikube_kube-system_676a8a1e3e146d0c0f7c4f6e1e96b578_0
  057bd6284395        119701e77cbc                   "/opt/kube-addons.sh"    About an hour ago   Up About an hour                          k8s_kube-addon-manager_kube-addon-manager-minikube_kube-system_65a31d2b812b11a2035f37c8a742e46f_0
  b7a55f7f2072        2c4adeb21b4f                   "etcd --advertise-cl…"   About an hour ago   Up About an hour                          k8s_etcd_etcd-minikube_kube-system_ab0e5db83350b69ce215cb10805e9e66_0
  8fbe35afe22e        2d3813851e87                   "kube-scheduler --bi…"   About an hour ago   Up About an hour                          k8s_kube-scheduler_kube-scheduler-minikube_kube-system_31d9ee8b7fb12e797dc981a8686f6b2b_0
  78c6485ea04a        k8s.gcr.io/pause:3.1           "/pause"                 About an hour ago   Up About an hour                          k8s_POD_kube-addon-manager-minikube_kube-system_65a31d2b812b11a2035f37c8a742e46f_0
  698f5abe2ba5        k8s.gcr.io/pause:3.1           "/pause"                 About an hour ago   Up About an hour                          k8s_POD_kube-controller-manager-minikube_kube-system_676a8a1e3e146d0c0f7c4f6e1e96b578_0
  e59cad7d4c42        k8s.gcr.io/pause:3.1           "/pause"                 About an hour ago   Up About an hour                          k8s_POD_kube-scheduler-minikube_kube-system_31d9ee8b7fb12e797dc981a8686f6b2b_0
  f61bae4eb786        k8s.gcr.io/pause:3.1           "/pause"                 About an hour ago   Up About an hour                          k8s_POD_etcd-minikube_kube-system_ab0e5db83350b69ce215cb10805e9e66_0
  f654c67e5be5        k8s.gcr.io/pause:3.1           "/pause"                 About an hour ago   Up About an hour                          k8s_POD_kube-apiserver-minikube_kube-system_a598478bb79fd320264d4bafd5c540f2_0
  ```
  </p></details>

- Удаление pod's для проверки устойчивости k8s

  ```bash
  $ docker rm -f $(docker ps -a -q)
  ```

  <details><summary>Результат</summary><p>
 
  ```bash
  $ docker ps
  CONTAINER ID        IMAGE                    COMMAND                  CREATED             STATUS              PORTS               NAMES
  f68a0043ddf9        kubernetesui/dashboard   "/dashboard --insecu…"   12 seconds ago      Up 11 seconds                             k8s_kubernetes-dashboard_kubernetes-dashboard-5c8f9556c4-47qwd_kubernetes-dashboard_251381b2-c87e-4c00-88d0-b64b8cb9d7df_0
  dd5d3b9f4d29        amolodchenko/web-app     "nginx -g 'daemon of…"   14 seconds ago      Up 14 seconds                             k8s_web_web-pod_default_772c14ec-f86a-4c6a-9bea-24dca15be60a_0
  4fe882ef9345        44390ebe2b73             "/metrics-sidecar"       15 seconds ago      Up 14 seconds                             k8s_kubernetes-metrics-scraper_kubernetes-metrics-scraper-86456cdd8f-9bqrp_kubernetes-dashboard_d5cc976f-bd50-44e5-bc0e-24697700728c_0
  1109de373991        eb516548c180             "/coredns -conf /etc…"   15 seconds ago      Up 15 seconds                             k8s_coredns_coredns-5c98db65d4-pcgcv_kube-system_d0cb146c-eb01-42a3-ba1b-655749ccc941_0
  6689da001ebb        4689081edb10             "/storage-provisioner"   16 seconds ago      Up 15 seconds                             k8s_storage-provisioner_storage-provisioner_kube-system_a547ca42-386b-415f-8514-ab8be27a1f65_0
  e267e7515622        8328bb49b652             "kube-controller-man…"   16 seconds ago      Up 15 seconds                             k8s_kube-controller-manager_kube-controller-manager-minikube_kube-system_676a8a1e3e146d0c0f7c4f6e1e96b578_0
  320f7ad3b7fa        eb516548c180             "/coredns -conf /etc…"   16 seconds ago      Up 15 seconds                             k8s_coredns_coredns-5c98db65d4-cklj7_kube-system_b48188bc-d619-4747-891d-1c95d569e76a_0
  8037f28c09e8        k8s.gcr.io/pause:3.1     "/pause"                 17 seconds ago      Up 15 seconds                             k8s_POD_kubernetes-dashboard-5c8f9556c4-47qwd_kubernetes-dashboard_251381b2-c87e-4c00-88d0-b64b8cb9d7df_0
  8863e74ce687        k8s.gcr.io/pause:3.1     "/pause"                 17 seconds ago      Up 15 seconds                             k8s_POD_coredns-5c98db65d4-pcgcv_kube-system_d0cb146c-eb01-42a3-ba1b-655749ccc941_0
  16b82efb7892        k8s.gcr.io/pause:3.1     "/pause"                 17 seconds ago      Up 15 seconds                             k8s_POD_storage-provisioner_kube-system_a547ca42-386b-415f-8514-ab8be27a1f65_0
  929a69081c13        k8s.gcr.io/pause:3.1     "/pause"                 17 seconds ago      Up 15 seconds                             k8s_POD_kube-controller-manager-minikube_kube-system_676a8a1e3e146d0c0f7c4f6e1e96b578_0
  c9818efc0ca8        k8s.gcr.io/pause:3.1     "/pause"                 17 seconds ago      Up 14 seconds                             k8s_POD_kubernetes-metrics-scraper-86456cdd8f-9bqrp_kubernetes-dashboard_d5cc976f-bd50-44e5-bc0e-24697700728c_0
  ad5e9023c63a        d235b23c3570             "/usr/local/bin/kube…"   17 seconds ago      Up 15 seconds                             k8s_kube-proxy_kube-proxy-f58sv_kube-system_ef69284b-6fe0-4de2-a469-60163dba44d0_0
  bb96dbd9e4b5        2c4adeb21b4f             "etcd --advertise-cl…"   18 seconds ago      Up 15 seconds                             k8s_etcd_etcd-minikube_kube-system_ab0e5db83350b69ce215cb10805e9e66_0
  81cb07ddf70c        119701e77cbc             "/opt/kube-addons.sh"    18 seconds ago      Up 17 seconds                             k8s_kube-addon-manager_kube-addon-manager-minikube_kube-system_65a31d2b812b11a2035f37c8a742e46f_0
  cc0f2565b47e        201c7a840312             "kube-apiserver --ad…"   18 seconds ago      Up 17 seconds                             k8s_kube-apiserver_kube-apiserver-minikube_kube-system_a598478bb79fd320264d4bafd5c540f2_0
  a56adfbf294e        2d3813851e87             "kube-scheduler --bi…"   18 seconds ago      Up 17 seconds                             k8s_kube-scheduler_kube-scheduler-minikube_kube-system_31d9ee8b7fb12e797dc981a8686f6b2b_0
  738454d47c84        k8s.gcr.io/pause:3.1     "/pause"                 18 seconds ago      Up 16 seconds                             k8s_POD_coredns-5c98db65d4-cklj7_kube-system_b48188bc-d619-4747-891d-1c95d569e76a_0
  4069aacb02bf        k8s.gcr.io/pause:3.1     "/pause"                 18 seconds ago      Up 17 seconds                             k8s_POD_kube-proxy-f58sv_kube-system_ef69284b-6fe0-4de2-a469-60163dba44d0_0
  478eb8069f54        k8s.gcr.io/pause:3.1     "/pause"                 18 seconds ago      Up 17 seconds                             k8s_POD_etcd-minikube_kube-system_ab0e5db83350b69ce215cb10805e9e66_0
  6482cda8fb06        k8s.gcr.io/pause:3.1     "/pause"                 18 seconds ago      Up 16 seconds                             k8s_POD_web-pod_default_772c14ec-f86a-4c6a-9bea-24dca15be60a_1
  1bb64e7d2113        k8s.gcr.io/pause:3.1     "/pause"                 18 seconds ago      Up 18 seconds                             k8s_POD_kube-addon-manager-minikube_kube-system_65a31d2b812b11a2035f37c8a742e46f_0
  06b91c27b777        k8s.gcr.io/pause:3.1     "/pause"                 19 seconds ago      Up 18 seconds                             k8s_POD_kube-scheduler-minikube_kube-system_31d9ee8b7fb12e797dc981a8686f6b2b_1
  8e369f97a74a        k8s.gcr.io/pause:3.1     "/pause"                 19 seconds ago      Up 18 seconds                             k8s_POD_kube-apiserver-minikube_kube-system_a598478bb79fd320264d4bafd5c540f2_1
  ```
  </p></details>

- Просмотр системных компонентов k8s 
  ```bash
  $ kubectl get pods -n kube-system
  ```

  <details><summary>Результат</summary><p>
  
  ```bash
  NAME                               READY   STATUS    RESTARTS   AGE
  coredns-5c98db65d4-cklj7           1/1     Running   0          112m
  coredns-5c98db65d4-pcgcv           1/1     Running   0          112m
  etcd-minikube                      1/1     Running   0          111m
  kube-addon-manager-minikube        1/1     Running   0          111m
  kube-apiserver-minikube            1/1     Running   0          111m
  kube-controller-manager-minikube   1/1     Running   0          111m
  kube-proxy-f58sv                   1/1     Running   0          112m
  kube-scheduler-minikube            1/1     Running   0          111m
  storage-provisioner                1/1     Running   0          112m
  ```
  </p></details>

- Проверим что кластер работает и находится в исправном состоянии

  ```bash
  $ kubectl get componentstatuses
  ```

  <details><summary>Результат</summary><p>

  ```bash
  NAME                 STATUS    MESSAGE             ERROR
  controller-manager   Healthy   ok                  
  scheduler            Healthy   ok                  
  etcd-0               Healthy   {"health":"true"}
  ```
  </p></details>

## Dockerfile для веб-сервера

  ```bash
  FROM python:3.7-alpine3.10

  WORKDIR /app
  VOLUME ["/app"]
  USER 1001:1001
  EXPOSE 8000

  ENTRYPOINT ["python3", "-m", "http.server"]
  ```

## Манифест	pod

  <details><summary>Подробнее</summary><p>

  ```bash
  apiVersion: v1
  kind: Pod
  metadata:
    name: web
    labels:
      app: web
  spec:
    initContainers:
    - name: init
      image: busybox:1.31.0
      command: ['sh', '-c', 'wget -O- https://raw.githubusercontent.com/express42/otus-platform-snippets/master/Module-02/Introduction-to-Kubernetes/wget.sh | sh']
      volumeMounts:
      - mountPath: /app
        name: app
    containers:
    - name: web
      image: amolodchenko/kubernetes-intro
      volumeMounts:
      - mountPath: /app
        name: app
    volumes:
    - name: app
      emptyDir: {}
  ```
  </p></details>

- Применение манифейста
  
  ```bash
  kubectl apply -f web-pod.yaml && kubectl get pods -w
  ```

  <details><summary>Результат</summary><p>

  ```bash
  NAME   READY   STATUS     RESTARTS   AGE
  web    0/1     Init:0/1   0          0s
  web    0/1     PodInitializing   0          1s
  web    1/1     Running           0          6s
  ```
  </p></details>

- Проверка работы приложения
  
  Для доступа к поду воспользуемся командой [kubectl port-forward](https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/)
  ```bash
  kubectl port-forward --address 0.0.0.0 pod/web 8000:8000
  ```

  <details><summary>Результат</summary><p>

  ![Kubernetes pod](https://i.imgur.com/9ghoWhI.png)
  
  </p></details>

## HW #2 - Безопасность и управлении доступом Kubernetes

- Cоздание ServiceAccount с ролью admin в рамках всего кластера

  <details><summary>Подробнее</summary><p>

  ```yml
    ---
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: bob
      namespace: default
    ---
    apiVersion: rbac.authorization.k8s.io/v1beta1
    kind: ClusterRoleBinding
    metadata:
      name: bob
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: ClusterRole
      name: cluster-admin
    subjects:
      - kind: ServiceAccount
        name: bob
        namespace: default
  ```
  </p></details>

- Cоздание ServiceAccount без доступа к кластеру

  <details><summary>Подробнее</summary><p>

  ```yml
    ---
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: dave
  ```
  </p></details>

- Cоздание Namespace prometheus

  <details><summary>Подробнее</summary><p>

  ```yml
    ---
    apiVersion: v1
    kind: Namespace
    metadata:
      name: prometheus
  ```
  </p></details>

- Cоздание Namespace prometheus

  <details><summary>Подробнее</summary><p>

  ```yml
    ---
    apiVersion: v1
    kind: Namespace
    metadata:
      name: prometheus
  ```
  </p></details>

- Cоздание ServiceAccount в неймспейсе prometheus

  <details><summary>Подробнее</summary><p>

  ```yml
    ---
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: carol
      namespace: prometheus
  ```
  </p></details>

- Предоставление возможностей get, list, watch для всех ServiceAccount в неймспейсе prometheus в отношении объектов Pods всего кластера 

  <details><summary>Подробнее</summary><p>

  ```yml
    ---
    apiVersion: rbac.authorization.k8s.io/v1beta1
    kind: ClusterRole
    metadata:
      name: pod-reader
    rules:
    - apiGroups: [""]
      resources: ["pods"]
      verbs: ["get", "list", "watch"]

    ---
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRoleBinding
    metadata:
      name: pod-reader
    subjects:
    - kind: Group
      name: system:serviceaccounts:prometheus
      apiGroup: rbac.authorization.k8s.io
    roleRef:
      kind: ClusterRole
      name: pod-reader
      apiGroup: rbac.authorization.k8s.io
  ```
  </p></details>

- Cоздание Namespace dev

  <details><summary>Подробнее</summary><p>

  ```yml
    ---
    apiVersion: v1
    kind: Namespace
    metadata:
      name: dev
  ```
  </p></details>

- Cоздание ServiceAccount в неймспейсе dev c правами admin

  <details><summary>Подробнее</summary><p>

  ```yml
    ---
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: jane
      namespace: dev
    ---
    kind: Role
    apiVersion: rbac.authorization.k8s.io/v1beta1
    metadata:
      name: admin-ns
      namespace: dev
    rules:
    - apiGroups: ["*"]
      resources: ["*"]
      verbs: ["*"]
    ---
    kind: RoleBinding
    apiVersion: rbac.authorization.k8s.io/v1beta1
    metadata:
      name: admin-ns-binding
      namespace: dev
    subjects:
    - kind: ServiceAccount
      name: jane
      namespace: dev
    roleRef:
      kind: Role
      name: admin-ns
      apiGroup: rbac.authorization.k8s.io

  ```
  </p></details>

- Cоздание ServiceAccount в неймспейсе dev c правами view

  <details><summary>Подробнее</summary><p>

  ```yml
    ---
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: ken
      namespace: dev
    ---
    kind: Role
    apiVersion: rbac.authorization.k8s.io/v1beta1
    metadata:
      name: view-ns
      namespace: dev
    rules:
    - apiGroups: ["*"]
      resources: ["*"]
      verbs: ["get", "list", "watch"]
    ---
    kind: RoleBinding
    apiVersion: rbac.authorization.k8s.io/v1beta1
    metadata:
      name: view-ns-binding
      namespace: dev
    subjects:
    - kind: ServiceAccount
      name: ken
      namespace: dev
    roleRef:
      kind: Role
      name: view-ns
      apiGroup: rbac.authorization.k8s.io

  ```
  </p></details>


## HW #4 - Volumes, Storages,StatefulSet

### kind

- Установка kind

  ```bash
  $ cd /tmp && curl -Lo ./kind-darwin-amd64 https://github.com/kubernetes-sigs/kind/releases/download/v0.4.0/kind-darwin-amd64
  $ chmod +x ./kind-darwin-amd64 && sudo mv ./kind-darwin-amd64 /usr/local/bin/kind
  ```

- Запуск kind

  ```bash
  $ kind create cluster
  $ export KUBECONFIG="$(kind get kubeconfig-path --name="kind")"
  ```

### StatefulSet

- Применим манифест для StatefulSet

  ```bash
  $ curl -Lo ./minio-statefulset.yaml https://raw.githubusercontent.com/express42/otus-platform-snippets/master/Module-02/Kuberenetes-volumes/minio-statefulset.yaml
  $ kubectl -f minio-statefulset.yaml
  ```

  <details><summary>Подробнее</summary><p>
  
  ```bash
  $ kubectl get pods
    NAME      READY   STATUS    RESTARTS   AGE
    minio-0   1/1     Running   0          17m
  ```

  ```bash
  $ kubectl get statefulsets
    NAME    READY   AGE
    minio   1/1     20m
  ```

  ```bash
  $ kubectl get pv
    NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                  STORAGECLASS   REASON   AGE
    pvc-5d582e73-50ff-4910-9d71-a0d9fb877f36   10Gi       RWO            Delete           Bound    default/data-minio-0   standard                20m
  ```

  ```bash
  $ kubectl get pvc
    NAME           STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
    data-minio-0   Bound    pvc-5d582e73-50ff-4910-9d71-a0d9fb877f36   10Gi       RWO            standard       20m
  ```
  </p>
  </details>

### Headless Service

- Применим манифест для Headless Service

  ```bash
  $ curl -Lo ./minio-headless-service.yaml https://raw.githubusercontent.com/express42/otus-platform-snippets/master/Module-02/Kuberenetes-volumes/minio-headless-service.yaml
  $ kubectl -f minio-headless-service.yaml
  ```

  <details><summary>Подробнее</summary><p>
  
  ```bash
  $ kubectl get service
    NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)    AGE
    kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP    36m
    minio        ClusterIP   None         <none>        9000/TCP   27m
  ```
  </p>
  </details>

### Secrets

- Создание Secret

  ```bash
  apiVersion: v1
  kind: Secret
  metadata:
    name: minio
  data:
    access_key: bWluaW8=
    secret_key: bWluaW8xMjM=
  ```
- Применение манифеста с секретом

  ```bash
  $ kubectl apply -f kubernetes-volumes/minio-secret.yaml
    secret/minio created
  ```

  <details><summary>Подробнее</summary><p>
  
  ```bash
  $ kubectl get secrets
    NAME                  TYPE                                  DATA   AGE
    default-token-f8dkg   kubernetes.io/service-account-token   3      38m
    minio                 Opaque                                2      6s
  ```
  </p>
  </details>

- Обновляем StatefulSet для использования внось созданного секрета

  ```bash
  ...

      spec:
      containers:
      - name: minio
        env:
        - name: MINIO_ACCESS_KEY
          valueFrom:
            secretKeyRef:
              name: minio
              key: access_key
        - name: MINIO_SECRET_KEY
          valueFrom:
            secretKeyRef:
              name: minio
              key: secret_key
        image: minio/minio:RELEASE.2019-07-10T00-34-56Z
  
  ...
  ```
