# How to install AWX Ansible

## Install VirtualBox
## Install Vagrant
### Setup VM for AWX Ansible

Make new folder c:\vagrant
Download vagrantfile from: and copy it to the just created folder c:\vagrant
Run cmd.exex via run command
```bash
cd c:\vagrant
vagrant up
```
After VM setup finishes work run
```bash
vagrant ssh
```
Inside VM run commands:

```bash
git clone https://github.com/zukudm/awx.git
cd awx
ansible-galaxy install -r roles/requirements.yml
ansible-playbook install-docker.yml
ansible-playbook install-awx.yml
```
In case install-awx get any errors wait for some time (it could take several hours) run  
```bash
kubectl get pod --namespace=ansible-awx
```
Whell all 3 applications (Awx-perator, ansible-awx*) will be in ready state, you will be able to finish setup with
(It won't ryn if one of them status will be smth like Init:Imagexxxxxx)
```bash
ansible-playbook finish_install-awx.yml
```

