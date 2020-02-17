Spin up and configure Windows virtual machines in VMware environmnet
------------------------

This script allows you deploy and configure a virtual machine automatically in your VMware environment. 

<img src="img/build.png" width="60%">

**Requirements**

* Have a Windows template ready
* Install [pyVmomi](https://github.com/vmware/pyvmomi) in Jenkins server
* Install [Kerbereos Library](https://docs.ansible.com/ansible/latest/user_guide/windows_winrm.html#installing-the-kerberos-library)
* [Configure Kerberos](https://docs.ansible.com/ansible/latest/user_guide/windows_winrm.html#configuring-host-kerberos)
* Modify Ansible playbooks for your environment

**Jenkins Job Steps**

1. Download job's files from repository
2. Spin up virtual machine and join the VM to the Windows domain
3. Configure Window OS in the VM (expand drives, add users to admin and RDP groups, configure local administrator password)
4. Move VM to proper OU in AD

**Create Jenkins Seed Job**

The [Job DSL](https://plugins.jenkins.io/job-dsl/) plugin allows you to define jobs as code. You will have to install this plugin and then configure the seed job.

Install Job DSL plugin
<img src="img/dsl-job-1.png" width="80%">

Create Seed Job

If you already have a seed job you just need to add the code in the file [seedjob](seedjob) to your existing job if not you can create a new DSK job.

<img src="img/dsl-job-01.png" width="80%">

<img src="img/dsl-job-2.png" width="40%">

Speficy the repository URL where the DLS job will be

<img src="img/dsl-job-3.png" width="100%">

Specify the name of the seed job

<img src="img/dsl-job-4.png" width="100%">

You also need to disable the option shown below 

<img src="img/dsl-job-5.png" width="60%">

**Modify Ansible Playbooks**

**Configure Kerberos**
