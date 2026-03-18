# eks-kubernetes-nginx-clustercreation-lab

# 🚀 EKS Cluster Setup + Kubernetes Basic Commands

This guide shows how to:

* Create an Amazon EKS Cluster
* Connect using kubectl
* Run a basic nginx pod
* Expose and test it

---

# 🧱 Step 1: Launch EC2 Instance

* Launch Ubuntu EC2 instance in AWS
* Allow SSH (port 22)

---

# ⚙️ Step 2: Install eksctl

```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
```

---

# ⚙️ Step 3: Install kubectl

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```

---

# ⚙️ Step 4: Install AWS CLI

```bash
sudo apt install unzip -y
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

---

# 🔐 Step 5: Configure AWS

```bash
aws configure
```

Enter:

* Access Key
* Secret Key
* Region → ap-south-1

---

# ☸️ Step 6: Create EKS Cluster

```bash
eksctl create cluster \
--name eks-cluster-demo \
--region ap-south-1 \
--version 1.29 \
--nodegroup-name linux-nodes \
--node-type t2.micro \
--nodes 1
```

---

# 🔗 Step 7: Connect to Cluster

```bash
aws eks update-kubeconfig --name eks-cluster-demo
```

---

# ✅ Step 8: Verify Cluster

```bash
kubectl get nodes
```

---

# 🚀 Step 9: Run NGINX Pod

```bash
kubectl run nginx-pod --image=nginx
```

---

# 📦 Step 10: Check Pods

```bash
kubectl get pods
kubectl get pods -o wide
```

---

# 🌐 Step 11: Expose Pod

```bash
kubectl expose pod nginx-pod --type=NodePort --port=80
```

---

# 📡 Step 12: Check Services

```bash
kubectl get svc
```

---

# 🌐 Access Application

http://<EC2-PUBLIC-IP>:<NODE-PORT>

⚠️ Open NodePort in Security Group

---

# 🔍 Test Pod

```bash
kubectl exec -it nginx-pod -- curl localhost
```

---

# 🖥️ Enter Pod

```bash
kubectl exec -it nginx-pod -- bash
```

---

# ❌ Delete Pod

```bash
kubectl delete pod nginx-pod
```

---

# 🧹 Delete Cluster

```bash
eksctl delete cluster --name eks-cluster-demo --region ap-south-1
```
