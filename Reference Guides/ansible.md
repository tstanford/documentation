# Ansible

## Adhoc command to run shell command on remote hosts

    ansible -i inventory/iaasprodzone.ini -u ansible --private-key /etc/wbp/.ansible-key-iaasprodzone all -m shell -a "curl https://slglvms2.internal.standardlife.com:9999" -v

## Run playbook

    ansible-playbook -i inventory/iaasprodzone.ini -u ansible --private-key /etc/wbp/.ansible-key-iaasprodzone myplaybook.yml

## Inventories

### use real hostnames

    [web]
    webserver1
    webserver2

### or ip addresses with alias

    [web]
    server1 ansible_host=10.60.65.134
    server2 ansible_host=10.60.65.135

    [app]
    server3 ansible_host=10.60.65.136
    server4 ansible_host=10.60.65.137

    [mygroup:children]
    web
    app

### get file and save it as hostname.log

    - name: get log file
      fetch:
        src: /var/log/dmesg
        dest: ~/ans1/{{ inventory_hostname }}.log
        flat: yes
