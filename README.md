example execution command.

requires the building docker containers using [linuxsimba scale testing repo]('https://github.com/linuxsimba/ansible-scale-testing')

Example execution command

```
ansible-playbook multi-role-playbook/vm-deployment-with-apps.yml -t "vm-setup,pre-vm-setup,vm-status,apps" -u root --private-key=ansible_test -e @input.yml
```

And if you want to keep the roles somewhere else then run ansible-galaxy against the requirements.yml
