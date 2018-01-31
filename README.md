Demo showing some vm provisioning methods using Ansible

```
ansible-playbook multi-role-playbook/vm-deployment-with-apps.yml  -e @input.yml
```

Example output:

```
TASK [pre-vm-setup : transform user_entry info with extra bits] ***************************************************************************************************************************************************
ok: [localhost]

TASK [vm-setup : debug] *******************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "create VM"
}

TASK [vm-setup : debug] *******************************************************************************************************************************************************************************************
ok: [localhost] => (item={'ansible_port': 9003, 'hostname': u'ts003', 'app_list': u"[u'app1', u'app2', u'app3']", 'ansible_host': u'localhost', 'groups': u'deploy_vms'}) => {
    "changed": false,
    "item": {
        "ansible_host": "localhost",
        "ansible_port": 9003,
        "app_list": "[u'app1', u'app2', u'app3']",
        "groups": "deploy_vms",
        "hostname": "ts003"
    },
    "msg": "attributes used {'ansible_port': 9003, 'hostname': u'ts003', 'app_list': u\"[u'app1', u'app2', u'app3']\", 'ansible_host': u'localhost', 'groups': u'deploy_vms'}"
}
ok: [localhost] => (item={'ansible_port': 9002, 'hostname': u'ts002', 'app_list': [u'app1'], 'ansible_host': u'localhost', 'groups': u'deploy_vms'}) => {
    "changed": false,
    "item": {
        "ansible_host": "localhost",
        "ansible_port": 9002,
        "app_list": [
            "app1"
        ],
        "groups": "deploy_vms",
        "hostname": "ts002"
    },
    "msg": "attributes used {'ansible_port': 9002, 'hostname': u'ts002', 'app_list': [u'app1'], 'ansible_host': u'localhost', 'groups': u'deploy_vms'}"
}

TASK [vm-setup : Add hosts to the inventory creating the VMs] *****************************************************************************************************************************************************
[DEPRECATION WARNING]: Using variables for task params is unsafe, especially if the variables come from an external source like facts. This feature will be removed in version 2.6. Deprecation warnings can be
disabled by setting deprecation_warnings=False in ansible.cfg.
changed: [localhost] => (item={'ansible_port': 9003, 'hostname': u'ts003', 'app_list': u"[u'app1', u'app2', u'app3']", 'ansible_host': u'localhost', 'groups': u'deploy_vms'})
changed: [localhost] => (item={'ansible_port': 9002, 'hostname': u'ts002', 'app_list': [u'app1'], 'ansible_host': u'localhost', 'groups': u'deploy_vms'})

PLAY [deploy_vms] *************************************************************************************************************************************************************************************************

TASK [Gathering Facts] ********************************************************************************************************************************************************************************************
ok: [ts003]
ok: [ts002]

TASK [vm-status : debug] ******************************************************************************************************************************************************************************************
ok: [ts003] => {
    "msg": "Checking VM status"
}
ok: [ts002] => {
    "msg": "Checking VM status"
}

TASK [app1 : debug] ***********************************************************************************************************************************************************************************************
ok: [ts003] => {
    "msg": "Deploying App 1"
}
ok: [ts002] => {
    "msg": "Deploying App 1"
}

TASK [app2 : debug] ***********************************************************************************************************************************************************************************************
skipping: [ts002]
ok: [ts003] => {
    "msg": "Deploying App2"
}

TASK [app3 : debug] ***********************************************************************************************************************************************************************************************
skipping: [ts002]
ok: [ts003] => {
    "msg": "Deploying App3"
}

PLAY RECAP ********************************************************************************************************************************************************************************************************
localhost                  : ok=4    changed=1    unreachable=0    failed=0
ts002                      : ok=3    changed=0    unreachable=0    failed=0
ts003                      : ok=5    changed=0    unreachable=0    failed=0
```
