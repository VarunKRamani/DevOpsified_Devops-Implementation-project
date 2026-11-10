# Kubernetes Manifests 

Understanding Kubernetes manifests:

**deployment.yaml** : Deployment file does is manage lifecycle, scaling and rolling updates for the application pod. It ensures that specified number of container replicas are running and healthy.

- `kind: Deployment` -> Declares this resource as a kubernetes deployment.
- `spec.replicas` -> defines what number of Identical Instances(pods) of the application must run simultaneously. (Set to 1 here)
- `spec.selector` -> It tells the deployment which pod it controls by matching lables.
- `spec.template` -> Acts as the blueprint for the pods, configuring the container image, name and application port.

```
# Deployment manifest file for go-web-app.
apiVersion: apps/v1
kind: Deployment
metadata:
  name: go-web-app
  labels:
    app: go-web-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: go-web-app
  template:
    metadata:
      labels:
        app: go-web-app
    spec:
      containers:
      - name: go-web-app
        image: <docker-user-name>/go-web-app
        ports:
        - containerPort: 8080
```
**service.yaml** : Service acts as an Internal Load Balancer and steady Network abstraction layer. Because Pods are ephemeral ( IP changes when they restart). Service provides a stable internal IP and DNS name to route traffic to the correct pods.

- `kind: Service` -> Declares this resource as Kubernetes service.
- `spec.type: ClusterIP` -> Expose the service on a cluster-internal IP, making it reachable from only within Kubernetes Cluster.
- `spec.selector` -> Finds the Pods to which the trafice has to be routed by matching their lables.
- `spec.ports` -> Mapes the incoming target ports to the containers target listening port. 
```
# Service for the application
apiVersion: v1
kind: Service
metadata:
  name: go-web-app
  labels:
    app: go-web-app
spec:
  ports:
  - port: 80
    targetPort: 8080
    protocol: TCP
  selector:
    app: go-web-app
  type: ClusterIP
```

**ingress.yaml** : It manages external the HTTP/HTTPS access from outside the cluster to the services inside the cluster, acting as an smart layes-7 router that handles rules like domain-based routing and path mapping. 

- `kind: Ingress` -> Declares the resource type.
- `metadata.annotations` -> Configuration instructions from the controller, such as URL path rewriting. 
- `spec: ingressClassName` -> specifies which ingress controller implimentation should process this resource.
- `spec: rules` -> Defines the traffic routing rules. (In this case `go-web-app.local` via path `\` to the internal `go-web-app` service on port `80`)
```
# Ingress resource for the application
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: go-web-app
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx
  rules:
  - host: go-web-app.local
    http:
      paths: 
      - path: /
        pathType: Prefix
        backend:
          service:
            name: go-web-app
            port:
              number: 80
```

