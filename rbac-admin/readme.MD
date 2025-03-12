# RBAC Role Based Access Control
* Role and RoleBinding are Namespace Level
* ClusterRole and Cluster RoleBinding are Cluster Level
* Based on the users and their desigantions, we will provide access to the resources that are in Namespace and cluster levels.

* Resources: nodes, pods, pv, pvc, deployments, namespaces, services, crontabs, configmaps, jobs, endpoints, etc These are all respources in a cluster.

* Verbs: get, list, watch, delete, create, patch, update, deletecollection, view, post, these are actions that will peroform on resources.


## STPES:
1. Create IAM policy to Describe EKS Cluster with policy name eg: DescribeExpenseEKSClusterPolicy.

2. Create a user and add DescribeExpenseEKSClusterPolicy to user

3. Create a Role to which resources should have acces to user and what are all actions and api Groups as well.

4. Create RoleBinding to user, then only users can able access.

5. Same for ClusterRole and ClusterroleBinding.

Once all above steps completed. You should configure configamp with manually or eksctl command as well.

Manually:
1. kubectl get configmap aws-auth -n kube-system -o yaml
2. Add User Groups to configmap. So user can able to access your described cluster based on the roles and rolebindings.
```
apiVersion: v1
data:
  mapRoles: |
    - groups:
      - system:bootstrappers
      - system:nodes
      rolearn: arn:aws:iam::537124943253:role/eksctl-expense-dev-nodegroup-spot-NodeInstanceRole-XEplbFwzJfV4
      username: system:node:{{EC2PrivateDNSName}}
  mapUsers: |
    - groups:
      - rl-pod
      userarn: arn:aws:iam::537124943253:user/suresh
      username: suresh
    - groups:
      - role-all
      userarn: arn:aws:iam::537124943253:user/ramesh
      username: ramesh
kind: ConfigMap
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"mapRoles":"- groups:\n  - system:bootstrappers\n  - system:nodes\n  rolearn: arn:aws:iam::537124943253:role/eksctl-expense-dev-nodegroup-spot-NodeInstanceRole-XEplbFwzJfV4\n  username: system:node:{{EC2PrivateDNSName}}\n","mapUsers":"- groups:\n  - rl-pod\n  userarn: arn:aws:iam::537124943253:user/suresh\n  username: suresh\n"},"kind":"ConfigMap","metadata":{"annotations":{},"creationTimestamp":"2025-03-11T09:45:16Z","name":"aws-auth","namespace":"kube-system","uid":"08e68376-c0ff-4369-b09e-576eb0a0532e"}}
  creationTimestamp: "2025-03-11T09:45:16Z"
  name: aws-auth
  namespace: kube-system
  # resourceVersion: "9349" #remove version here, it automatically updates, when u apply
  uid: 08e68376-c0ff-4369-b09e-576eb0a0532e
```
3. Apply: kubectl apply -f <configmap-name>  or
You can directly edit: 
```
kubectl edit -n kube-system configmap/aws-auth
```

4. Once above stpes completed. Ask user to check whether they are able to access or not.

Users: users must configure kubectl commands (client to communicate eks cluster)
```
aws eks update-kubeconfig --region <region-code> --name <cluster-name>

aws eks update-kubeconfig --region us-east-1 --name expense-dev
```

5. Now user can see .kube/config file has been updated.
6. Hence, user can able to authorization to do some actions on eks cluster.


