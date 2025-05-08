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
   
   ```
   
2. Review the ConfigMap.yaml file.
   
   ```bash
   
   ```
   <img src="" width=800 />
   
3. Apply the mosquitto-without-volumes.yaml file.
   
   ```bash
   
   ```
   <img src="" width=800 />
   
4. Verify that the pod is running.
   
   ```bash
   
   ```
   <img src="" width=800 />
   
5. Access the Mosquitto pod.
    
   ```bash
   
   ```
   <img src="" width=800 />
   
6. Verify the current directory, then navigate to the mosquitto directory.

    ```bash

    ```

    <img src="" width=800 />
   
7. Open the config directory and verify the files.

    ```bash

    ```

    <img src="" width=800 />
   
8. Delete the current Mosquitto pod.
    
    ```bash

    ```

    <img src="" width=800 />
   

9. Apply the config-file.yaml and secret-file.yaml files.
    
    ```bash

    ```

    <img src="" width=800 />
   
10. Verify that the ConfigMap and Secret were created.
    
    ```bash

    ```

    <img src="" width=800 />
   
11. Mount the volumes in the Mosquitto.yaml file and save your changes.
    
    ```bash

    ```

    <img src="" width=800 />
   
12. Apply the  updated Mosquitto.yaml file.
    
    ```bash

    ```

    <img src="" width=800 />
   
13. Verify that the new pod is running.
    
    ```bash

    ```

    <img src="" width=800 />
   
14. Access the updated pod.
    
    ```bash

    ```

    <img src="" width=800 />
   
15. Navigate to the mosquitto directory.
    
    ```bash

    ```

    <img src="" width=800 />
   
16. Verify that the secret file was created and check its content.
    
    ```bash

    ```

    <img src="" width=800 />
   
17. Go to the config directory and confirm that mosquitto.conf was overwritten.
    
    ```bash

    ```

    <img src="" width=800 />
   




