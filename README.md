# How to install AWX Ansible
This manual describes how to install AWX ansible on windows or Linux OS
# Install AWX Ansible using VirtualBox and Vagrant
## Install VirtualBox
Download the installation for your OS from [here](https://www.virtualbox.org/wiki/Downloads)

Choose your OS from binary platform packages.
  
## Install Vagrant
Download the installation from [here](https://developer.hashicorp.com/vagrant/downloads)
Follow install instructions for your OS

### Setup VM for AWX Ansible

Make a new folder *Vagrant*
Download Vagrantfile from: [here](https://raw.githubusercontent.com/zukudm/awx/main/vagrant/Vagrantfile)

Copy that file to the just created *Vagrant* folder  
Run cmd.exe using the run command
```bash
cd c:\vagrant
vagrant up
```
After the VM setup finishes work run
```bash
vagrant ssh
```
Inside VM run commands:

```bash
git clone https://github.com/zukudm/awx.git
cd awx
ansible-galaxy install -r roles/requirements.yml
ansible-playbook install-docker.yml
```
Log out from VM (exit or Ctrl-d) then login again
```bash
vagrant ssh
```
Inside VM run
```bash
cd awx
ansible-playbook install-awx.yml
```
#### Possible problems:

In case the task "Check latest version" fails, run *ansible-playbook install-awx.yml* once again after "some time"
 <details>
 
   <summary> Error example </summary>
 <img src="images/check_latest_version_error.png">
  </details>
  
One of the longest tasks is *Waiting for AWX to start*
<details>
 <summary> Log example </summary>
 <img src="images/waiting_for_awx_services.png">
</details>

In case that task fails, you have to wait (???)
<details>
 <summary> Error example </summary>
 <img src="images/waiting_for_awx_error.png">
</details>

After some time we can check the AWX status using command
```bash
kubectl get pod --namespace=ansible-awx
```
All statuses must be in *Running* state

In case if one of them is not

<details>
 <summary> Error example </summary>
 <img src="images/faulty_status.png">
</details>

We have to wait more o run the script *ansible-playbook install-awx.yml" again

When all 3 applications (Awx-operator, ansible-awx*) will be in *running* state
<details>
 <summary> Log example </summary>
 <img src="images/good_status.png">
</details>

 You will be able to finish setup with
(It won't run if one of their status will be smth like Init:Imagexxxxxx)
```bash
ansible-playbook finish_install-awx.yml
```
You won't need to finish setup if *ansible-playbook install-awx.yml* finish without errors

