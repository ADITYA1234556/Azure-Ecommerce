# Ecommerce Demo in AZURE
In this project, I am hosting an ecommerce application in AKS. I am using <a href="https://github.com/instana/robot-shop">**Instana/robot-shop**</a> repo for getting source code and creating containers from that.

## **Steps to follow**
- Created Azure Kubernetes cluster and connected to it
```bash
az aks get-credentials --resource-group robotshop --name robotshop
```
- Create a namespace robot-shop
```bash
kubectl create namespace robot-shop
```
- Deploy the Helm charts to the kubernetes cluster
```bash
cd helm
helm install robot-shop --namespace robot-shop . 
kubectl get all -n robot-shop
```
- Redis Deployment comes with persistent volume claim type standard that is used in AWS environment. In azure we have type default that we can use.
- Change the storage class to use the default and Create a persistent volume and volume claim with storage class name with default
```bash
kubectl get storageclass
kubectl delete pvc -n robot-shop data-redis-0
kubectl apply -f pvc.yml -n robot-shop
kubectl apply -f pv.yml -n robot-shop
```
- Verify all pods are running
```bash
kubectl get pods -n robot-shop
```
- Get the LoadBalancer endpoint, make sure you allow incoming traffic in network settings
```bash
kubectl get svc -n robot-shop
```
- Access the application



