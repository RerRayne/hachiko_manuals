# Visual Studio Code to work inside remote docker container

While you are tired from developing code in Jupyter notebook in your browser, you can try VS Code to develop exactly inside docker container on Hachiko from a user-friendly interface.

All necessary information are in [Tutorial](https://code.visualstudio.com/docs/remote/containers-advanced#_developing-inside-a-container-on-a-remote-docker-host)

But shortly, you need to:

* Install Docker+Remote Developing pack - see [HOWTO](https://code.visualstudio.com/docs/remote/containers#_installation)

    If you already have docker, VSCode and your ```$USER``` in ```docker``` group (```sudo usermod -aG docker $USER```), just install extension by pressing CTRL+P and passing the following command:
    
    ```bash
    ext install ms-vscode-remote.vscode-remote-extensionpack
    ```
 
* Add remote host in settings:
  1. Press Ctrl+Comma (File->Preferences->Settings):
  2. Find "edit in settings.json" 
  3. Add line (with your data). hachiko1: 10.30.16.130, hachiko2: 10.30.16.131:  
  ``` "docker.host":"ssh://eponomarev@<host_ip>"```
 
* In VS Code Attach to existed docker container:
    1. Connect to container 
    2. Press F1: 
        
        ```Remote-Containers: Attach to Running Container....```