# Ansible Basic commands :

ansible utilitys:
    1 . To check memory space :
    ```yaml
                    [webserver]    [python module]
        - ansible ServerName/Group -m command -a "free -m" -s
                                              [arguments]   [root privilege]
    ```
        > ansible web -m command -a "free -m" -s 

    2. To copy perticular file 
        - ansible webNode1 -m copy -a " src=/  dest=/ "

        > ansible webNode1 -m copy -a "src=./file1 dest=/etc/ansible/"

    3. To install perticular package 
        - ansible webNode1 -m yum -a " name=httpd state=present " -s 

PLAYBOOK commands
=========================================================
# ansible-playbook playbookName
# it is use for to change only those server 
- ansible-playbook playbookName.yml -i /etc/ansible/playbookName.retry

# to see how many host effected 
    - ansible-playbook playbookName.yml --list-host 

# to see check syntex 
    - ansible-playbook playbookName.yml --syntex-check 


# to check how many tasks is to executed 
    - ansible-playbook playbookName.yml --list-tasks


# to control execution flow 
    - ansible-playbook playbookName.yml --step 
        > it ask YES or NOT or CONTINUE

===============================================================================
    - ansible_connection # connection type to th target host 
    - ansible_user       # the username to use when connection to the target
    - ansible_ssh_pass   # the password to use to authentication the username
    - ansible_port       # the connection port numbers
===============================================================================

Facts 
-------------------------==============---------------------------
### Setup module 
    - ansible_host module 
    - ansible_all_ipv4_addresses module
    - 
    setup 
    - ansible all -m setup -a "filter=ansible_os_family"
    - ansible all -m setup
    - ansible web -m setup 




# Conditionals statements 

WHEN clause 


# Loops in yaml

1. Loop
2. with_lookup
 - name: Creating multiple user using with_lookup loop
      user: name={{ item }} state=present
      with_items:
        - Aditya
        - Manish
        - Aryan
        - Sunny
        - Ruturaj

syntex : 
    {{ item }}
    
    with_items:
    - list
    - test




# Variables 

1. Internal 
2. External
3. Command line 
4. Predefine (Inventory Variables)

1. Internal:
    - vars:
        pkg_name=httpd
        user_Name= 'Aditya'


2. External:
    make onther external file 
        + demo.yaml
            > pkg_name= httpd
              user_name= test

3. CommandLine:
    Taking at runtime
        - ansible-playbook playbookName.yml -e "varName=value" 
                                               "user=ansuser"
        
        # another way to do that using passing a json file 
        
        - ansible-playbook playbookName -e @VariablesPass.json 

4. Predefine Varialble 
    Inventory file variable :   
            - ansible_host, ansible_hostname, etc.

To take the value of variable use {{ }} this.


# Tags:

    Tags basically give us the freedom to choice which process executed using tags.

    1. package
    2. always


    - ansible-playbook tags.yml -t package
    or
    - ansible-playbook tags.yml --tags package

        To executed the perticular process who having package tags

    To skip that we can use --skip-tags 

    - ansible-playbook tags.yml --skip-tags package

    To list all the tags to display in perticular playbook 

    the ALWAYS tag execute every time 


    To execute from perticular place 
        - 
            - ansible-playbook tags.yml --start-at-task 'name of the task' 
                                                        'Copy config file'


    
