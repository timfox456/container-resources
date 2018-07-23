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

---

## Container Registries

 * Docker Hub is public.
 * Your company data is **NOT**.
 * You may want to have your own container registry.
 * But we may still use Docker Hub as well.

Notes:

Instructor Notes:

Participant Notes:

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

--- 

## Lab 2.2: Deleting

  * Navigate to 02-containers/2.2-deleting.md
 
Notes:

Instructor Notes:

Participant Notes:

