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
