# Kubernetes Manifests 

Understanding Kubernetes manifests:

**deployment.yaml** : Deployment file does is manage lifecycle, scaling and rolling updates for the application pod. It ensures that specified number of container replicas are running and healthy.

`kind: Deployment` -> Declares this resource as a kubernetes deployment.
`spec.replicas` -> defines what number of Identical Instances(pods) of the application must run simultaneously. (Set to 1 here)
`spec.selector` -> It tells the deployment which pod it controls by matching lables.
`spec.template` -> Acts as the blueprint for the pods, configuring the container image, name and application port.

```
# This is a sample deployment manifest file for a simple web application.
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
**service.yaml** : exp -----------
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

**ingress.yaml** : exp -----------
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

