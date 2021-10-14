# 🔥 Kubernetes Course 🔥 
[Kubernetes](https://kubernetes.io/), also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications.

### [Kubernetes Documentation](https://kubernetes.io/docs/home/)

## Getting started 🔥
 we will need [minikube](https://minikube.sigs.k8s.io/docs/start/) and  kubectl.

- [How to set up my local environment](https://www.youtube.com/watch?v=X48VuDVv0do&t=2087s&ab_channel=TechWorldwithNana)
- [Kubectl basic commands](https://www.youtube.com/watch?v=X48VuDVv0do&t=2692s&ab_channel=TechWorldwithNana)
- [Configuration files](https://www.youtube.com/watch?v=X48VuDVv0do&t=3723s&ab_channel=TechWorldwithNana)

## External service

We need to specify the field `type` and a `nodePort` when creating an external service.
```yaml
apiVersion: v1
kind: Service
metadata:
  name: mongo-express-service
spec:
  selector:
    app: mongo-express
  type: LoadBalancer  
  ports:
    - protocol: TCP
      port: 8081
      targetPort: 8081
      nodePort: 30000
```
when we the service is created, we can see that it doesn't have a public IP yet. We need to specify using `minikube`.
```bash
❯ kubectl get service
NAME                    TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
kubernetes              ClusterIP      10.96.0.1        <none>        443/TCP          25h
NAME-OF-THE-SERVICE   LoadBalancer   10.107.26.64     <pending>     8081:30000/TCP   3m7s
mongodb-service         ClusterIP      10.101.116.156   <none>        27017/TCP        18h
```
```bash
minikube service NAME-OF-THE-SERVICE
```
## ⚠️ IT'S NOT RECOMMENDED TO USE EXTERNAL SERVICES
We can use Ingress to forward request from the browser to an internal service.
https://kubernetes.io/docs/concepts/services-networking/ingress/