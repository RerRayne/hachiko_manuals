# Instructions for a persistent docker container

To create a container that will persist when you detach, type
```bash
nvidia-docker run -t nvcr.io/nvidia/tensorflow:18.06-py3
```
This will create a container with an allocated tty (How to share data with container? Checkout the [first post](https://oseledets.ryver.com/#posts/1591328) in the channel).

When you finished working in the container, e.g. you've run a script that would carry out computations for a while, you would like to detach from the container - type `ctrl + d`.

Now you're outside the container, and you can check if the container is still running (see status column):
```bash
nvidia-docker ps -a
```
The above command will show you the `container_id`, which you will need whenever you feel like returning to the container:
```bash
nvidia-docker exec -ti container_id bash
```

Though docker gives funny names to containers, you *should* use `--name` option to give it a name that easily identifies the owner:
```bash
nvidia-docker run --name=username_tf3 -t nvcr.io/nvidia/tensorflow:18.06-py3
```

Then it's more convenient to return back to it:
```bash
nvidia-docker exec -ti username_tf3 bash
```

Remember that while container has not been removed it will save the changes that you are making in there. Once you decide that the container you used is no longer of any value to you:
```bash
nvidia-docker stop container_id; nvidia-docker rm container_id
```

**NB** Always make sure that there are no unused containers with `nvidia-docker ps -a`.