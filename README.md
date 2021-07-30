# learn_ansible_202107

## setting

change hosts(inventry file)

## check syntax
```
ansible-playbook -i hosts --syntax-check playbook/loopMkdir.yml 

playbook: playbook/loopMkdir.yml
```


## exe ansible-play book
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
 

