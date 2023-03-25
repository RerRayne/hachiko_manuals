# TL;DR Docker + Jupyter (for Dummies)
The following command creates a docker container, mounts raid/data folder to your workspace, manages ports and limits CPU load
```bash
docker run --rm -ti --name=YOUR_CONTAINER_NAME -p YOUR_PORT:YOUR_PORT --cpus=8 -v /home/YOUR_USERNAME:/workspace -v /raid/:/workspace/raid YOUR_DOCKER_IMAGE
```

Note:
- YOUR_PORT should be a unique number,
- YOUR_CONTAINER_NAME should identify you (e.g. contain your username),
- the latest docker image can be found in the topics.

Example:
```bash
docker run --rm -ti --name=talgat2 -p 1313:1313 --cpus=8 --ipc=host -v /home/tdaulbaev:/workspace -v /raid/:/workspace/raid nvcr.io/nvidia/pytorch:19.07-py3
```

Detach the process (Ctrl + Q or Ctrl + P) and run the following command that executes your container: 
```bash
docker exec -ti YOUR_CONTAINER_NAME bash
```

Then, you have to make jupyter notebooks work. Run
```bash 
jupyter notebook --generate-config 
```

and then open `/root/.jupyter/jupyter_notebook_config.py` using your favorite text editor. 

You should change the following settings (don't forget to uncomment the corresponding lines):
• `#c.NotebookApp.port = 8888` → `c.NotebookApp.port = YOUR_PORT`
• `#c.NotebookApp.ip = 'localhost'` → `c.NotebookApp.ip = '0.0.0.0'`
• `#c.NotebookApp.open_browser = True` → `c.NotebookApp.open_browser = False`
• `#c.NotebookApp.allow_root = False` → `c.NotebookApp.allow_root = True`

Make sure that in ssh config on a local computer you have the following line:
`LocalForward YOUR_LOCAL_PORT localhost:YOUR_PORT`

Run `jupyter notebook` and open http://localhost:YOUR_LOCAL_PORT in your browser, the token is in the command line. 


Have fun!
