Docker Introduction
============

# Introducing Docker

## What is Docker?

![https://www.docker.com/sites/default/files/horizontal.png](../images/docker-horizontal.png)

* Docker is the current industry standard container format.
* Docker (the company) also makes developer tools:
* Docker for Windows
* Docker for Mac
* Docker for Linux
* Docker also has server-side container frameworks for Linux and Windows
* Windows versions run on top of Hyper-V

Notes:

Instructor Notes:

Participant Notes:

Docker's name is almost synonymous with containers.   While arguably Docker's contribution
is not the largest or the most significant to the container ecosystem, it is the one that
is closest to the developer -- as the developer relies on Docker tools to create container
application images. 

---

##  Docker uses the Host Kernel
* Docker will use the host kernel on Linux.
* What about Windows and Mac (Developer) Versions of Docker?
  - Windows and Mac versions run a virtualized Linux kernel in a VM
  - Only the kernel runs in the VM.  The container runs separately.
  - In Windows, the VM is in Hyper-V (and thus requires Hyper-V to be installed)
  - On Mac, the VM runs in Apple’s Hypervisor Framework
* Windows Server Native Windows Kernels
  - Windows Server Applications can run in Windows Native Containers on Windows Server
  - No VMs involved. (although you may want a VM for security reasons)


Notes:

Instructor Notes:

Participant Notes:

It's important to understand how containers work.  They generally use the host kernel. We say
generally because in fact on non-Linux platforms the kernel is usually virtualized.  

The situation is a little complicated when it comes to Windows, because there are multiple 
incompatible Windows kernels for various flavors of Windows.  Because of that, most Windows
"Native" containers run in virtualized mode except in production.

---

## Docker for Windows (Developer)

![https://www.docker.com/sites/default/files/horizontal.png](../images/docker-horizontal.png)

 * Docker for Windows has the following requirements:
   * Windows 10 Professional 64 Bit (or Higher)  (not Home, Not Home Pro)
   * Virtualization Extensions Available in CPU and turned on in BIOS.
   * Hyper-V (optional component) installed
   * Reasonable CPU / Memory requirements
 * Docker Toolbox
   * Windows Users unable to run Docker for Windows can run in Docker Toolbox
   * Toolbox requires Oracle VirtualBox for Virtualization.

![http://www.virtualizationsoftware.com/wp-content/uploads/2013/04/hyperv-logo2.jpg](../images/windows-310290_1280.png)

Notes:

Instructor Notes:

Participant Notes:
Docker for Windows has fairly steep requirements.

Why does Docker require Hyper-V?  Because all containers on Windows require virtualization. Even windows containers require virtualization because those containers require Windows Server kernels which are different from Windows 10 (client) kernels.

Hyper-V does not run on Windows Home versions (most consumer-grade windows machines).  So, Docker for Windows will not run on those versions either.  One needs a Windows Professional.

Hyper-V will require that Virtualization extensions be turned on in the BIOS.  Typically, from the factory these are turned off on client machines for security reasons, as some exploits have targeted these instruction sets.

Docker Toolbox can be used together with Oracle VirtualBox to run Docker containers on older versions of windows such as 8.1 or 7 or on Home versions of Windows 10.  However, it’s a pretty painful developer experience, so it’s not recommended.


---

## Docker and Windows Server

![https://www.docker.com/sites/default/files/horizontal.png](../images/docker-horizontal.png)

* Docker for Windows Server is designed for App deployment rather than Development
  - Developers should use Docker for Windows instead.
  - Supports running Linux containers containers (via Hyper-V)
  - And Native Windows Containers (using Hyper-V or native Windows Containers)
* Native Windows Containers
  - Native Windows Containers must use the same Windows Server kernel as the host
  - Both host and guest must be Windows Server to run native (not Windows 10)
  - Native Windows Containers must use Windows Server kernel
  - Able to run native containers without virtualization
  - Minimal Performance Penalty

![http://www.virtualizationsoftware.com/wp-content/uploads/2013/04/hyperv-logo2.jpg](../images//hyperv-logo2.jpg)

Notes:

Instructor Notes:

Participant Notes:

Native Windows Containers are not all that common at this time, but Microsoft is pushing them because they
realize that the Windows platform needs to be have this capability to continue to be relevant as a server-side
platform.  

---

## Docker on Windows Use Cases

|                     | Windows 10 (Linux Kernel) | Windows 10 (Windows Server Kernel) | Windows Server (Virtualized Kernel) | Windows Server (Native Kernel) |
|---------------------|---------------------------|------------------------------------|-------------------------------------|--------------------------------|
| Use Case            | Developer                 | Developer                          | Deployment                          | Deployment                     |
| Container OS        | Linux                     | Windows Server                     | Linux or Windows Server             | Windows Server                 |
| Isolation from Host | Yes (via Hyper-V)         | Yes (via Hyper-V)                  | Yes (via Hyper-V)                   | Not Virtualized                |
| Startup Delay       | 500ms - 1s                | 500ms - 1s                         | 500ms - 1s                          | No Delay                       |

Notes:

Instructor Notes:

Participant Notes:

This slides shows the relative use cases of various use cases on Windows. Docker realizes that Windows is its most common platform for development, even for applications 
that will not be deployed on Windows.  Because of this, the Windows platform has the richest number of options.  Windows users need to choose between developing 
"native" Windows server containers or Linu containers.  The advantage of the native containers is that there is minimal delay in starting a native container,
similar to what one would expect on Linux platforms.


---


## Docker on Mac (Developer)

![https://www.docker.com/sites/default/files/horizontal.png](../images/docker-horizontal.png)

* Docker on Mac is only supported as a development platform.
  - There are no ”native” mac containers as there are on Linux and Windows
* Docker for Mac uses only Linux containers
  - Windows containers can be run entirely inside a VM 
  - Linux Containers use a VM for the Linux kernel only
* Docker for Mac uses Apple’s VM Hypervisor

![http://www.thriftysigns.com/apple-logo-decal-sticker-apple-logo](../images/apple-logo-decal-sticker-apple-logo-500x500.png)

Notes:

Instructor Notes:

Participant Notes:

Apple is an extremely popular platform for development, so it comes as no surprise that Docker has versions for this platform.  As Apple has no real presence in the 
data center, it is strictly for development.

While it's often thought that Apple is built on top of Unix, it has chosen BSD Unix as its base, which is not compatible with the Linux Kernel.  So, like Windows,
Mac users must run in a VM, though unlike Windows, all modern Mac systems are capable of running virtualization without any special actions. 

There is no way to run "native" Windows containers on Mac, except for in a VM.  This isn't a common use case.

---

## Lab 1: Installing Docker

 * docker-labs/01-install/README.md

Notes:

Instructor Notes:

Participant Notes:

---

# Docker Hub and Container Registries

## What is Docker Hub?

![https://www.docker.com/sites/default/files/horizontal.png](../images/docker-hub-logo.png)

 * Docker Hub is a registry of containers
 * Think "GitHub" for containers
 * Thousands of Containers Available
 * We rarely start from scratch
   - Use an image from Docker Hub!


Notes:

Instructor Notes:

Participant Notes:

If Docker's container image format is its first great contribution, Docker Hub and similar container registries are the second. The fact that users can
share and get container images from Docker Hub is a huge catalyst to containers, as it allows code to be shared across multiple teams.  More importantly,
it means there's no reason to re-invent the wheel. In fact, Docker Hub is designed to minimize re-invention of any kind.

We will see later how Docker's build process allows us to leverage other people's work.

---

## Container Registries

 * Docker Hub is public.
 * Your company data is **NOT**.
 * You may want to have your own container registry.
 * But we may still use Docker Hub as well.

Notes:

Instructor Notes:

Participant Notes:

Corporate environments invariably have Docker Hub blocked, much like Maven repository coordinate and Github itself. Because of this, companies are able to use
private container registries.  In fact, this is encouraged in Docker and rarely will someone attempt to put something out on public Docker Hub unless there is a
very good reason to do so.

The doesn't mean that one can't use Docker Hub.  If you want to start with, say, a basic linux image, using something from Docker Hub as a start makes
a lot of sense.

---


## Docker Pull
 * Typing `docker pull` will download a container.
 * In the lab, we will use a container called `alpine`:
   - Ultra-lightweight Linux 
   - 4MB in Size (tiny).

```bash
docker pull alpine
```

Notes:

Instructor Notes:

Participant Notes:

Anyone who has used Github and Git will find the Docker syntax easy to remember.  Instead of using a copy of the source code repository, Docker will
store the binary container image (usually a hash) in a local place on the user's hard drive.

---


# Docker Commands

## Docker LS (list)
 * typing `docker ls` will **list** your containers
 * It will only show **running** containers
 * Stopped containers say `docker ls -a'

```console
 $ docker ls

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              e38bc07ac18e        5 weeks ago         1.85kB
alpine              latest              3fd9065eaf02        4 months ago        4.15MB
```

Notes:

Instructor Notes:

Participant Notes:

Running "docker ls" will show all the containers that you currently have.  Note that you may see containers show up that aren't in fact direclty being used.
That's because the docker pull will recursively bring down containers and store them.

Note that every time you start a container, you will continue to see that container in docker ls.   Do not be alarmed, because only the differences between
the original image and the stopped container will be stored.  

---


## Docker Run
 * We can run a docker container with `docker run`.
 * Example: running alpine

```bash
docker container run alpine /bin/ash
```
 * This will run alpine and start a shell
 * Alpine doesn't have "bash" -- too big!

Notes:

Instructor Notes:

Participant Notes:

Docker containers can be started with "run" -- this is because it's better to look at running a container as more like an app than a VM.  

Alpine is extremely popular as mini-sized Linux to start containers.  While running with a starter like ubuntu certainly gives a lot more
power plus the familiarity with ordinary tools like "bash", alpine is great when all we really need is just enough of an OS to run our 
application.

---



## Running a Shell
 * We don't *typically* ssh to our container.
 * We simply run a shell in the container

```console
docker container run -it --rm alpine /bin/ash
```

 * What does this mean?
   - -i : interactive mode
   - -t : terminal mode
   - --rm : remove container after we are done
   - /bin/ash : bash is big and needs to be installed.  ash (almquist shell) is small. We also have old-school sh.

Notes:

Instructor Notes:

Participant Notes:

Many users ask how to "ssh" to the container.  This isn't typically how we accomplish this, instead, what we do is to attach our terminal to the container.

Some containers we probably want to automatically stop when we are not longer using the container. This depends a lot of the use case.  If the container is
more of background service, then we probably do not want to do this.  However, if it is an interactive application then this is not a bad idea.

---

## Lab 2.1: Alpine

  * Navigate to 02-containers/2.1-alpine.md

Notes:

Instructor Notes:

Participant Notes:

---

## Docker RM
 * What happens if we need to delete a container?
 * The `docker rm` command will do this trick for us.


```bash
docker container --rm ls -l
```

Notes:

Instructor Notes:

Participant Notes:

Running "docker rm" is a good way to clean up and de-clutter our container registry.  That said, one should not expect to save lots of space by running docker rm,
because even larger container images are stored in the base repository, and deleing our derived images from these will not save an extraordinary amount of space.  
Remember, Docker overlays changes from one filesystem to the next, so only the changes will be removed..

---

## Removing a Container
 * `docker rm` does **NOT** delete the container **image**.
   - The container image is from Docker Hub.
   - It is stored locally in our local repo.
 * It deletes tehe container instance
   - The instance will container an overlay
   - Any changes to the original image are the overlay.
   - This is why we need OverlayFS in Docker.

Notes:

Instructor Notes:

Participant Notes:

We differentiate between the container image and the container instance.  The image is not going to be directly deleted this way, but the instance
will be. 

Knowing the difference between instance and image is extremely important.

--- 

## Lab 2.2: Deleting

  * Navigate to 02-containers/2.2-deleting.md
 
Notes:

Instructor Notes:

Participant Notes:

