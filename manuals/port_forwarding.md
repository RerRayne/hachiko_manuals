# Forwarding ports from docker container


```bash
docker run -t -p host_port:container_port container_image
```

Inside container run jupyter as follows (don't forget to customize jupyter config! `jupyter notebook --generate-config`, set `c.NotebookApp.open_browser = False`, `c.NotebookApp.port = 8888`) :
```bash
jupyter notebook --ip 0.0.0.0 --allow-root
```
On your host open browser and go to `localhost:host_port`.

Also you can map 1:1 docker's ports to the host's ones by adding ` --net="host"` to `docker run ...`. For example:
 ```bash
     docker run --name tensor_compression -it -v /home/lmarkeeva/workspace/nntc:/workspace/nntc -v /mnt/local:/workspace/mnt/local --net=host tc:1.0.1
 ```
