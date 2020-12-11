---
title: "Orientation and setup"
keywords: get started, setup, orientation, quickstart, intro, concepts, containers, docker desktop
description: Get oriented on some basics of Docker and install Docker Desktop.
redirect_from:
- /engine/getstarted-voting-app/
- /engine/getstarted-voting-app/cleanup/
- /engine/getstarted-voting-app/create-swarm/
- /engine/getstarted-voting-app/customize-app/
- /engine/getstarted-voting-app/deploy-app/
- /engine/getstarted-voting-app/node-setup/
- /engine/getstarted-voting-app/test-drive/
- /engine/getstarted/
- /engine/getstarted/last_page/
- /engine/getstarted/step_five/
- /engine/getstarted/step_four/
- /engine/getstarted/step_one/
- /engine/getstarted/step_six/
- /engine/getstarted/step_three/
- /engine/getstarted/step_two/
- /engine/tutorials/dockerimages/
- /engine/tutorials/dockerizing/
- /engine/tutorials/usingdocker/
- /engine/userguide/containers/dockerimages/
- /engine/userguide/dockerimages/
- /engine/userguide/intro/
- /get-started/part1/
- /get-started/part6/
- /getstarted/
- /getting-started/
- /learn/
- /linux/last_page/
- /linux/started/
- /linux/step_four/
- /linux/step_one/
- /linux/step_six/
- /linux/step_three/
- /linux/step_two/
- /mac/last_page/
- /mac/started/
- /mac/step_four/
- /mac/step_one/
- /mac/step_six/
- /mac/step_three/
- /mac/step_two/
- /userguide/dockerimages/
- /userguide/dockerrepos/
- /windows/last_page/
- /windows/started/
- /windows/step_four/
- /windows/step_one/
- /windows/step_six/
- /windows/step_three/
- /windows/step_two/
---

{% include_relative nav.html selected="1" %}

Welcome! We are excited that you want to learn Docker.

This page contains step-by-step instructions on how to get started with Docker. We also recommend the video walkthrough from Dockercon 2020.

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/iqqDU2crIEQ?start=30" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The Docker Quickstart training module teaches you how to:

1.  Set up your Docker environment (on this page)

2.  [Build and run your image](part2.md)

3.  [Share images on Docker Hub](part3.md)

## Docker concepts

Docker is a platform for developers and sysadmins to **build, run, and share**
applications with containers. The use of containers to deploy applications
is called _containerization_. Containers are not new, but their use for easily
deploying applications is.

Containerization is increasingly popular because containers are:

- **Flexible**: Even the most complex applications can be containerized.
- **Lightweight**: Containers leverage and <span class='important'>share the host kernel</span>,
  making them much more efficient in terms of system resources than virtual machines.
- **Portable**: You can build locally, deploy to the cloud, and run anywhere.
- **Loosely coupled**: Containers are highly <span class='important'>self sufficient and encapsulated</span>,
  allowing you to replace or upgrade one without disrupting others.
- **Scalable**: You can <span class='important'>increase and automatically distribute container replicas</span> across a datacenter.
- **Secure**: Containers apply <span class='important'>aggressive constraints and isolations</span> to processes without any configuration required on the part of the user.

### Images and containers

Fundamentally, a container is <span class='important'>nothing but a running process</span>,
with some <span class='important'>added encapsulation features</span> applied to it in order to keep it isolated from the host and from other containers.
One of the most important aspects of container isolation is that each container interacts with its <span class='definition'>own private filesystem</span>; this filesystem is provided by a Docker **image**.
An <span class='definition'>image</span> includes everything needed to run an application - <span class='important'>the code or binary,
runtimes, dependencies, and any other filesystem objects required</span>.

### Containers and virtual machines

A container runs _natively_ on Linux and <span class='important'>shares the kernel of the host
machine with other containers</span>. It runs a <span class='important'>discrete process</span>, taking no more memory
than any other executable, making it lightweight.

By contrast, a <span class='definition'>**virtual machine** (VM)</span> runs a <span class='important'>full-blown "guest" operating</span>
system with _virtual_ access to host resources through a <span class='definition'>hypervisor</span>. In general,
VMs incur a lot of overhead beyond what is being consumed by your application logic.

![Container stack example](/images/Container%402x.png){:width="300px"} | ![Virtual machine stack example](/images/VM%402x.png){:width="300px"}

## Set up your Docker environment

### Download and install Docker Desktop

Docker Desktop is an easy-to-install application for your Mac or Windows environment that enables you to start coding and containerizing in minutes. Docker Desktop includes everything you need to build, run, and share containerized applications right from your machine.

Follow the instructions appropriate for your operating system to download and install Docker Desktop.

 [Docker Desktop for Mac](/docker-for-mac/install/){: target="_blank" rel="noopener" class="_"}{: .button .outline-btn} [Docker Desktop for Windows](/docker-for-windows/install/){: target="_blank" rel="noopener" class="_"}{: .button .outline-btn}

### Test Docker version

After you've successfully installed Docker Desktop, open a terminal and run `docker --version` to check the version of Docker installed on your machine.

```shell
$ docker --version
Docker version 19.03.13, build 4484c46d9d
```

### Test Docker installation

1.  Test that your installation works by running the [hello-world](https://hub.docker.com/_/hello-world/){: target="_blank" rel="noopener" class="_"} Docker image:

    ```shell
        $ docker run hello-world

        Unable to find image 'hello-world:latest' locally
        latest: Pulling from library/hello-world
        ca4f61b1923c: Pull complete
        Digest: sha256:ca0eeb6fb05351dfc8759c20733c91def84cb8007aa89a5bf606bc8b315b9fc7
        Status: Downloaded newer image for hello-world:latest

        Hello from Docker!
        This message shows that your installation appears to be working correctly.
        ...
    ```

2.  Run `docker image ls` to <span class='definition'>list</span> the `hello-world` image that you downloaded to your machine.

3.  <span class='definition'>List the `hello-world` container</span> (spawned by the image) which exits after displaying its message. If it is still running, you do not need the `--all` option:

    ```shell
        $ docker ps --all

        CONTAINER ID     IMAGE           COMMAND      CREATED            STATUS
        54f4984ed6a8     hello-world     "/hello"     20 seconds ago     Exited (0) 19 seconds ago
    ```

## Conclusion

At this point, you've installed Docker Desktop on your development machine, and ran a quick test to ensure you are set up to build and run your first containerized application.

[On to Part 2 >>](part2.md){: class="button outline-btn" style="margin-bottom: 30px; margin-right: 100%"}

For information on how to build and run your first containerized application using Node.js, go to [Build your Node.js image](/nodejs/build-images.md).

## CLI references

Refer to the following topics for further documentation on all CLI commands used in this article:

- [docker version](https://docs.docker.com/engine/reference/commandline/version/)
- [docker run](https://docs.docker.com/engine/reference/commandline/run/)
- [docker image](https://docs.docker.com/engine/reference/commandline/image/)
- [docker container](https://docs.docker.com/engine/reference/commandline/container/)
