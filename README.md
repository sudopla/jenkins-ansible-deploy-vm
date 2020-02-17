Spin up and configure Windows virtual machines in VMware environmnet
------------------------

This script allows you deploy and configure a virtual machine automatically in your VMware environment. The user would run the Jenkins Job as shown in the picture below. The Jenkins job executes Ansible playbooks to perform the different configuration tasks. 

<img src="img/build.png" width="80%">

**Jenkins Job Steps**

1. Download job's files from repository
2. Spin up virtual machine and join the VM to the Windows domain
3. Configure Window OS in the VM (expand drives, add users to admin and RDP groups, configure local administrator password)
4. Move VM to proper OU in AD

**Requirements**

* Have a Windows template ready
* Install [pyVmomi](https://github.com/vmware/pyvmomi) in Jenkins server
* Install [Kerbereos Library](https://docs.ansible.com/ansible/latest/user_guide/windows_winrm.html#installing-the-kerberos-library) in Jenkins server
* [Configure Kerberos](https://docs.ansible.com/ansible/latest/user_guide/windows_winrm.html#configuring-host-kerberos)
* Modify Ansible playbooks for your environment

**Create Jenkins DLS Job (Seed Job)**

The [Job DSL](https://plugins.jenkins.io/job-dsl/) plugin allows you to define Jenkins jobs as code. You will have to install this plugin and then configure the seed job. The [DSL job](seedjob) defined in this project will create the spin_up_vm job which is the one the user will run to deploy new virtual machines.   

Install Job DSL plugin
![dsl-job](img/dsl-job-1.png)

If you already have a seed job you just need to add the code in the file [seedjob](seedjob) to your existing job if not you need to create a new DSL job.
<img src="img/dsl-job-01.png" width="100%">

<img src="img/dsl-job-2.png" width="60%">

Speficy the repository URL where the seed job file will be saved. 

<img src="img/dsl-job-3.png" width="100%">

Specify the name of the seed job file

<img src="img/dsl-job-4.png" width="100%">

You also need to disable the option shown below. (Manage Jenkins -> Configure Global Security) 

<img src="img/dsl-job-5.png" width="60%">

**Ansible Playbooks**

To deploy the VMs in the VMware environment I am using the [vmware_guest](https://docs.ansible.com/ansible/latest/modules/vmware_guest_module.html) ansible module. 

You will 


**Configure Kerberos**
