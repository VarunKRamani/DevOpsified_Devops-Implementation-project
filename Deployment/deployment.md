# Project Deployment Instructions 

## Installing prerequisites
- Git
- Docker
- AWS CLI
- Eksctl
- Kubectl
_____

**Deployment process**: 
- Starting the deployment process from Cloning the repository to get the source code and needed files on our VM. (We are using Oracle VM VirtualBox - Ubuntu image)

- Starting with Dockerfile : build, run and push. 
- Moving to Kubernetes manifest: Deployment.yaml, Service.yaml and Ingress.yaml formation under k8s/manifest.
- Configuring the VM to our aws account for resource creation. `aws configure` enter the required fields
- EKS Cluster creation `command`
- Creation of deployment, service and ingress resources `commands`
- Expose the service and check it's working on the cluster.
- Start by Editing the service type to NodePort i.e. `type: NodePort` to change run `kubectl edit svc go-web-app`
- Run `kubectl get svc` check the port and type.
- Run `get nodes -o wide`, note the external IP
- To access the project, run `externalIP:port/cources` in the Browser. ✔️ The project can be Accessed i.e. from with in the cluster.

- Now we need to expose it to the public, Run `kubectl get ing`, the Address is not available for this we need an **Ingress Controller**.
- We are using **Nginx Ingress Controller**

- Install Nginx from the official repo.

**Configuration Ingress Controller** 
- Once the Nginx is installed, It will look into the Ingress resource and create a **Load balancer**.
- Run `kubectl get ing`, the address i.e. FQDN (Fully qualified domain name) will be available. 
- Set the DNS record on the local to access the project on the browser, **why?** -> The Ingress resource is set to accept the request only on host `go-web-app.local`.
- get the Ip of the address by running `nslookup address` copy the IP and run `sudo vim /etc/hosts`, paste the ip and address (IP Address) and save it.
- Now the project will be Accessible.
# 😃🥳❗

## Helm Process --
**Deployment** 
[note: make sure the previous deployment is deleted. Run `kubectl delete deploy go-web-app`, `kubectl delete svc go-web-app`, and `kubectl delete ing go-web-app`. To check run `kubectl get all`, except Kubernetes service there will be nothing left.]

- Create a folder/dir `helm`, run `mkdir helm`.
- `cd helm`
- Run `helm create go-web-app-chart`, and `cd go-web-app-chart`
- there will be `chart.yaml`, `charts`, `templates`, and `values.yaml`. Delete `charts`, run `rm -rf charts`.
-  make sure only `deployment.yaml`, `service.yaml`, and `ingress.yaml` are present in templates folder/dir.
-  Come to `/helm` dir and run `helm install go-web-app ./go-web-app-chart` to **Deploy the Application** and check by running `kubectl get all`.
-  And to uninstall/delete the deployment, run `helm uninstall go-web-app`. It will remove deployment, service and ingress. to check run `kubectl get all`. 

_____

## **CI - Continues Integration (GitHub Actions)**

- Set the directory .github/workflows/cicd.yaml
- Under which all the jobs are described. Build, code-quality, push and  update-newtag-in-helm-chart.




