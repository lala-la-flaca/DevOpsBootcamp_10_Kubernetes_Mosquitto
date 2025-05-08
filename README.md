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
   <img src="" width=800 />
   
3. Apply the mosquitto-without-volumes.yaml file.
   
   ```bash
   kubectl apply -f mosquitto-without-volumes.yaml
   
   ```
   <img src="" width=800 />
   
4. Verify that the pod is running.
   
   ```bash
   kubectl get pod
   ```
   <img src="" width=800 />
   
5. Access the Mosquitto pod.
    
   ```bash
   kubectl exec -it mosquitto-84f7fdbf49-w89t5 -- /bin/sh
   ```
   <img src="" width=800 />
   
6. Verify the current directory, then navigate to the mosquitto directory.

    ```bash
    ls
    ```

    <img src="" width=800 />
   
7. Open the config directory and verify the files.

    ```bash
    cd config
    ```

    <img src="" width=800 />
   
8. Delete the current Mosquitto pod.
    
    ```bash
    kubectl delete -f mosquitto-without-volumes.yaml
    ```

    <img src="" width=800 />
   

9. Apply the config-file.yaml and secret-file.yaml files.
    
    ```bash
    kubectl apply -f config-file.yaml
    kubectl apply -f secret-file.yaml
    ```

    <img src="" width=800 />
   
10. Verify that the ConfigMap and Secret were created.
    
    ```bash
    kubectl get configmap
    kubectl get secret
    ```

    <img src="" width=800 />
   
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

    <img src="" width=800 />
   
12. Apply the  updated Mosquitto.yaml file.
    
    ```bash
    kubectl apply -f mosquitto.yaml
    ```

    <img src="" width=800 />
   
13. Verify that the new pod is running.
    
    ```bash
    kubectl get pod
    ```

    <img src="" width=800 />
   
14. Access the updated pod.
    
    ```bash
    kubectl exec -it mosquitto-7ddc67b6cd-9h9nk -- /bin/sh
    ```

    <img src="" width=800 />
   
15. Navigate to the mosquitto directory.
    
    ```bash
    cd mosquitto
    ```

    <img src="" width=800 />
   
16. Verify that the secret file was created and check its content.
    
    ```bash
    cd secret
    cat secret.file
    ```

    <img src="" width=800 />
   
17. Go to the config directory and confirm that mosquitto.conf was overwritten.
    
    ```bash
    cd config
    cat mosquitto.conf

    ```

    <img src="" width=800 />
   




