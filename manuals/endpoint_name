# endpoint with name `container_name`already exists in network bridge

If you encounter this:
```bash
docker: Error response from daemon: endpoint with name container_name already exists in network bridge
```
try this after stopping and removing the container with `container_name`:
```bash
docker network disconnect -f bridge container_name
```
