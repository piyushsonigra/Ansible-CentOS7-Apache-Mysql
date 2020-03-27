# Ansible-CentOS7-Apache-Mysql


This ansible playbook is useful to install Apache web server and Mysql databse in CentOS 7.

## Requirements

You should have below tool installed in your system.

  - Ansible ( Version >=2.4.2 )
  - SSH

## Configuration

Your system should have SSH access of target host. Confirm the target host SSH port and it's accessible through your system.
There is `hosts` file in repository. It contains all informations of the host or group of hosts to connect.

You need to modify `hosts` file as per requirements. More information is available [here](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)

    # Single host using IP or and Domain name
    1.1.1.1
    srv.example.com

    # For group of hosts
    [group_name]
    alpha.example.org
    beta.example.org
    1.1.1.1

    # For different ssh key and port
    webserver  ansible_host=1.1.1.1   ansible_user=ansible   ansible_ssh_private_key_file=~/.ssh/srv.pem   ansible_port=2222


After completion of above configuration you need to add Target Host or Groupname into `playbook.yml` file as shown below.


    - hosts: webserver   #Hostname or Group of Hosts
      become: yes
      tasks:

      ......  


## Usage

Once you finish the playbook configuration. You need to run below command to run or execute ansible playbook or tasks into Target hosts.

    $ ansible-playbook -i hosts playbook.yml


## Output

Below is the sample output of above ansible-playbook command. Once it done you should be able to access Apache default page on `http://host_ip:8080`.


    PLAY [web-db] *********************************************************************************************************************************************

    TASK [Gathering Facts] ************************************************************************************************************************************
    ok: [web-db]

    TASK [Setup repo for Mysql 5.7] ***************************************************************************************************************************
    ok: [web-db]


    TASK [Install Packages] ***********************************************************************************************************************************
    ok: [web-db]

    TASK [Start Apache] ***************************************************************************************************************************************
    ok: [web-db]

    TASK [Start Mysql] ****************************************************************************************************************************************
    ok: [web-db]

    TASK [Start Firewalld] ************************************************************************************************************************************
    ok: [web-db]

    TASK [Apache to listen on 8080] ***************************************************************************************************************************
    ok: [web-db]

    TASK [Allow 8080 port] ************************************************************************************************************************************
    ok: [web-db]

    TASK [Disable SELinux] ************************************************************************************************************************************
    [WARNING]: SELinux state change will take effect next reboot
    ok: [web-db]

    PLAY RECAP ************************************************************************************************************************************************
    web-db                     : ok=9    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
