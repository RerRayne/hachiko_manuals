# Establish SSH connection

## Preparation

Let `%username%` be your account name.

1. `mkdir -p ~/.ssh/control-master`
2. `vim  ~/.ssh/config`
3. Add the following lines:
   ```
   Host hachiko1 hachiko2
       ControlPath ~/.ssh/control-master/%C
       ControlMaster auto
       ControlPersist 10m
       User %username%

   Host hachiko1
       HostName 10.30.16.130

   Host hachiko2
       HostName 10.30.16.131
   ```

## Connection

**NOTE** MSc students are granted acess only to `hachiko2`.

1. Establish Skoltech VPN connection (if you're in Skoltech right now, skip this step).
2. Run `ssh  hachiko1` or `ssh  hachiko2`.

If you want to map some port from a remote machine:
```bash
ssh -L 8888:localhost:8894 hachiko2
```
where `8888` is a local host and `8894` is a remote one. After this line if you
connect to port `8888` on the localhost in fact you connect to `8894` port on
hachiko2.

## Troubleshooting

### What is SSH?

Try this links \[[1][1],[2][2],[3][3]\] or this video \[[4][4]\].

### What password should I type?

There is no password authorization. If you get message like
```shell
$ ssh hachiko1
username@10.30.16.130: Permission denied (publickey).
```
this means means that something wrong with your credentials. Also, ensure that
you are connecting to `hachiko2` if you are MSc student.

### Name or service not found?

This probably means some issues with host resolution and `~/.ssh/config` what
should be clear from the message.
```shell
$ ssh hachiko2
ssh: Could not resolve hostname hachiko2: Name or service not known
```
You always can try to connect via IP. For example, the following command
establish SSH with `hachiko2`.
```shell
$ ssh 10.30.16.131
```

[1]: https://schh.medium.com/ssh-for-dummies-ea168e6ff547
[2]: https://medium.com/pentesternepal/ssh-for-dummies-what-why-how-c3614f5f38c9
[3]: https://levelup.gitconnected.com/a-beginners-guide-to-ssh-fb4edbe91233
[4]: https://www.youtube.com/watch?v=v45p_kJV9i4
