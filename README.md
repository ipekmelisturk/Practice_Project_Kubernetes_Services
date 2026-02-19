# Practice Project for Kubernetes Services
# Using IBM course as an guide, I built and deployed a JavaScript application to Kubernetes using Docker.

The following concepts are explored:
- ConfigMap
- DaemonSet
- Kubernetes Service
- Secret
- Volumes and Persistent Volume Claims


To create a ConfigMap firstly we need to create an IBM Cloud container:
Export your namespace:
```
export MY_NAMESPACE=sn-labs-$USERNAME 
```
Build the Docker image: 
```
docker build . -t us.icr.io/$MY_NAMESPACE/myapp:v1 
```
Push the tagged image to the IBM Cloud container registry:
```
docker push us.icr.io/$MY_NAMESPACE/myapp:v1 
```
We can check all the images to verify the app:
```
ibmcloud cr images
```
We can get your namespace using:
```
ibmcloud cr namespaces
```
Apply the deployment:
```
kubectl apply -f deployment.yml
```
Start the application(using port 3000):
```
kubectl port-forward deployment.apps/myapp 3000:3000 
```
To set up a ConfigMap to manage configuration data for the myapp application:
Create a ConfigMap named myapp-config:
```
kubectl create configmap myapp-config --from-literal=server-url=http://example.com --from-literal=timeout=5000
```
Creating a DaemonSet:
Apply daemonset.yaml to your Kubernetes cluster using the following command:
```
kubectl apply -f daemonset.yaml
```
Verify its status:
```
kubectl get daemonsets
```

Secrets:
The following command helps create a secret named myapp-secret, providing key-value pairs for sensitive data:
```
kubectl create secret generic myapp-secret --from-literal=username=myuser --from-literal=password=mysecretpassword
```
To verify:
```
kubectl get secret myapp-secret
```


