## Edited .py files for Huawei ce_module to work with non CloudEnigne switches
Tested with Huawei S2750 switches and AR161 routers

Working modules:
- ce_config
- ce_command
- ce_facts

Enough to automate configuration of Huawei devices

Replace files in Ansible modules or change like in this repo

        ex. find / -name "ce*.py"

Ansible documentation for CloudEngine modules:

https://docs.ansible.com/ansible/latest/modules/list_of_network_modules.html#cloudengine

#Usage Example

Ex. playbook.yml file:
    
    - name: "Test Huawei playbook"
      hosts: test_hosts
      vars_files: vaulted_connection.yml
      gather_facts: no
      
      tasks:
        - name: "Get facts from device"
          ce_facts:
             gather_subset: all
             
Ex. vaulted_connection.yml file:

    ansible_connection: network_cli
    ansible_network_os: ce
    ansible_user: test_user
    ansible_password: test_password
    ansible_port: 22
    
Ex. ansible.cfg file:

    [defaults]
    inventory = inventory.yml
    timeout = 20 // necessary for Huawei switches
    
    [paramico_connection]
    host_key_auto_add = True //in case of SSH key problem/mismatch
    
Ex. inventory.yml file

    [test_host]
    <IP> or hostname
