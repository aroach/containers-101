# Containers 101

## Getting Started

In your web browser:

1. Create a <a href="https://hub.docker.com/signup" target="_blank">Docker account</a>
1. Open <a href="https://labs.play-with-docker.com" target="_blank">Play With Docker</a>
1. Login using your Docker account
1. Click on `Start`
1. Now that a new session is running, click on `+ Add New Instance`
1. After a few moments, you'll see a terminal window

## Take a peek!

1. Type `ls -la` at the `$` command prompt

Notice the files and directories that are present...

```
[node1] (local) root@192.168.0.13 ~
$ ls -la
total 20
drwx------    1 root     root            39 Aug 13 23:32 .
drwxr-xr-x    1 root     root            80 Aug 13 23:30 ..
drwx------    3 root     root            17 Jul 31 14:15 .cache
drwxr-xr-x    1 root     root            26 Aug 13 23:31 .docker
-rw-rw-r--    1 root     root            43 Jan 17  2018 .gitconfig
-rw-rw-r--    1 root     root          1865 Jan 17  2018 .inputrc
-rw-rw-r--    1 root     root           185 Jan 17  2018 .profile
drwxr-xr-x    2 root     root            61 Jul 31 14:23 .ssh
-rw-rw-r--    1 root     root            85 Jan 17  2018 .vimrc
```

## Part 1: Create a new "userland"

1. Start by creating a `Dockerfile` that will inheret from an old version of Ubuntu

`echo 'FROM ubuntu:15.04' >> Dockerfile`

2. Build the Docker image 

`docker build .`

3. Let's run the Docker image as a container

`docker run --name ubuntu --rm -i -t ubuntu:15.04 bash`

4. You'll notice that we are at a new command prompt! It should look something like this. What stands out to you as different?

`root@54f7f44ab67b:/#`

5. Type `ls -la` to list all files

```
$ docker run --name ubuntu --rm -i -t ubuntu:15.04 bash
root@54f7f44ab67b:/# ls -la
total 4
drwxr-xr-x   1 root root    6 Aug 13 23:32 .
drwxr-xr-x   1 root root    6 Aug 13 23:32 ..
-rwxr-xr-x   1 root root    0 Aug 13 23:32 .dockerenv
drwxr-xr-x   2 root root 4096 Jan 22  2016 bin
drwxr-xr-x   2 root root    6 Apr 17  2015 boot
drwxr-xr-x   5 root root  360 Aug 13 23:32 dev
drwxr-xr-x   1 root root   66 Aug 13 23:32 etc
drwxr-xr-x   2 root root    6 Apr 17  2015 home
drwxr-xr-x   8 root root  152 Jan 22  2016 lib
drwxr-xr-x   2 root root   34 Jan 22  2016 lib64
drwxr-xr-x   2 root root    6 Jan 22  2016 media
drwxr-xr-x   2 root root    6 Apr 17  2015 mnt
drwxr-xr-x   2 root root    6 Jan 22  2016 opt
dr-xr-xr-x 755 root root    0 Aug 13 23:32 proc
drwx------   2 root root   37 Jan 22  2016 root
drwxr-xr-x   4 root root   45 Jan 22  2016 run
drwxr-xr-x   1 root root   21 Jan 26  2016 sbin
drwxr-xr-x   2 root root    6 Jan 22  2016 srv
drwxrwxrwx  13 root root    0 Jul 14 21:22 sys
drwxrwxrwt   2 root root    6 Jan 22  2016 tmp
drwxr-xr-x   1 root root   18 Jan 26  2016 usr
drwxr-xr-x   1 root root   17 Jan 26  2016 var
```

Notice that you are now in an Ubuntu "userland"!

6. *Type `exit` followed by the Enter key*

## Summary: 'Create a new "userland"' 

* Created a `Dockerfile` that inherits from the Ubuntu 15.04 release
* Ran the Docker image
* Explored the new "userland"


## Part 2: Package an application

1. Create an application directory, and create your application!

`mkdir app && echo 'print("hello containers")' >> app/app.py`

2. Click on the Editor button to enter an interactive text editor session

3. Open the *Dockerfile* in the interactive text editor

4. Replace the contents of the *Dockerfile* with the following content

```
#Dockerfile
FROM python
RUN mkdir /app
COPY ./app/app.py /app
WORKDIR /app
CMD ["python", "app.py"]
```

5. Save the *Dockerfile*

6. It's time to build your container!

`docker build --tag=hello_python:1.0 .` 

(This might take a minute or two to complete.)

7. View the Docker images that we've created

`docker images`

8. Run the Docker container

`docker run -it hello_python:1.0`

You should see text in your terminal that we printed to standard out

`hello containers`

## Summary: 'Package an application'

* Created a small Python application that prints "hello containers"
* Updated the `Dockerfile` to include that application in the built image
* Ran the image as a container
