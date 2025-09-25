# SSH

## How to

### Put SSH in verbose mode

#### For git

```
GIT_SSH_COMMAND="ssh -vvv" git clone ...
```

#### For Ansible

```
ansible-playbook --ssh-common-args -vvv ...
```

#### General

```
ssh -vvv
```

#### Exit a blocked ssh session

```
~.
```
