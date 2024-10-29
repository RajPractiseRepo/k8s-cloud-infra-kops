# 🚀 𝗙𝗿𝗼𝗺 𝗚𝗿𝗼𝘂𝗻𝗱 𝗨𝗽 𝘁𝗼 𝗣𝗿𝗼𝗱𝘂𝗰𝘁𝗶𝗼𝗻-𝗥𝗲𝗮𝗱𝘆: 𝗕𝘂𝗶𝗹𝘁 𝗮 𝗙𝘂𝗹𝗹𝘆 𝗙𝘂𝗻𝗰𝘁𝗶𝗼𝗻𝗮𝗹 𝗞𝘂𝗯𝗲𝗿𝗻𝗲𝘁𝗲𝘀 𝗖𝗹𝘂𝘀𝘁𝗲𝗿 𝗼𝗻 𝗔𝗪𝗦 𝘄𝗶𝘁𝗵 𝗞𝗼𝗽𝘀! 🚀  ☸🚢
![351607330-7ca733d1-e154-4989-8079-db4e90145448](https://github.com/user-attachments/assets/8442572e-f284-45c4-ad65-878ba89034a8)

• In this Project, I’ll Walk you through the steps of setting up a Kubernetes cluster on AWS using kops (Kubernetes Operations).

• KOPS, also known as Kubernetes operations, is an open-source project which helps you create, destroy, upgrade, and maintain a highly available production-grade Kubernetes cluster. Depending on the requirement, KOPS can also provision cloud infrastructure.


# Kubernetes Architecture:
![k8s-arch](https://github.com/user-attachments/assets/36ad4c5a-eac2-4e75-9a55-034a8a8e3e1f)


# Prerequisites:
•	AWS Account: We’ll use AWS EC2, S3, and Route 53 for this setup. \
•	Domain Name: You’ll need a domain name to configure DNS. I used Hostinger for domain management. \
•	IAM Role: Permissions to create resources on AWS. \
• Create a Linux EC2 Instance in AWS — we will use this as Client Machine. \
• Install Kops Binary on Client Machine \
•Install Kubectl Binary on Binary Machine


# Control and worker nodes servers:

![k8s-nodes](https://github.com/user-attachments/assets/76ddb60c-bde2-478e-8b70-e47a610cd6ff)

# Kuberenetes cluster Setup:
![k8s-cluster](https://github.com/user-attachments/assets/9ca26ea1-00cd-4f8a-80e2-aee3a63caed5)



### Kubernetes Commands Overview Used in the session

**Generate SSH Keys:**
These keys will be used by KOPS and applied to all servers.

```sh
ssh-keygen 
```

---

**Smoke Testing:**

1. **Get Nodes:**
   ```sh
   kubectl get nodes
   ```
   
2. **Get Nodes (No Headers):**
   ```sh
   kubectl get nodes --no-headers
   ```

3. **Cluster Info:**
   ```sh
   kubectl cluster-info
   ```

4. **Get Namespaces:**
   ```sh
   kubectl get ns
   ```
   Example namespaces: Alpha, Bravo, Charlie.

*Note:* If three teams are working on three different projects but using the same cluster, we can isolate with Namespaces. To allow communication between them, use Network Policies.

---

**Pods Information:**

1. **Get Pods (Default Namespace):**
   ```sh
   kubectl get pods
   ```
   Output: "Nothing is there" (if no pods are running)

2. **Get Pods (Kube-System Namespace):**
   ```sh
   kubectl get pods -n kube-system
   ```

3. **Get Pods (Kube-System Namespace, Detailed):**
   ```sh
   kubectl get pods -n kube-system -o wide | grep -i <component-name>
   ```
   Replace `<component-name>` with the specific component you're looking for.

---

**Deploy Resources in Kubernetes:**

1. **Imperative Approach:**
   ```sh
   kubectl run testpod1 --image=nginx:latest --dry-run=client -o yaml
   ```
   *Note:* This generates the YAML manifest without creating the pod.

2. **Declarative Approach (Using YAML or JSON):**
   Create a file `pod.yaml` with the following content:
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: testpod1
   spec:
     containers:
     - name: nginx
       image: nginx:latest
   ```
   Apply the manifest:
   ```sh
   kubectl apply -f pod.yaml
   ```

3. **Run Pod Directly:**
   ```sh
   kubectl run testpod1 --image=nginx:latest
   ```

4. **Get Pods:**
   ```sh
   kubectl get pods
   ```

---




