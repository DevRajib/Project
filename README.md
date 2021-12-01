# Project

scp kubeconfig opc@150.230.239.7:/home/opc/kubeconfig

```
152.67.22.241


curl -sLS https://get.k3sup.dev | sh

{
export IP=150.230.239.7
export KUBECONFIG=`pwd`/kubeconfig
}


k3sup install --ip 150.230.239.7 --ssh-key ~/home/kali/id_rsa --user opc --sudo
k3sup join --ip 152.67.22.241 --server-ip 150.230.239.7 --server-user opc --ssh-key ~/home/kali/id_rsa --user opc --sudo

For host 
sudo apt install kubernetes-client



systemctl status firewalld
systemctl stop firewalld
systemctl disable firewalld



```
