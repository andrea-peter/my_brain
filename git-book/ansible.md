# Ansible

## How to

### Execute playbook

```
ansible-playbook -i INVENTORY [-i INVENTORY...] PLAYBOOK
```

#### With sudo password

```
--ask-become-pass
```

### Check playbook syntax

```
ansible-playbook --syntax-check PLAYBOOK
```

### Check inventories syntax

```bash
ansible-inventory -i inventories/ --list
```

### Force color output

Set variable `ANSIBLE_FORCE_COLOR=true`

