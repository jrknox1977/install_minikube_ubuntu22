# install_cb_containers_minikube

### Ubuntu 22 AWS EC2
I am using AWS EC2 ubuntu 22, but you should be able to use any fresh install of Ubuntu 22 to follow along.

## Commands: 
#### Update the system:
- `sudo apt update && sudo apt -y upgrade`
#### Check if reboot is required: 
- `[ -f /var/run/reboot-required ] && sudo reboot -f`  See note below if you want to understand this command better. 

### Install Docker
- `sudo apt -y install apt-transport-https ca-certificates curl software-properties-common`
- `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg`
- `echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`
- `sudo apt update`
- `sudo apt -y install docker-ce`
- `sudo systemctl status docker`
- `sudo systemctl enable docker`
#### Add user to docker group
- `sudo usermod -aG docker ${USER}`
- log out and back in for group to take effect or `su - ${USER}`

### Download minikube on Ubuntu 22.04|20.04|18.04
- `wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64`
- `chmod +x minikube-linux-amd64`
- `sudo mv minikube-linux-amd64 /usr/local/bin/minikube`
#### Confirm version installed
- `minikube version`

### Install kubectl on Ubuntu
- `curl -LO https://storage.googleapis.com/kubernetes-release/release/`
- `chmod +x ./kubectl`
- `sudo mv ./kubectl /usr/local/bin/kubectl`
#### Check kubectl version
- `kubectl version -o json --client`

### Starting minikube on Ubuntu 22.04|20.04|18.04
- `minikube start`
- `minikube addons list`
#### Minikube Basic operations
- `kubectl cluster-info`
- `kubectl config-view`
- `kubectl get nodes`
#### Access minikube VM using ssh
- `minikube ssh`
- Then inside VM: `sudo su -`





##### Note on reboot command:
- `[ -f /var/run/reboot-required ]` checks to see if a reboot is required. If it is required it will return `True`, if no reboot is required it will return `False`
-  `&& sudo reboot -f` The doubele `&` (`&&`) means only continue to the next command if the previous command was succesful (returned `True`) if the previous command failed (return `False`) then stop executing the command. The `-f` on the `reboot` command means `force reboot`
