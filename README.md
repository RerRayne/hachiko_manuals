# Hachiko Manuals
Manuals for DXG-1 servers Hachiko 1, 2 in Skoltech.

## How get access
1. You have to be a Ph.D. student or employee at Skoltech.
2. Ask your supervisor/manager for access.
3. Redirect to @rerayne a granted permission she'll make you an account.
4. E-mail helpdesk@skoltech.ru and request Skoltech VPN and usage instructions.
5. Read very thoroughly this manual before you start.
6. In any urgent or uncertain situation contact Emergency contacts ASAP.

## Main rules
 1. DXG-1 uses nvidia-docker. That's why, please read a starting manual about this system. <add link>
 2. Always use  nvidia-docker instead just docker if you want to use GPUs
 3. Don't keep a lot of docker images running. Running a container takes a lot of HDD.
 4. Each user creates a docker for their needs. Docker's name **HAS TO** contain the user's surname. Failure to satisfy this rule could result in a termination of the container.
 5. Don't hold resources that you don't need right now. If you work in iPython notebook release all cards you hold through kernel termination. A looped process could be terminated without saving the sate and data
 6. Limit your resources using special keys when you start your docker container. [Tutorial](manuals/resource_limiting.md)
 7. When you're starting your docker you can mount any local directory by adding ```-v <local_dir>:<docker_dir>``` to the starting command.
 8. NEVER attach the root directory to your docker. It could result in a total crash of the system. Just never do it. If you want to delete any folder but can't just contact [Emergency contacts](#Emergency_contacts).
 9. All datasets have to be stored in a corresponding RAID directory: ```/raid/data/datasets```.
 10. Save as little data in your home directory as you can. The rest has to be stored in ```/raid/data/%username%``` directory.
 11. It's a good idea to get familiar with tmux or screen apps for remote sessions.
 12. To check the amount of available GPUs and CPUs use ```watch nvidia-smi``` and ```htop``` correspondingly.
 13. To map identically ports from your docker to its host you can add --net="host" to starting command. For example:
 ```bash
     nvidia-docker run --name tensor_compression -it -v /home/lmarkeeva/workspace/nntc:/workspace/nntc -v /raid:/workspace/raid --net="host" tc:1.0.1
 ```
 
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
    * Telegram: @rerayne
    
 
