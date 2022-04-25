# Prerequisits:
- Setup Kubernetes Ccuster
- Install and configure kubectl
- Install helm
- Add Jenkins helm repo (`helm repo add jenkins https://charts.jenkins.io`)
- Create Github OAuth application (jenkins-config-secret)

# Installation Steps:
1) Create the Persisten Volume Claim for persisting configurations settings
    ```
    kubectl apply -f <PVC definition file>
    kubectl apply -f storage.yaml
    ```

2) Create the Jenkins Configuration Secret with Github OAuth Client ID and Secret
    ```
    kubectl create secret <secret name> generic --from-literal=GITHUB_CLIENT_ID=<Github Client ID> --from-literal=GITHUB_CLIENT_SECRET=<Github Client Secret>
    ```

3) Install Jenkins using the helm chart
    ```
    helm install <instance-name> <chart> -f <configuration overrides file>
    helm install jenkins-demo jenkins/jenkins -f values.yaml
    ```

4) Get the LoadBalancer Ingress IP
    ```
    kubectl describe service <service name>
    kubectl describe service jenkins-demo
    ```
    
5) Create/Update the Github OAuth application with Ingress IP

    `https://github.com/settings/applications/<Application ID>`
    
6) Open Jenkins

    `http://<Ingress IP>:80/login`
    