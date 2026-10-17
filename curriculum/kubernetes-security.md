# Kubernetes Security

## Table of Contents

- [Curriculum](#curriculum)
  - [01. Get the Client's Kubeconfig, Confirm Your kubectl Access, and Agree on Which Clusters You Can Test](#01-get-the-clients-kubeconfig-confirm-your-kubectl-access-and-agree-on-which-clusters-you-can-test)
  - [02. Use kubectl to Find Northstar's Pods, Services, Ingresses, Nodes, and Internet-Facing Apps](#02-use-kubectl-to-find-northstars-pods-services-ingresses-nodes-and-internet-facing-apps)
  - [03. Check Whether the Test Service Account Can Read Secrets or Change Resources Using kubectl auth can-i](#03-check-whether-the-test-service-account-can-read-secrets-or-change-resources-using-kubectl-auth-can-i)
  - [04. Find Privileged Pods, Root Containers, Host Mounts, and Missing Pod Security Restrictions](#04-find-privileged-pods-root-containers-host-mounts-and-missing-pod-security-restrictions)
  - [05. Check Whether the Shop Pod Can Reach the Database and Which Services Are Exposed Outside the Cluster](#05-check-whether-the-shop-pod-can-reach-the-database-and-which-services-are-exposed-outside-the-cluster)
  - [06. Check Who Can Read Kubernetes Secrets, Which Pods Mount Tokens, and Whether etcd Encrypts Secrets](#06-check-who-can-read-kubernetes-secrets-which-pods-mount-tokens-and-whether-etcd-encrypts-secrets)
  - [07. Scan the Shop Container Image with Trivy and Check Who Can Push Images to the Registry](#07-scan-the-shop-container-image-with-trivy-and-check-who-can-push-images-to-the-registry)
  - [08. Find Unsafe Settings in Helm Values and YAML, Then Check Who Can Approve Argo CD Changes](#08-find-unsafe-settings-in-helm-values-and-yaml-then-check-who-can-approve-argo-cd-changes)
  - [09. Check Kubelet Access, Node Permissions, and API Server or etcd Exposure on Approved Nodes](#09-check-kubelet-access-node-permissions-and-api-server-or-etcd-exposure-on-approved-nodes)
  - [10. Check Which AWS EKS or Azure AKS Identities Can Administer the Cluster and Access Cloud Resources](#10-check-which-aws-eks-or-azure-aks-identities-can-administer-the-cluster-and-access-cloud-resources)
  - [11. Find a Denied API Request in Kubernetes Audit Logs and Check Whether Falco Alerts on a Test Event](#11-find-a-denied-api-request-in-kubernetes-audit-logs-and-check-whether-falco-alerts-on-a-test-event)
  - [12. Run Kubescape and kube-bench, Then Manually Check the Reported RBAC and Pod Findings](#12-run-kubescape-and-kube-bench-then-manually-check-the-reported-rbac-and-pod-findings)
  - [13. Fix Findings, Retest the Cluster, and Deliver the Security Report](#13-fix-findings-retest-the-cluster-and-deliver-the-security-report)

## Curriculum

### 01. Get the Client's Kubeconfig, Confirm Your kubectl Access, and Agree on Which Clusters You Can Test

You’re joining Northstar Shop’s Kubernetes security review. Before testing a Pod, you’ll make sure your kubeconfig points to the client’s test cluster, learn what your account can see, and agree on what you may change.

Client scenario: Northstar gives SecureMinder a disposable staging cluster named northstar-staging, a read-only kubeconfig, an engineer contact, and namespaces shop, payments-test, and monitoring. All names and IP addresses in this course are training examples.

### 02. Use kubectl to Find Northstar's Pods, Services, Ingresses, Nodes, and Internet-Facing Apps

With the staging kubeconfig working, you’ll find the parts that run Northstar’s shop, see how requests reach them, and identify which Pods should never be reachable directly from the internet.

Client scenario: Northstar’s training cluster contains shop-web, orders-api, postgres-test, and an ingress controller. The engineer provides read-only access to the namespaces needed for the inventory.

### 03. Check Whether the Test Service Account Can Read Secrets or Change Resources Using kubectl auth can-i

Now you know what is running. You’ll check whether the shop-web service account and a normal developer have only the permissions their jobs require.

Client scenario: The engineer provides service accounts shop-web-sa and orders-api-sa, a developer-test user, and an RBAC policy that should allow reading shop Pods but not Secrets or changing Deployments.

### 04. Find Privileged Pods, Root Containers, Host Mounts, and Missing Pod Security Restrictions

After checking who may change Kubernetes objects, you’ll check what privileges a running container has and whether the cluster rejects unsafe Pod settings.

Client scenario: Northstar has a disposable debug Pod and normal shop-web and orders-api workloads. The engineer approves dry-run checks in a dedicated security-lab namespace.

### 05. Check Whether the Shop Pod Can Reach the Database and Which Services Are Exposed Outside the Cluster

You’ve checked Pod permissions. Next you’ll check traffic: the public web Pod should reach orders-api, while only orders-api should be able to contact the test database.

Client scenario: Northstar supplies two disposable connectivity-check Pods, a postgres-test Service on TCP 5432, and a network plugin that the engineer confirms enforces Kubernetes NetworkPolicy.

### 06. Check Who Can Read Kubernetes Secrets, Which Pods Mount Tokens, and Whether etcd Encrypts Secrets

You’ve checked network access. Now you’ll see which Pods and people can read credentials and whether the cluster encrypts Secret values stored in etcd.

Client scenario: Northstar provides a dummy database credential in a Secret, shop-web and orders-api service accounts, and an administrator who can show encryption settings without exposing key material.

### 07. Scan the Shop Container Image with Trivy and Check Who Can Push Images to the Registry

You’ve checked running Pods and secrets. Now you’ll trace the shop-web image back to the registry and find out whether unreviewed packages or image changes could reach the cluster.

Client scenario: Northstar supplies a disposable shop-web image, a registry read-only account, a sample Dockerfile, and a training CI job with a separate test repository.

### 08. Find Unsafe Settings in Helm Values and YAML, Then Check Who Can Approve Argo CD Changes

The image source is now checked. Next you’ll see how a changed YAML file becomes a running Pod and which people may approve production-style deployment changes.

Client scenario: Northstar uses a training Helm chart for shop-web and an Argo CD project that watches a disposable Git repository.

### 09. Check Kubelet Access, Node Permissions, and API Server or etcd Exposure on Approved Nodes

You’ve reviewed deployment changes. Now you’ll check the nodes and control-plane services that Kubernetes relies on, using the access the customer explicitly grants.

Client scenario: Northstar provides a dedicated test node, node-administrator read-only reports, and control-plane configuration details. Managed EKS/AKS components are reviewed through provider settings rather than assumed to be directly accessible.

### 10. Check Which AWS EKS or Azure AKS Identities Can Administer the Cluster and Access Cloud Resources

The cluster configuration is mapped. You’ll now check which cloud identities can change Kubernetes access or read Northstar’s storage.

Client scenario: Northstar supplies a disposable EKS cluster and a separate AKS training resource group, each with one app identity and one administrator identity. Test only the provider enabled for a given exercise.

### 11. Find a Denied API Request in Kubernetes Audit Logs and Check Whether Falco Alerts on a Test Event

After checking cloud identities, you’ll confirm that Northstar can see suspicious Kubernetes actions and respond before the problem becomes a larger incident.

Client scenario: Northstar provides a read-only audit-log viewer, a Falco test deployment on disposable nodes, and a security engineer who approves harmless test events.

### 12. Run Kubescape and kube-bench, Then Manually Check the Reported RBAC and Pod Findings

Now that you know the cluster and the available logs, you’ll use scanners to find missed settings and check their warnings against the real YAML and permissions.

Client scenario: Northstar permits a read-only Kubescape scan of approved namespaces and a kube-bench run on its disposable node. The engineer supplies the Kubernetes version and provider details.

### 13. Fix Findings, Retest the Cluster, and Deliver the Security Report

You’ve completed the manual and automated checks. Finally, you’ll help Northstar’s engineers fix three training issues, rerun the original tests, and deliver a report that shows what changed.

Client scenario: Northstar has queued fixes for shop-web's Pod security settings, a service account with too much access, and a missing network restriction between shop-web and postgres-test.
