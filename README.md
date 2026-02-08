# Docker-Java-kubernetes-project

## Step 1: Create AWS EC2 instance

- EC2 type: Amazon Linux, m7i-flex-large
- EBS volume: 30GB
- Region: US-EAST-1

<img width="959" height="442" alt="ec2-instance" src="https://github.com/user-attachments/assets/bb210651-1397-4757-a7c7-45438e4d897d" />

## Step 2: Update packages and install docker

- yum update -y
- yum install docker -y
- systemctl start docker
- systemctl enable docker

## Step 3: Install conntrack and minikube

- yum install conntrack -y
- curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
- sudo install minikube-linux-amd64 /usr/local/bin/minikube
- /usr/local/bin/minikube start --force --driver=docker

## Step 4: Install Maven, Git and Java

- yum install git -y
- yum install maven -y
- yum install java -y

## Step 5: Install kubectl

- curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.20.4/2021-04-12/bin/linux/amd64/kubectl
- chmod +x ./kubectl
- mkdir -p $HOME/bin
- cp ./kubectl $HOME/bin/kubectl
- export PATH=$HOME/bin:$PATH
- echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
- source $HOME/.bashrc
- kubectl version --short –client

<img width="949" height="377" alt="kubectl-installed" src="https://github.com/user-attachments/assets/aca0a5d0-3655-4102-b819-ec131b729617" />

## Step 6: Clone Git repo

- git clone https://github.com/sjoseph-22/devops_project2.git

<img width="946" height="412" alt="git-repo-clone" src="https://github.com/user-attachments/assets/ed5e8d72-6a63-4eb0-948e-39a85430cf44" />

## Step 7: 

- cd git_repo/shopfront/
- mvn clean install -DskipTests
- docker build -t sjoseph22/shopfront:latest .
- docker push sjoseph22/shopfront:lates
<br>

- cd git_repo/productcatalogue/
- mvn clean install -DskipTests
- docker build -t sjoseph22/productcatalogue:latest .
- docker push sjoseph22/productcatalogue:latest
<br>

- cd git_repo/stockmanager/
- mvn clean install -DskipTests
- docker build -t sjoseph22/stockmanager:latest .
- docker push sjoseph22/stockmanager:latest

<img width="947" height="443" alt="dockerhub-repo" src="https://github.com/user-attachments/assets/d2b56ca6-3071-460f-8478-0311e4d5fdd0" />


## Step 8: 

- cd git_repo/kubernetes
- kubectl apply -f shopfront-service.yaml
- kubectl apply -f productcatalogue-service.yaml
- kubectl apply -f stockmanager-service.yaml
- kubectl get pods
- /usr/local/bin/minikube dashboard

<img width="947" height="418" alt="pods-created" src="https://github.com/user-attachments/assets/bd2f3400-13d0-4ac2-bd22-32a2ef5617e3" />

<img width="949" height="409" alt="kubectl-dashboard-url" src="https://github.com/user-attachments/assets/5a34bb1d-9b01-43a9-b2b5-c4c8df4d406a" />

## Step 9:

- kubectl proxy --address='0.0.0.0' --accept-hosts='^*$'

<img width="946" height="413" alt="set-proxy" src="https://github.com/user-attachments/assets/9f44fbb2-5391-4c59-91da-a6a3bf902763" />

## Step 10: Change security group of EC2 instance

EC2 instance -> Security -> Security group -> Edit inbound rules
Type: All Traffic
Source: Anywhere-IPv4

<img width="1918" height="882" alt="image" src="https://github.com/user-attachments/assets/4167acd8-18a0-4830-a691-6dd1a95d9140" />

## Step 11: Kubernetes dashboard

View kubernetes dashboard using the link:
- http://(EC2-IP):8001/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/#/pod?namespace=default

<img width="959" height="442" alt="kubernetes-dashboard" src="https://github.com/user-attachments/assets/473be497-984c-4b34-a9a2-28c8ec43f7a2" />


<img width="959" height="441" alt="kubernetes-dashboard-2" src="https://github.com/user-attachments/assets/a9e9b990-9e01-4567-b5d2-09528bcb329d" />














