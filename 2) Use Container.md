# Use Container

## Get the image

If you don't have an Ubuntu image locally, Docker will pull the Ubuntu images.

```shell
$ docker pull ubuntu
```

```
> docker pull ubuntu                                                                       
Using default tag: latest
latest: Pulling from library/ubuntu
dbf6a9befcde: Pull complete
Digest: sha256:dfd64a3b4296d8c9b62aa3309984f8620b98d87e47492599ee20739e8eb54fbf
Status: Downloaded newer image for ubuntu:latest
```



---



## Start the container

```shell
$ docker run -it ubuntu /bin/bash	
```

Output: 

```shell
> docker run -it ubuntu /bin/bash                                                         
root@82c2c25a9180:/#
```



Parameters description:

- ``-i`` : interactive operation
- ``-t`` : terminal
- ``Ubuntu`` : Ubuntu images
- ``/bin/bash`` : Put after the image name is the command, here we want to have an interactive shell, so we can use  ``/bin/bash``.

To exit the terminal, enter ``exit`` or push ``Ctrl + D``.

---





## Start a container that has stopped running

The command to view all containers is as follows:

```shell
$ docker ps -a	
```

```shell
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS              PORTS     NAMES
1ebfe3cefc57   ubuntu:15.10   "/bin/echo 'Hello wo…"   About an hour ago    Exited (0) About an hour ago             eloquent_cori
```

Start a stopped container:

```
$ docker start 1ebfe3cefc57
```

---





### Runs in the background

In most cases, we want Docker's service to run in the background, and we can specify the runtime mode of the container with **-d**.

```shell
$ docker run -itd --name ubuntu-test ubuntu /bin/bash
```

Output: 

```shell
faf78f8fa82b414bc7547fb2e8a333ef9921812e9b6c0a7a73c07cb334e85ed9
```



**Note:** Adding the **-d** parameter will **not enter** the container by default, and you need to use the command **docker exec** (described below) to enter the container.

---





### Stop a container

The command to stop a container is as follows:

```shell
$ docker stop <Container ID>
```

Stopped containers can be restarted via docker restart:

```shell
$ docker restart <Container ID>
```

---





## Enter the container

When the ``-d``  is used, the container goes into the background after it starts. At this time, if you want to enter the container, you can enter it through the following command:

```shell
$ docker attach faf78f8fa82b
```

Output: 

```shell
root@faf78f8fa82b:/#
```



> Note: Exiting from this container will cause the container to stop.



**Exec command** 

The following demonstrates the use of the docker exec command.

```shell
$ docker exec -it faf78f8fa82b /bin/bash
```

Output: 

```shell
root@faf78f8fa82b:/#
```



> If you exit from this container, the container will not stop, which is why it is recommanded to use ``docker exec``.
>
> For more parameter descriptions, use ``docker exec --help`` command to get help.

---





## Export and import containers

**Export the container**

If you want to export a container locally, you can use the following command.

```shell
$ docker export faf78f8fa82b > ubuntu.rar
```

It will export the container ``faf78f8fa82b`` snapshot to the local file ``ubuntu.rar``.



**Import a container snapshot**

You can use ``docker import`` to import from a container snapshot file and then to an image, and the following example imports the snapshot file ``ubuntu.rar`` to the image ``test/ubuntu:v1``.

```shell
cat docker/ubuntu.rar | docker import - test/ubuntu:v1
```

Output: 

```shell

```

| 季度 | 销售量 |
| ---- | ------ |
| 1    | 100    |
| 2    | 150    |
| 3    | 200    |
| 4    | 250    |
| 5    | 300    |
| 6    | 350    |
