# Hachiko Manuals
Manuals for DXG-1 servers Hachiko 1, 2 in Skoltech.

## How get access
1. You have to be a MSc student, PhD student or employee at Skoltech.
2. Ask your supervisor/manager for access.
3. Redirect to [@ChuPIka][1], [@rerayne][2], or [@maremun][3] a granted permission to make you an account.
4. E-mail [helpdesk@skoltech.ru][4] and request Skoltech VPN and usage instructions.
5. Read very thoroughly this manual before you start.
6. In any urgent or uncertain situation contact Emergency contacts ASAP.

## Main rules

1. DXG-1 uses `docker`. That's why, please read a starting manual about this system. <add link>
2. Don't keep a lot of docker images running. Running a container takes a lot of HDD.
3. Each user creates a docker for their needs. Docker's name **HAS TO** contain the user's surname according to template `<username>-mysmallcontainer`.
Failure to satisfy this rule could result in a termination of the container.
4. Don't hold resources that you don't need right now. If you work in Jupyter notebook release all cards you hold through kernel termination. A looped process could be terminated without saving the sate and data.
5. Limit your resources using special keys when you start your docker container (see [tutorial][5] for details).
6. When you're starting your docker you can mount any local directory by adding `-v <local_dir>:<docker_dir>` to the starting command. Directory should be specified as an absolute paths starting with `/` (forward slash).
7. NEVER attach the root directory to your docker. It could result in a total crash of the system. Just never do it. If you want to delete any folder but can't just contact [Emergency contacts](#Emergency_contacts).
8. All datasets have to be stored in a corresponding RAID directory: `/raid/data/datasets`.
9. Save as little data in your home directory as you can. The rest has to be stored in `/raid/data/<username>` directory. Failure to satisfy this rule could result in a termination of the container.
10. It's a good idea to get familiar with `tmux` or `screen` apps for remote sessions.
11. To check the amount of available GPUs and CPUs use `watch nvidia-smi` and `htop` correspondingly.
12. In case of extreme necessity you can add `--net=host` to starting command in order to map identically ports from your docker to its host.

## Manuals
* [General Info](manuals/general_info.md)
* [Establish SSH connection](manuals/connect_ssh.md)
* [VPN for Linux](manuals/vpn_under_linux.md)
* [Visual Studio Code to work inside remote docker container](manuals/vs_remote.md)
* [CUDA Profiler](manuals/cuda_profiler.md)
* [TL;DR Docker + Jupyter (for Dummies)](manuals/docker_jupyter.md)
* [Fix long lines printing bug](manuals/long_lines.md)
* [Datasets](manuals/datasets.md)
* [endpoint with name `container_name`already exists in network bridge](manuals/endpoint_name.md)
* [Pull docker if `docker pull` doesn't work](manuals/pull_docker.md)
* [hachikō: How to modify docker](manuals/modify_docker.md)
* [Resource Limiting](manuals/resource_limiting.md)
* [Forwarding ports from docker container](manuals/port_forwarding.md)
* [Instructions for a persistent docker container](manuals/persistant_container.md)
* [Update Root CAs](manuals/update-trusted-ca.md)

## Emergency contacts <span id="Emergency_contacts"><span>

* @rerayne
    * E-mail: rerayne@gmail.com
    * Telegram: [@rerayne][2]

[1]: https://t.me/ChuPika
[2]: https://t.me/rerayne
[3]: https://t.me/maremun
[4]: mailto:helpdesk@skoltech.ru
[5]: ./manuals/resource_limiting.md
