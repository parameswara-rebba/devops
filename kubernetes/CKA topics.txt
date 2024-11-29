https://medium.com/@kapare.sushant23/cka-certified-kubernetes-administrator-cheat-sheet-44c414d314fb

Search
Write

Parameswara Rebba
CKA (Certified Kubernetes Administrator) Cheat Sheet
Kapare Sushant
Kapare Sushant

·
Following

3 min read
·
Jul 4, 2024
53


1






1. Understanding Kubernetes Cluster Architecture
— Master node components: API server, etcd, scheduler, controller manager.
— Worker node components: kubelet, kube-proxy, container runtime.

2. Kubernetes Objects and Workloads
— Pods, Deployments, StatefulSets, DaemonSets, Jobs, CronJobs.
— Understand how to create, update, and maintain these workloads.

3. Networking in Kubernetes
— Pod networking concepts, CNI.
— Services and their types (ClusterIP, NodePort, LoadBalancer, ExternalName).
— Ingress controllers and Ingress resources.

4. Storage in Kubernetes
— Understand Persistent Volumes (PV), Persistent Volume Claims (PVC), StorageClasses.
— ConfigMaps, Secrets for configuration and sensitive data.

5. Security in Kubernetes
— RBAC (Role-Based Access Control) — Roles, ClusterRoles, RoleBindings, ClusterRoleBindings.
— Network Policies.
— Pod Security Policies.

6. Cluster Maintenance
— Cluster upgrade process.
— Backup and restore methodologies for Kubernetes and etcd.

7. Monitoring and Logging
— Basics of cluster-level logging and monitoring.
— Familiarize with tools like Prometheus and Grafana, ELK stack.

8. Troubleshooting
— Troubleshoot application failure.
— Troubleshoot control plane failure.
— Troubleshoot worker node failure.
— Troubleshoot networking.

Key kubectl Commands:
`kubectl get pods/deployments/services -n namespace` — List resources in a namespace.
- `kubectl describe pod/deployment <name> -n namespace` — Get detailed info about a resource.
- `kubectl create -f config.yaml` — Create resource from a YAML file.
- `kubectl apply -f config.yaml` — Apply changes from a YAML file.
- `kubectl delete pod/deployment <name>` — Delete a resource.
- `kubectl exec -it <pod_name> — /bin/bash` — Execute an interactive bash shell in the pod.
- `kubectl logs <pod_name>` — Get logs from a pod.
- `kubectl port-forward pod/<pod_name> 8080:80` — Port forward a local port to a pod.
- `kubectl drain <node_name>` — Prepare a node for maintenance.
- `kubectl cordon/uncordon <node_name>` — Mark node as unschedulable/schedulable.
- `kubectl top node/pod` — Display resource (CPU/Memory) usage.
Kubernetes Commands and Syntax for CKA Exam
General Management

kubectl get [resource]: List resources. For example, kubectl get pods.
kubectl describe [resource] [name]: Show detailed information about a resource. For example, kubectl describe pod my-pod.
Creating and Managing Resources

kubectl create -f [file.yaml]: Create a resource from a YAML file.
kubectl apply -f [file.yaml]: Apply a configuration to a resource from a YAML file.
kubectl delete [resource] [name]: Delete a resource. For example, kubectl delete pod my-pod.
kubectl edit [resource] [name]: Edit the configuration of a resource.
Namespaces

kubectl get namespaces: List all namespaces.
kubectl create namespace [name]: Create a new namespace.
Pods

kubectl run [name] --image=[image]: Run a pod with a specific image.
kubectl exec -it [pod-name] -- [command]: Execute a command in a running pod.
Deployments and Replicas

kubectl scale deployment [deployment-name] --replicas=[number]: Scale a deployment to the specified number of replicas.
kubectl rollout status deployment/[deployment-name]: Get the rollout status of a deployment.
kubectl rollout undo deployment/[deployment-name]: Rollback to the previous deployment.
Services

kubectl expose deployment [deployment-name] --type=[type] --port=[port]: Expose a deployment as a new Kubernetes service.
Logs and Debugging

kubectl logs [pod-name]: Fetch the logs of a pod.
kubectl logs -f [pod-name]: Stream the logs of a pod.
Node Management

kubectl get nodes: List all nodes in the cluster.
kubectl cordon [node-name]: Mark node as unschedulable.
kubectl drain [node-name]: Drain node in preparation for maintenance.
Resource Inspection

kubectl top pod: Display metrics for pods.
kubectl top node: Display metrics for nodes.
Configuration

