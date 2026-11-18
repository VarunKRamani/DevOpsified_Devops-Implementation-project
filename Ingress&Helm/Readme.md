# Understanding Ingress controller

  
- It acts an critical **bridge between external traffic and the Internal Service**, running on the kubernetes cluster.
- It acts like a entry gate for **external traffic** and **directs** requests to the correct **services** inside.
- It watches the Ingress resource configuration and **automatically create Load Balancer to handle the incoming requests**.
- **Path-Based Routing** : It can look at the URL path (like /shop or /menu) and route traffic to entirely different service.
- **Host-Based Routing**: It can look at the domain name (like app.example.com vs. admin.example.com) and send traffic to the appropriate backend.

<img width="1408" height="768" alt="Gemini_Generated_Image_mz14symz14symz14" src="https://github.com/user-attachments/assets/88cc3e4d-da65-4fa0-8a2c-c869dd0e9f5b" />

## Nginx Ingress Controller 
**Nginx IC**: widely used for it's lightweight, speed and ability to handle massive amount traffic without crashing or slowing down.

- **Lightweight:**  ------------
- **built to be a Traffic cop:**---------------
- **Handles thousands of connections at once:**---------------------

_____

**The Complete Traffic Journey. Once everything is applied, when a request hits your cluster:**

- Traffic arrives from outside the cluster at your Load Balancer (managed by the Ingress controller).
- It flows directly into the NGINX Ingress Controller pods.
- NGINX matches the domain/path using your Ingress rules (go-web-app.local).
- NGINX forwards the request to your internal Service (ClusterIP on port 80).
- The Service balances and routes the traffic straight to your application Pod on port 8080

<img width="1376" height="768" alt="Traffic flow" src="https://github.com/user-attachments/assets/1d36e723-102c-46a1-abfa-fadae009a262" />



_____

## Helm 

Helm is a took that is used to **manage and deploy application on Kubernetes cluster**.

It packages all the kubernetes resources files (like deployment.yaml, service.yaml and ingres .yaml) into a single logical unit called **chart**.

It uses a values.yaml filr to inject dynamic configuration.

Key Components: 
- templates --> 
- values.yaml -->
- chart.yaml --> 
