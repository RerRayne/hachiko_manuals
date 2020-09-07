# Establish SSH connection

## Preparation
1. `vim  ~/.ssh/config`
2. Add the following lines:
```bash
Host hachiko1
HostName 10.30.16.130
User %username%
ControlMaster auto
ControlPath ~/.ssh/control-master/%r@%h:%p

Host hachiko2
HostName 10.30.16.131
User %username%
ControlMaster auto
ControlPath ~/.ssh/control-master/%r@%h:%p
```

where `%username` is your account name.

## Connection

1. Establish Skoltech VPN connection (if you're in Skoltech right now, skip this step)
2. Run `ssh  hachiko1` or `ssh  hachiko2`

If you want to map some port from a remote machine:
```bash
ssh -L 8888:localhost:8894 hachiko2         
``` 

where `8888` is a local host and `8894` is a remote one. After this line if you connect to port `8888` on the localhost in fact you connect to `8894` port on hachiko2. 