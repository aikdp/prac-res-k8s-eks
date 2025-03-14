# AWS Load Balancer Controller

* Should install LB controller along with some OIDC, IAM Policies, IAM Role, Service Account, Helm to install AWS Load balancer Controller etc.

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

* Check: Once the above steps completed. You will get below info of AWS LB Controller running.
```
kubectl get pods -n kube-system
```
NAME                                            READY   STATUS    RESTARTS   AGE
aws-load-balancer-controller-5fd7794f55-277qq   1/1     Running   0          24s
aws-load-balancer-controller-5fd7794f55-9wzwm   1/1     Running   0          24s
aws-node-jspd2                                  2/2     Running   0          16m
aws-node-q252t                                  2/2     Running   0          16m
coredns-789f8477df-bg5jh                        1/1     Running   0          21m
coredns-789f8477df-vw699                        1/1     Running   0          21m
eks-pod-identity-agent-25sjl                    1/1     Running   0          16m
eks-pod-identity-agent-qqkz2                    1/1     Running   0          16m
kube-proxy-7dgzm                                1/1     Running   0          17m
kube-proxy-z4zdb                                1/1     Running   0          17m

