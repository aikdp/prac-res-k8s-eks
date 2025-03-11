# RBAC Role Based Access Control
* Role and RoleBinding are Namespace Level
* ClusterRole and Cluster RoleBinding are Cluster Level
* Based on the users and their desigantions, we will provide access to the resources that are in Namespace and cluster levels.

* Resources: nodes, pods, pv, pvc, deployments, namespaces, services, crontabs, configmaps, jobs, endpoints, etc These are all respources in a cluster.

* Verbs: get, list, watch, delete, create, patch, update, deletecollection, view, post, these are actions that will peroform on resources.


## STPES:
1. Create IAM policy to Describe Clusetr of your cluster with policy name eg: DescribeExpenseEKSCluster.

2. Create a user and add policy to user them.

3. Create a Role to which resources should have some acces to that user.

4. Create RoleBinding to that user, then only users can able access.

5. Same for ClusterRole and ClusterroleBinding.


