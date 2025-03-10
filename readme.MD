## Create Cluster
* Ec2 with all docker, kubectl, eksctl commands installed.
* Resize the /, /var (You can increase if you have any.)
* aws configure -- To authenticate with AWS
* Once all above steps compelted, Just logout and Ligin again your Ec2

# Docker Commands:
```
sudo dnf -y install dnf-plugins-core
```

```
dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
```

```
dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```


```
systemctl start docker
```

```
usermod -aG docker ec2-user
```

```
docker --version
```

# Resize Disk

```
lsblk
```

```
growpart /dev/nvme0n1 4
```
```
lvextend -l +50%FREE /dev/RootVG/rootVol 
```
```
lvextend -l +50%FREE /dev/RootVG/varVol
```

```
xfs_growfs /
```

```
xfs_growfs /var
```

# Install kubectl

```
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.32.0/2024-12-20/bin/linux/amd64/kubectl
```

```
chmod +x ./kubectl
```
```
mv kubectl /usr/local/bin/kubectl
```

```
kubectl version
```

# Install eksctl

```
USER_ID=$(id -u)
ARCH=amd64
```

```
curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"
```

```
tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz
```

```
mv /tmp/eksctl /usr/local/bin
```
```
eksctl version
```


# Install Kubens

```
sudo git clone https://github.com/ahmetb/kubectx /opt/kubectx
sudo ln -s /opt/kubectx/kubectx /usr/local/bin/kubectx
sudo ln -s /opt/kubectx/kubens /usr/local/bin/kubens
```