# KUBERNETES
---
## Minikube Service Command
* Cek status :
`minikube status`
* Jalankan minikube :
`minikube start`
* Hentikan minikube :
`minikube stop`
---

## 2. Nodeport
### Generate yaml file
* Terminal
    ```bash
    kubectl create -f html-nodeport.yaml
    ```
* Output
    ```bash
    replicaset.apps/cvhtml-nodeport created
    service/html-service-nodeport created
    ```
* Kemudian pastikan statusnya sudah running dengan menggunakan perintah
    ```
    kubectl get all
    ```
* Jalankan nodeport dengan menggunakan perintah berikut dan kemudian browser akan otomatis terbuka untuk menjalankan aplikasinya
    ```
    minikube service html-service-nodeport
    ```
---
## 3. Load-Balancer
### Generate file yaml
* Terminal
    ```bash
    kubectl create -f html-loadbalancer.yaml
    ```
* Output
    ```bash
    replicaset.apps/html-loadbalancer created
    service/html-service created
    ```
* Cek url
    ```bash
    minikube service html-service --url
    ```
* Run di browser
    ```
    http://172.17.0.2:31619
    ```
---
## 4. Ingress
### Enable addon
* Terminal
    ```bash
    minikube addons enable ingress
    ```
* Output
    ```bash
    🔎  Verifying ingress addon...
    🌟  The 'ingress' addon is enabled
    ```
### Generate file
* Terminal
    ```bash
    kubectl create -f html-ingress.yaml
    ```
* Output
    ```bash
    replicaset.apps/htmlcv-ingress created
    service/htmlservices-ingress created
    ingress.networking.k8s.io/htmlnets-ingress created
    ```
### Cek daftar ingress yang sudah dibuat
* Terminal
    ```bash
    kubectl get ingresses
    ```
* Output
    ```bash
    NAME               CLASS    HOSTS           ADDRESS      PORTS   AGE
    htmlnets-ingress   <none>   musyahid.cv.local             80      8m6s
    ```
### Mengubah host dan ip address
* Terminal
    ```bash
    sudo nano ~ /etc/hosts
    ```
* Ubah seperti
    ```gnu
    127.0.0.1       localhost
    172.17.0.2      musyahid.cv.local
    ```
* Run di browser
    ```
    http://musyahid.cv.local/
    ```