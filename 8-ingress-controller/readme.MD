# AWS Load Balancer Controller

* Should install LB controller along with some OIDC, IAM Policies, etc.

1. Create an IAM OIDC provider. You can skip this step if you already have one for your cluster.
```
eksctl utils associate-iam-oidc-provider \
    --region us-east-1 \
    --cluster expense-dev \
    --approve
```
2. If your cluster is in any other region:
```
curl -o iam-policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.12.0/docs/install/iam_policy.json
```
3. Create an IAM policy named AWSLoadBalancerControllerIAMPolicy. If you downloaded a different policy, replace iam-policy with the name of the policy that you downloaded.
```
aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam-policy.json
```
4. Create an IAM role and Kubernetes ServiceAccount for the LBC. Use the ARN from the previous step.
```
eksctl create iamserviceaccount \
--cluster=expense-dev \
--namespace=kube-system \
--name=aws-load-balancer-controller \
--attach-policy-arn=arn:aws:iam::537124943253:policy/AWSLoadBalancerControllerIAMPolicy \
--override-existing-serviceaccounts \
--region us-east-1 \
--approve
```

5. Add the EKS chart repo to Helm.
```
helm repo add eks https://aws.github.io/eks-charts
```

6. Helm install command for clusters with IRSA: (Note: if Service account not created then, put true)
```
helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=expense-dev --set serviceAccount.create=false --set serviceAccount.name=aws-load-balancer-controller
```
(ref: https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/deploy/installation/)

Check:
```
kubectl get pods -n kube-system
```
NAME                                            READY   STATUS    RESTARTS   AGE
aws-load-balancer-controller-5f8ccd4f94-6jndb   1/1     Running   0          43s
aws-load-balancer-controller-5f8ccd4f94-rs4d4   1/1     Running   0          43s
aws-node-jdlnx                                  2/2     Running   0          24m
coredns-586b798467-5dlzs                        1/1     Running   0          17m
coredns-586b798467-mq5bb                        1/1     Running   0          16m
kube-proxy-tl87r                                1/1     Running   0          24m
metrics-server-7b6c698b65-b8g8f                 1/1     Running   0          17m
metrics-server-7b6c698b65-gq7lt                 1/1     Running   0          16m
