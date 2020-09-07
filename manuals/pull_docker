# Pull docker if `docker pull` doesn't work

* Some DGX-1's are not connected to the internet for security reasons, making access to NVIDIA registry impossible.
 
Follow instructions to pull and save an image from a PC(=enable internet access machine), and load the saved image on the air-gapped DGX-1.
 
Before pulling an image from DGX registry, we must install Docker on the connected machine.

1. Log on to https://compute.nvidia.com , select your image, then copy the pull command. 
2. From the command prompt, paste the pull command to pull the image to this machine 
3. Check for images pulled
    ```bash
    docker images
    ```
4. Save the image to C:\docker_images\xxxx-5.1.tar 
    ```bash
    Docker save -o ./xxx.tar nvcr.io/nvidia/framewark
    ```
5. Zip the .tar file to .bz2 to reduce size. Sneakerware your file to the DGX-1.
6. To launch the container on DGX-1
    ```bash
        docker load --input framework(.bz2 file)
    ```