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

- -------------
