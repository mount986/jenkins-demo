# Prerequisits:
- Setup Kubernetes Ccuster
- Install and configure kubectl
- Install helm
- Add Jenkins helm repo (`helm repo add jenkins https://charts.jenkins.io`)
- Create Github OAuth application and secret

# Installation Steps:
1) Create the Persisten Volume Claim for persisting configurations settings
    ```
    kubectl apply -f <PVC definition file>
    kubectl apply -f storage.yaml
    ```

2) Install Jenkins using the helm chart
    ```
    helm install <instance-name> <chart> -f <configuration overrides file>
    helm install jenkins-demo jenkins/jenkins -f values.yaml
    ```

3) Get the LoadBalancer Ingress
    ```
    kubectl describe service <service name>
    kubectl describe service jenkins-demo
    ```
    
4) Create/Update the Github OAuth application with Ingress IP:

    `https://github.com/settings/applications/<Application ID>`
    https://github.com/settings/applications/1888818
    
5) Open Jenkins

    `http://<Ingress IP>:80/login`
    