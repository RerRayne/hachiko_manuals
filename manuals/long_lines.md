# Fix long lines printing bug

Connect to a container using the following cmd:
```bash
nvidia-docker exec -ti --env COLUMNS=tput cols --env LINES=tput lines name bash
```