kubectl config view: View Kubernetes configuration.
kubectl config use-context [context-name]: Switch to a different cluster context.
kubectl Cheat Sheet

Kubernetes has an official kubectl cheat sheet which is an invaluable resource: https://kubernetes.io/docs/reference/kubectl/cheatsheet/
Tips for Using kubectl Commands
Understand Contexts: Know how to switch contexts if you’re working with multiple clusters.
Use YAML Files for Complex Configurations: While imperative commands are useful, declarative configurations using YAML are more consistent and repeatable.
Explore kubectl Autocomplete: It can significantly speed up command entry.
Remember Selectors: They are powerful for filtering results, especially with get commands.
This cheat sheet covers the fundamental concepts and commands that are essential for the CKA exam and day-to-day Kubernetes administration. Remember, hands-on practice and familiarity with the official Kubernetes documentation are key to success in the CKA exam.

53


1




Kapare Sushant
Written by Kapare Sushant
96 Followers
·
2 Following
🚀 DevOps Engineer | Automation Enthusiast | Cloud Wizard ☁️ | Bridging Dev & Ops | Passionate about CI/CD & Infrastructure as Code 🛠️ | Learner 📚 |

Following
Responses (1)
Parameswara Rebba
Parameswara Rebba
﻿

Cancel
Respond
Respond

Also publish to my profile

Mutha Nagavamsi
Mutha Nagavamsi

3 months ago


Nice one. But when you talking about putting what you are learning into practice, "Cluster upgrade process" is not something everyone experience. Because in most cases it's managed by cloud.

1 reply

Reply

More from Kapare Sushant
Kubernetes Commands And Tricks For DevOps Engineer
Kapare Sushant
Kapare Sushant

Kubernetes Commands And Tricks For DevOps Engineer
This article will help in understanding most important and majorly used Kubernetes commands that would be required for a DevOps Engineer…
Aug 5
8


Kubernetes Best Practices
Kapare Sushant
Kapare Sushant

Kubernetes Best Practices
1. Version Control Manifests:
Oct 8
4


K8s Kubernetes Questions and Answers Part-I
Kapare Sushant
Kapare Sushant

K8s Kubernetes Questions and Answers Part-I
explain k8s architecture?
Jul 8
1


K8s Kubernetes Questions and Answers Part-II
Kapare Sushant
Kapare Sushant

K8s Kubernetes Questions and Answers Part-II
what is self-healing in k8s?
Jul 11


See all from Kapare Sushant
Recommended from Medium
Mastering Kubernetes Networking: Types, Setup, and Best Practices
Mohammed Talha Kalimi
Mohammed Talha Kalimi

Mastering Kubernetes Networking: Types, Setup, and Best Practices
Kubernetes networking plays a crucial role in ensuring smooth communication between containers, services, and external resources. In this…

Sep 14
79
1


DevOps and Cloud Resources 2024 (PDF Books)
Cumhur Akkaya
Cumhur Akkaya

DevOps and Cloud Resources 2024 (PDF Books)
I updated DevOps and Cloud resources. I added 51 new documents. In this article;🔎 You may find the pdf of the resources about DevOps Tools…

Sep 17
216
2


Lists


Staff picks
776 stories
·
1469 saves



Stories to Help You Level-Up at Work
19 stories
·
880 saves



Self-Improvement 101
20 stories
·
3093 saves



Productivity 101
20 stories
·
2599 saves
7 AWS VPC Best Practices Every Cloud Engineer Should Know
AWS in Plain English
In

AWS in Plain English

by

Rahul Sharma

7 AWS VPC Best Practices Every Cloud Engineer Should Know
Transform Your AWS VPC Setup with these seven steps

Nov 11
513
2


AWS Interview Questions!
DevPulse
In

DevPulse

by

Rsprasangi

AWS Interview Questions!
📍A company is moving from a monolithic architecture to a microservices architecture on AWS. Which services would you recommend to…

5d ago
12


The cover image of the article
Level Up Coding
In

Level Up Coding

by

Guillaume Vincent

Top 5 Kubernetes Best Practices for Ensuring High Availability and Scalability
Key Practices for Achieving Reliable and Scalable Kubernetes Deployments

Jul 26
86


Top 10 Kubernetes Pod Concepts That Confuse Beginners
Programming Domain
In

Programming Domain

by

howtouselinux

Top 10 Kubernetes Pod Concepts That Confuse Beginners
When I first started working with Kubernetes, it felt like trying to decode a secret language.

Aug 19
408
1


See more recommendations
Help

Status

About

Careers

Press

Blog

Privacy

Terms

Text to speech

Teams