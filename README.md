# Rancher Kubernetes Setup
Rancher is a Kubernetes management tool to deploy and run clusters anywhere and on any provider. Here we setup Rancher on a Linux virutal machine. 

Assuming we have SSH access to the VM.
1. Login with ssh to the VM. Install curl
```
sudo apt install curl
```
2. Install docker that Rancher recommends. Find it here https://ranchermanager.docs.rancher.com/getting-started/installation-and-upgrade/installation-requirements/install-docker
```
curl https://releases.rancher.com/install-docker/20.10.sh | sh
```
3. Add user to Docker user group
```
sudo usermod -aG docker $USER && newgrp docker
```
4. Run rancher docker container. https://www.rancher.com/quick-start
```
sudo docker run --privileged -d --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher
```
5. Open a browser and browse to your VM ip address. Ignore ssl warning.
6. The login setup require us to know the containerId of the rancher that is running on the docker. Then run the command (with the containerId replaced) shown in the login setup, which will give us a bootstrap password. 
7. Enter the bootstrap password. After login you can choose your own password.


### How to connect Rancher cluster from local Kubectl client.
Assuming you already have the Kubectl client. If not download it from here https://kubernetes.io/docs/tasks/tools/

Download the KubeConfig yaml file from Rancher. There are usually 3 ways we can connect to different clusters.

Option 1: Using the kubeconfig on every command
```
kubectl get nodes --kubeconfig={LOCATION TO KUBECONFIG.yaml}
```
Option 2: Using environment variable. Set environment variable KUBECONFIG with the location to kubeconfig file.

Option 3: Merging multiple kubeconfig files

For more check out the link https://dbafromthecold.com/2020/02/21/merge-kubectl-config-files-on-windows/

To list all the contexts ```kubectl config get-contexts```

ENJOY!


