---
title: "Minikube Set-up for Dev Environmnet"
seoTitle: "minikube install"
seoDescription: "minikube on linux"
datePublished: Sat Jan 13 2024 17:24:14 GMT+0000 (Coordinated Universal Time)
cuid: clrcc77iv00040aib00qx67ti
slug: minikube-set-up-for-dev-environmnet
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/pz6m6bTsJA8/upload/9bc91f44a716af18f10be219a8c98cb9.jpeg
tags: docker, kubernetes, devops, containers, devsecops, minikube

---

# **Why Minikube? 🤔**

Minikube is local Kubernetes, focusing on making it easy to learn and develop for Kubernetes.

All you need is Docker (or similarly compatible) container or a Virtual Machine environment.

For more about [minikube](https://minikube.sigs.k8s.io/docs/start/)

**Warning :** Not recommended run in production env. Running on dev purpose only.

# **What you’ll need 📃**

* 2 CPUs or more
    
* 2GB of free memory
    
* 20GB of free disk space
    
* Internet connection
    
* Container or virtual machine manager, such as: [Docker](https://minikube.sigs.k8s.io/docs/drivers/docker/), [QEMU](https://minikube.sigs.k8s.io/docs/drivers/qemu/), [Hyperkit](https://minikube.sigs.k8s.io/docs/drivers/hyperkit/), [Hyper-V](https://minikube.sigs.k8s.io/docs/drivers/hyperv/), [KVM](https://minikube.sigs.k8s.io/docs/drivers/kvm2/), [Parallels](https://minikube.sigs.k8s.io/docs/drivers/parallels/), [Podman](https://minikube.sigs.k8s.io/docs/drivers/podman/), [VirtualBox](https://minikube.sigs.k8s.io/docs/drivers/virtualbox/), or [VMware Fusion/Workstation](https://minikube.sigs.k8s.io/docs/drivers/vmware/)
    

In this blog we can see, **How to run Minikube using Docker**.

# **Requirements: ⬇️**

* Install Docker-engine
    

***Note:*** *Minikube run as ordinary user not root.*

# **Step 1: Set Up Docker Environment 1️⃣**

## **Remove old versions:**

```bash
sudo yum remove -y docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

## **Set-up Repo:**

```bash
sudo yum install -y yum-utils
sudo yum-config-manager - add-repo https://download.docker.com/linux/centos/docker-ce.reposudo 
```

## **Install and start Docker Engine:**

* Use docker 18.09 or higher (20.10 or higher is recommended)
    

```bash
#Install Docker.io
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Start and Enable docker at boot
sudo systemctl enable docker && sudo systemctl start docker
```

# **Step 2: Installing Minikube 2️⃣**

```bash
#Download Minikube 
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

#Provide Exeute permission
chmod +x minikube-linux-amd64

#Make as internal command
sudo mv minikube-linux-amd64 /bin/minikube

#check minikube version
minikube version
```

# **Step 3: Start Minikube 3️⃣**

Run the below command to start Minikube.

Note: Minikube initialization it will sometime, please wait and don’t interrupt

```bash
minikube start - driver=docker
```

# **Step 4: Set kubectl command 4️⃣**

In default minikube command as follow, but it will not convenient for all

```bash
minikube kubectl -- get pods -A
```

Let’s make a change.

```bash
alias kubectl='minikube kubectl --'
alias k='minikube kubectl --'

#Set up in bashrc for permanent 
echo "alias kubectl='minikube kubectl --'"   >> ~/.bashrc
echo "alias k='minikube kubectl --'" >> ~/.bashrc
```

## **Set docker driver as default 🤝**

To set a docker driver default, run the below commands.

```bash
minikube config set driver docker
```

# **Minikube Commands: ✌️**

* **miniube status** — Check status of minikube
    
* **minikube ip** — Check ip of minikube cluster
    
* **minikube dashboard**\- Access the Kubernetes dashboard running within the minikube cluster
    
* **minikube service lis**t — Check the services list
    
* **minikube stop** — Stop minikube cluster
    
* **minikube ssh** — login to minikube Node
    
* **minikube service &lt;service-name&gt; — — url** → Returns a URL to connect to a service
    
* **minikube tunner** - Connect to LoadBalancer services
    
* **minikube images** — check the images
    
* **minikube pause/unpause** - pause/unpause Kubernetes
    
* **minikube delete** — Deletes a local Kubernetes cluster
    

# **Debug**

## **Error: X Exiting due to PROVIDER\_DOCKER\_NOT\_RUNNING:**

```bash
* minikube v1.32.0 on Centos 7.9.2009
* Using the docker driver based on user configuration

X Exiting due to PROVIDER_DOCKER_NOT_RUNNING: deadline exceeded running "docker version --format <no value>-<no value>:<no value>": signal: killed
* Suggestion: Restart the Docker service
* Documentation: https://minikube.sigs.k8s.io/docs/drivers/docker/
```

For this error try to Restart your docker , it will fix then start Minikube again.

---

Follow for More 👉

[![Karthick Dk](https://miro.medium.com/v2/resize:fill:55:55/1*wjjLaOLpOggypEpFfAmu5A.jpeg align="left")](https://www.linkedin.com/in/karthick-dkk/)

* * Medium —  [https://karthidkk123.medium.com/](https://karthidkk123.medium.com/)
        
    * LinkedIn — [linkedin.com/in/karthick-dkk](https://karthidkk123.medium.com/)
        
    * Instagram — [instagram.com/karthick\_dkk\_dk](https://karthidkk123.medium.com/)
        
    * Hashnode: [https://karthick-dk.hashnode.dev/](https://karthidkk123.medium.com/)
        
    * Dev.to : [https://dev.to/karthickdkk](https://karthidkk123.medium.com/)
        
    * StackOverflow : [https://stackoverflow.com/users/17715768/karthick-d](https://karthidkk123.medium.com/)