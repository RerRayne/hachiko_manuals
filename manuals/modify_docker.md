# hachikō: How to modify docker

Нашел способ, как открыть и jupyter и tensorboard с существующим контейнером и примонтировать raid

1. Получить номер процесса:
    ```bash
    docker ps  -a
    ```

2. Закомиттить докер, имя произвольное:
    ```bash
    docker commit 7db334108b24 kek
    ```

4. Добавить побольше портов и примонтировать raid. Имя тут то, куда коммитили:
    ```bash
    docker run -t -p 9496-9500:9496-9500 --name=kekus -v /home/eponomarev/kek:/workspace -v /mnt/local/data/eponomarev/:/mnt kek
    ```

5. Добавить эти порты в .ssh/config у себя (похоже только копипастой):
    ```bash
    LocalForward 9496 localhost:9496
    LocalForward 9497 localhost:9497
    LocalForward 9498 localhost:9498
    LocalForward 9499 localhost:9499
    LocalForward 9500 localhost:9500
    ```
    
6. Запускать как обычно:
    ```bash
    docker exec -ti kekus bash
   ```
   
   Хорошей идеей так же будет добавить `--shm-size 8G` к команде.
