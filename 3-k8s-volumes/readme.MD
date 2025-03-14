# kubernetes Volumes:
## EBS
* EBS Static
1. create Volume in AWS and
2. Insatll EBS drivers
3. EKS should access EBS, so Add permsion to your nodes. Give IAM role policy: EBSCSIDriver ploicy.
4. Create PV manifest file
5. create PVC manifest file
6. Claim through pod
7. Check with Service

* EFS Dynamic
1. create Storage Calss yaml code(SC will take care of Volume)
2. Insatll EBS drivers
3. EKS should access EBS, so Add permsion to your nodes. Give IAM role policy: EBSCSIDriver ploicy.
4. Create PVC manifest file
5. Claim through pod
6. Check with Service

## EFS
* EFS Static Provisioning
1. create EFS file system in AWS
2. Insatll EFS drivers
3. EKS should access EFS, so Add permsion to your nodes. Give IAM role policy: EBSCSIDriver ploicy.
4. NFS SG should allow traffic from EKS nodes (2049)
5. Create PVC manifest file
6. Claim through pod
7. Check with Service


* EFS Dynamic Provisioning
1. Create EFS file system in AWS
2. Insatll EFS drivers
3. EKS should access EFS, so Add permsion to your nodes. Give IAM role policy: EBSCSIDriver ploicy.
4. NFS SG should allow traffic from EKS nodes (2049)
5. Create SC manifest file
5. Create PVC manifest file
6. Claim through pod
7. Check with Service


# StatefulSet 
It has headless service along with normal service
