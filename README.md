# learn_ansible_202107
This repository is my study record for ansible.
Mainly udemy(getting started ansible in Japanese) and my test sample playbook.

## setting

change hosts(inventry file)

## check syntax(sample) or dry-run(option --check)
```
ansible-playbook -i hosts --syntax-check playbook/loopMkdir.yml 

playbook: playbook/loopMkdir.yml
```


## exe ansible-play book(sample)
```
ansible-playbook -i hosts playbook/loopMkdir.yml 

PLAY [all] *****************************************************************************************

TASK [Gathering Facts] *****************************************************************************
ok: [10.0.0.51]
ok: [10.0.1.190]

TASK [Loop mkdir] **********************************************************************************
ok: [10.0.1.190] => (item=test1)
ok: [10.0.0.51] => (item=test1)
ok: [10.0.1.190] => (item=test2)
ok: [10.0.0.51] => (item=test2)
ok: [10.0.1.190] => (item=test3)
ok: [10.0.0.51] => (item=test3)

PLAY RECAP *****************************************************************************************
10.0.0.51                  : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
10.0.1.190                 : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

``` 

## offen used command sampl

### check ping
if terget-server didn't  exchange ssh-key and you required password, you have to add opptin -k


```
$ ansible -i hosts my -m ping
10.0.0.51 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    }, 
    "changed": false, 
    "ping": "pong"
}
```

### allow var in ansible
```
$ ansible -i hosts my -m setup
10.0.0.51 | SUCCESS => {
    "ansible_facts": {
        "ansible_all_ipv4_addresses": [
            "10.0.0.51"
        ], 
        "ansible_all_ipv6_addresses": [
            "fe80::434:35ff:fec1:1ad7"
        ], 
        "ansible_apparmor": {
            "status": "disabled"
        }, 
        "ansible_architecture": "x86_64", 
        "ansible_bios_date": "08/24/2006", 
        "ansible_bios_version": "4.11.amazon", 
        "ansible_cmdline": {
            "BOOT_IMAGE": "/boot/vmlinuz-3.10.0-1062.12.1.el7.x86_64", 
            "LANG": "en_US.UTF-8", 
     .....
     
       "ansible_system_capabilities_enforced": "True", 
        "ansible_system_vendor": "Xen", 
        "ansible_uptime_seconds": 13186, 
        "ansible_user_dir": "/home/centos", 
        "ansible_user_gecos": "Cloud User", 
        "ansible_user_gid": 1000, 
        "ansible_user_id": "centos", 
        "ansible_user_shell": "/bin/bash", 
        "ansible_user_uid": 1000, 
        "ansible_userspace_architecture": "x86_64", 
        "ansible_userspace_bits": "64", 
        "ansible_virtualization_role": "guest", 
        "ansible_virtualization_type": "xen", 
        "discovered_interpreter_python": "/usr/bin/python", 
        "gather_subset": [
            "all"
        ], 
        "module_setup": true
    }, 
    "changed": false
}


```

### directly command input
```
ansible -i hosts my -a "ls -l /tmp"
10.0.0.51 | CHANGED | rc=0 >>
合計 92
drwx------. 2 centos centos    41  7月 30 06:17 ansible_command_payload_5oQdpj
drwxrwxr-x. 2 centos centos   228  7月 30 05:00 backup_playbook
-rw-rw-r--. 1 centos centos    43  7月 30 05:50 date.txt
-rw-rw-r--. 1 centos centos   242  7月 30 04:58 ip-10-0-0-51.ap-northeast-1.compute.internal.txt
-rw-rw-r--. 1 centos centos 73219  7月 30 05:43 k10013169271000.html
drwx------. 3 root   root      17  7月 30 01:50 systemd-private-e613c1b0e1b943b6bb4f000e95f49751-chronyd.service-FuHMlY
drwxrwxr-x. 2 centos centos    39  7月 30 05:35 test
-rw-rw-r--. 1 centos centos 10240  7月 25 09:44 test.tar
```

