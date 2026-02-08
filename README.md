# Docker-Java-kubernetes-project

Step 1: Create AWS EC2 instance

- EC2 type: Amazon Linux, m7i-flex-large
- EBS volume: 30GB
- Region: US-EAST-1

<img width="959" height="442" alt="ec2-instance" src="https://github.com/user-attachments/assets/bb210651-1397-4757-a7c7-45438e4d897d" />

Step 2: Update packages and install docker

- yum update -y
- yum install docker -y
- systemctl start docker
- systemctl enable docker

Step 3: Install conntrack and minikube

- yum install conntrack -y
- curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
- sudo install minikube-linux-amd64 /usr/local/bin/minikube
- /usr/local/bin/minikube start --force --driver=docker

Step 4: Install Maven, Git and Java

- yum install git -y
- yum install maven -y
- yum install java -y

Step 5: Install kubectl

- curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.20.4/2021-04-12/bin/linux/amd64/kubectl
- chmod +x ./kubectl
- mkdir -p $HOME/bin
- cp ./kubectl $HOME/bin/kubectl
- export PATH=$HOME/bin:$PATH
- echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
- source $HOME/.bashrc
- kubectl version --short –client

<img width="949" height="377" alt="kubectl-installed" src="https://github.com/user-attachments/assets/aca0a5d0-3655-4102-b819-ec131b729617" />

Step 6: Clone Git repo

- git clone https://github.com/sjoseph-22/devops_project2.git

<img width="946" height="412" alt="git-repo-clone" src="https://github.com/user-attachments/assets/ed5e8d72-6a63-4eb0-948e-39a85430cf44" />

Step 7: 

* cd shopfront/
* mvn clean install -DskipTests
* docker build -t sjoseph22/shopfront:latest .
* docker push sjoseph22/shopfront:latest

* cd productcatalogue/
* mvn clean install -DskipTests
* docker build -t sjoseph22/productcatalogue:latest .
* docker push sjoseph22/productcatalogue:latest

* cd stockmanager/
* mvn clean install -DskipTests
* docker build -t sjoseph22/stockmanager:latest .
* docker push sjoseph22/stockmanager:latest







