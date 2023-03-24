# General Info


DGX-1 stations
* Hachikō1 ip: 10.30.16.130
* Hachikō2 ip: 10.30.16.131

OS
* Ubuntu 16.04

Python distributions:
* python2.7
* python3.5
* python3.6

Shared conda

Miniconda3 (/opt/miniconda3/, remember to create your own environments!)

To use conda prepend: 
```bash
export PATH="/opt/miniconda3/bin:$PATH"
```
to your `.bashrc`

# Tensorflow
To use tensorflow, you have to use `docker`:
```bash
docker run -it --rm -v /home/username/proj1:/workspace nvcr.io/nvidia/tensorflow:18.04-py3
```


Where:
* `-it` means run in interactive mode
* `-rm` will delete the container when finished
* `-v` is the mounting directory
* `local_dir` is the directory or file from your host system (absolute path) that you want to access from inside your container. For example, the *local_dir* in the following path is ` /home/username/proj1`.
`-v  /home/username/proj1:/workspace`

If you are inside the container, for example, `ls /workspace`, you will see the same files as if you issued the `ls  /home/username/proj1` command from outside the container.
* *container_dir* is the target directory when you are inside your container. For example, `/workspace` is the target directory in the example:
` -v  /home/username/proj1:/workspace`
 
To use python3 in container specify it in the command:
`python3 script.py`

For details about docker read the post [here](https://github.com/nvidia/nvidia-container-runtime).