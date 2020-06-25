---
title: "Docker for Beginners"
date: 2020-06-25T08:54:20-07:00
draft: true
toc: true
---

## Introduction

So, I've heard of Docker a lot, and while I understand what it does, I never really got the point of it. With DevOS being the hot new trend, I decided to take an online course for absolute beginners on Docker to finally get to the bottom of this. If you'd like to take the course yourself, you can find it for free on YouTube [here](https://youtu.be/fqMOX6JJhGo). As anything new that I learn, I like to take notes, a lot of notes. The rest of this post are those notes, effectively summarizing the 2 hour course into a short read. 



## Why use Docker at all?

Docker solves the age-old compatibility problem from using different technologies each with different libraries and dependencies all sharing the same Operating System and underlying hardware resources. 

The simplest example of this would be having two Python apps using different versions of Python each with different associated libraries and dependencies. If you're familiar with Python, virtual environments probably come up to mind as a solution to this problem. Docker is basically the same concept but for more than just Python programs.

Take for example, a developer stack using Node.js, mongoDB, Redis, and Ansible. To begin, you have to ensure each of these services are compatible with the same version of OS you're on. This may mean downgrading or upgrading some services to satisfy the OS requirement. Then, making sure each service has compatible libraries and dependencies. It's not uncommon to find out two or more services require different versions of the same dependency. Finally, if you ever need to upgrade a service down the road, you have to go through all these checks all over again. This dependency matrix gets the devilish name of the "matrix from hell." Add more than one developer to the mix and you can picture how hard it is for an entire development team to ensure everyone is using the same versions of each service. Also, setting up the new hire with the right environment can be a dull task for a newbie. Some dev teams may even be using different development, testing, and production environments which slows down development, building, and shipping.

{{< figure src="/uploads/hell-matrix.png" caption="from the Free Tutorial">}}

Docker solves this by running each component in a separate container, each with its own dependencies and its own libraries. Build the Docker environment one time and every developer is on the same page.

### What are containers?
* Completely Isolated Environments each with their own:
    * processes
    * services
    * network interfaces
    * mounts
* While all sharing the same OS kernel
    * e.g. If the host OS is Ubuntu, then Docker can run any OS on top as long as it's based on the same Linux kernel (so, no Windows)
        * **Note:** When running a Linux container on a Windows machine, Docker is running the container on a virtual machine  

* Docker is a high-level tool that makes it easy to setup low-level LXC containers
* Docker is *not* meant to virtualize and run different OSes and kernels on the same hardware
* The **main purpose** of Docker is to package & containerize apps so that they can be ran and shipped anywhere, anytime as many times as you want

### Containers vs. Virtual Machines
{{< figure src="/uploads/container-vs-vm.png" caption="Get out of the way dude!">}}

### Image vs. Container
* Image is a package or template
* Container is a running instance of an image

### DevOps Connection
* Traditionally, a development team would develop a project and then handed off to an operations team to deploy & manage in the production environment
    * The dev team would provide documentation for the Ops team
    * When problems arose, the Ops team would seek the Dev team for help
* Docker allows the Dev and Ops teams to work more hand-in-hand
    * Both teams contribute to create a docker file which becomes a docker image which is used by the Dev team to develop the application and by the Ops team to deploy the application

## Docker Basic Commands

| cmd                 | description                        |
| ------------------- | ---------------------------------- |
| run \<name> | start a container|
| ps | list running containers |
| ps -a | list all containers |
| stop \<name or id> | stop a container |
| rm \<name>| remove a container permanently|
| images | list images |
| rmi \<name> | remove images |
| pull \<name>| download an image|
| run \<name> \<command> | append a command (e.g. docker run ubuntu sleep 5)|
| exec \<command>| execute a command|
| run -d | run in detached mode|
| attach \<id> | re-attach to a container|



**Note:** a container only lives as long as a process is alive
