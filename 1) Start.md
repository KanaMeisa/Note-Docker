# Docker S

## Hello world

Docker allow you to run applications in containers, here is a example to print "Hello World!".

```shell
$ sudo docker ubuntu:15.10 /bin/echo "Hello, world!"
```

Parameters:

- docker run -- Run a container
- ubuntu:15.10 -- Specifies the image to run, Docker will first search the image in the local host. If it doesn't exist, Docker will download the public image from the Docker Hub repository.
- /bin/echo "Hello, world!" -- The command to run.



The complete meaning of the given command can be explained as follows: Docker creates a new container using the ubuntu:15.10 image, and then executes the command /bin/echo "Hello world" inside the container, resulting in the output of "Hello world". 

---





## Running an interactive container

We use two parameters of Docker, -i and -t, to enable the "conversation" capability of the container:

```bash
kana@arch:~$ docker run -i -t ubuntu:15.10 /bin/bash 
root@0123ce188bd8:/#
```



Parameter explanations:

- -t: Allocates a pseudo-tty or terminal in the new container. 
- -i: Allows interaction with the standard input (STDIN) of the container.

Note the second line, root@0123ce188bd8:/#. We have entered a container with an Ubuntu 15.10 system.



We attempt to run the commands cat /proc/version and ls to view the version information of the current system and the file list in the current directory within the container, respectively.

```
root@0123ce188bd8:/# cat /proc/version 
Linux version 4.4.0-151-generic (buildd@lgw01-amd64-043) (gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.10) )  #178-Ubuntu SMP Tue Jun 11 08:30:22 UTC 2019 

root@0123ce188bd8:/# ls 
bin boot dev etc home lib lib64 media mnt opt proc root run sbin srv sys tmp usr var 

root@0123ce188bd8:/#
```



We can exit the container by running the "exit" command or using CTRL+D.

---





## Start container (background mode)

Use the following command to create a container that runs as a process.

```shell
kana@arch:~$ docker run -d ubuntu:15.10 /bin/sh -c "while true; do echo hello world; sleep 1; done"
b42a1c25658db78d4376337e4b5c0bb53b18e17f7ecd6e0c7212bcef16b64599
```

In the output, we don't see the expected "hello world", but a string of long characters.

``b42a1c25658db78d4376337e4b5c0bb53b18e17f7ecd6e0c7212bcef16b64599``

This long string is called the container ID, which is unique to each container, and we can see what happened to the corresponding container by the container ID.



First, we need to make sure that the container is running, which can be viewed through ``docker ps``:

```shell
kana@arch:~$ docker ps
CONTAINER ID        IMAGE                  COMMAND              	 ...  
b42a1c25658d        ubuntu:15.10           "/bin/sh -c 'while t…"    ...
```

Output details:

- CONTAINER ID**: THE CONTAINER ID**.

- **IMAGE:** The image used.

- **COMMAND:** The command that runs when the container is started.

- CREATED: THE TIME THE CONTAINER WAS **CREATED**.

- **STATUS:** The status of the container.

> There are 7 states:
> - Created
> - Restarting:
> - running or up
> - Removing (on migration)
> - Paused
> - Exited
> - Dead

- **PORTS:** The port information of the container and the type of connection used (tcp\udp).

- **NAMES:** THE NAME OF THE AUTOMATICALLY ASSIGNED CONTAINER.

Use the ``docker logs`` command inside the host host to view the standard output inside the container:

```shell
$ docker logs b42a1c25658d
```

```shell
> docker logs b42a1c25658d
hello world
hello world
hello world
hello world
hello world
```



```shell
$ docker logs stupefied_blackwell
```

```shell
> docker logs stupefied_blackwell
hello world
hello world
hello world
hello world
hello world
hello world
```




------




## Stop vessel

We use the **docker stop** command to stop the container.

Looking through **docker ps**, the container has stopped working:

```shell
$ docker ps
```

You can see that the container is no longer there.

You can also stop it with the following command:

```shell
$ docker stop stupefied_blackwell
```

