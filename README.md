# ☸️ Kubernetes
This demo project is part of Module 9: AWS Services from Nana DevOps Bootcamp. They cover deploying services into a local Kubernetes cluster using tools like **Minikube**, and managing configurations with **ConfigMap** and **Secrets**

## 📦 Demo 2: Deploy Mosquitto Broker with ConfigMap & Secret Volume Types
In this demo, we deploy the **Mosquitto MQTT message broker** on Kubernetes. We manage its custom configuration and passwords using **ConfigMap** and **Secret volume types**, mounting them directly into the container.

## 🚀 Technologies Used
- **Kubernetes (minikube)**: Container orchestration
- **Docker**: Containers
- **Mosquito**: Message broker
  
## 📋 Prerequisites
- Ensure minikube is running

## 🎯 Features

- **Define configuration and passwords for Mosquito using ConfigMap and Secret Volume Type**


## 🏗 Project Architecture

<img src=""/>

## ⚙️ Project Configuration
1. Clone the bootcamp repository.

   ```bash
   git clone <repo>   
   ```
   
2. Review the Config-File.yaml file.
   
   ```bash
    apiVersion: v1
    kind: ConfigMap
    metadata:
        name: mosquitto-config-file
    data:
        mosquitto.conf: |
            log_dest stdout
            log_type all
            log_timestamp true
            listener 9001
   ```
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Mosquitto/blob/main/Img/1%20configfile.png" width=800 />
   
3. Apply the mosquitto-without-volumes.yaml file.
   
   ```bash
   kubectl apply -f mosquitto-without-volumes.yaml
   
   ```
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Mosquitto/blob/main/Img/2%20apply%20mosquito%20no%20volumes.png" width=800 />
   
4. Verify that the pod is running.
   
   ```bash
   kubectl get pod
   ```
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Mosquitto/blob/main/Img/3%20current%20pods.png" width=800 />
   
5. Access the Mosquitto pod.
    
   ```bash
   kubectl exec -it mosquitto-84f7fdbf49-w89t5 -- /bin/sh
   ```
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Mosquitto/blob/main/Img/4%20entering%20the%20container.png" width=800 />
   
6. Verify the current directory, then navigate to the mosquitto directory.

    ```bash
    ls
    ```

    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Mosquitto/blob/main/Img/5%20checking%20mosqitto.png" width=800 />
   
7. Open the config directory and verify the files.

    ```bash
    cd config
    ```
   
8. Delete the current Mosquitto pod.
    
    ```bash
    kubectl delete -f mosquitto-without-volumes.yaml
    ```

    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Mosquitto/blob/main/Img/6%20deleting%20the%20mosquitto%20using%20the%20same%20file.png" width=800 />
   

9. Apply the config-file.yaml and secret-file.yaml files.
    
    ```bash
    kubectl apply -f config-file.yaml
    kubectl apply -f secret-file.yaml
    ```

    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Mosquitto/blob/main/Img/7%20applying%20configfile%20and%20secret%20file.png" width=800 />
   
10. Verify that the ConfigMap and Secret were created.
    
    ```bash
    kubectl get configmap
    kubectl get secret
    ```

    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Mosquitto/blob/main/Img/9%20configmap%20secret.png" width=800 />
   
11. Mount the volumes in the Mosquitto.yaml file and save your changes.
    
    ```bash
          spec:
          containers:
            - name: mosquitto
              image: eclipse-mosquitto:2.0
              ports:
                - containerPort: 1883
              volumeMounts: 
                - name: mosquitto-config
                  mountPath: /mosquitto/config
                - name: mosquitto-secret
                  mountPath: /mosquitto/secret
                  readOnly: true
          volumes:
            - name: mosquitto-config
              configMap:
                name: mosquitto-config-file
            - name: mosquitto-secret
              secret:
                secretName: mosquitto-secret-file
    ```

    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Mosquitto/blob/main/Img/12%20mosquitto%20yaml%20file%20mounting%20volumes.png" width=800 />
   
12. Apply the  updated Mosquitto.yaml file.
    
    ```bash
    kubectl apply -f mosquitto.yaml
    ```
   
13. Verify that the new pod is running.
    
    ```bash
    kubectl get pod
    ```

    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Mosquitto/blob/main/Img/13%20mosquito%20pod.png" width=800 />
   
14. Access the updated pod.
    
    ```bash
    kubectl exec -it mosquitto-7ddc67b6cd-9h9nk -- /bin/sh
    ```
15. Navigate to the mosquitto directory.
    
    ```bash
    cd mosquitto
    ```
   
16. Verify that the secret file was created and check its content.
    
    ```bash
    cd secret
    cat secret.file
    ```
   
17. Go to the config directory and confirm that mosquitto.conf was overwritten.
    
    ```bash
    cd config
    cat mosquitto.conf
    ```

    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Mosquitto/blob/main/Img/14%20entering%20container%20and%20checking%20that%20the%20confi%20file%20was%20overwritten%20and%20secrets%20created.png" width=800 />
   




