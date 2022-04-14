---
author: ""
---

# Introduction to Docker and Containers

Source for this presentation and examples can be found at:

https://github.com/pcrockett/docker-intro

---

## Background

### History - Physical Servers

The old way to host a service

* Expensive
* Poor compartmentalization
* Hard to manage
* Great performance

---

## Background

### History - Virtual Machines

Great for reducing how many physical servers you have to manage

* Like living in the Matrix
* Hardware emulation, "computer within a computer"
* Excellent compartmentalization
* Less expensive / better hardware utilization
* Very high overhead, performance hit

---

## Background

### History - Containers

A middle ground between physical and virtual servers

* Less like the Matrix, more like a jail cell
* _Very low_ overhead
    * it's just a normal process, with restrictions
* _Pretty good_ compartmentalization
    * tighter integration with physical machine

---

## Background

### What is a (Linux) container?

* "container" != "Docker"
* Regular Linux process(es)
* Runs directly on top of the Linux kernel
* Has a "restricted view" of the world
    * control groups, namespaces, capabilities, blah blah blah

---

## Background

### What is a container runtime?

_Runtimes_ are tools that manage cgroups, namespaces, capabilities, etc. for processes.

* Example: LXD - "system containers"
    * Like a lightweight VM. Focus on deploying _systems_ easily.
* Example: Docker - "application containers"
    * Focused on running applications the same way _everywhere_.

---

## Background

### What is a container orchestrator?

* A tool that makes multiple containers work together
* Helps you build / manage a whole system of containers
* Ex: Docker Compose, Docker Swarm, Kubernetes, Nomad...
* Each tool strikes a different balance between complexity and power
* The more containers you have, the more helpful an orchestrator can be

---

## Docker

That's enough about containers in general. Let's talk about Docker specifically.

---

## Docker

### Basic Concepts: Images

* An image is like a snapshot of an operating system
* Contains a file system, with software and config files
* Containers run from the contents of an image
* Most images you can download from Docker Hub (though other repos exist)
* Tip: Stick to "official" Docker images unless you know what you're doing

---

## Docker

### Basic Concepts: Containers are disposable

* Images are immutable, but containers can modify their copy of an image
* When the container is destroyed _all changes are lost_
* Containers are frequently destroyed and recreated
* Changing state should be avoided if possible, however if needed...
* you can set up a _volume_ that is shared between container and host

---

## Docker

### Basic Concepts: Layers

* Each image made up of multiple layers
* Makes it possible to cache, reuse parts of a Docker image
* Dockerfiles build images by adding layers

---

## Docker

### Dockerfile Example

```docker
# Select your base image
FROM ubuntu:latest

# Create a layer on top of Ubuntu's image
RUN echo "foo" > some-file

# Create another layer on top of the previous one
RUN echo "bar" > some-other-file
```

---

## Docker

### Practical Example

Let's look at some examples now.

---

## Last Remarks

### Tools: Hadolint

Dockerfile linter. Error messages are helpful, but wiki is even more helpful:

https://github.com/hadolint/hadolint/wiki

Not only does it explain lint errors, but also suggests what you should do to correct the problem.

---

## Last Remarks

### Tools: Dockerfile reference

Everything you need to know about Dockerfiles:

https://docs.docker.com/engine/reference/builder/

Links to a good best practices article if you want to go deeper.

---

## Last Remarks

### There's More

There are lots of other Docker options that allow you to:

* run containers in background
* attach a terminal to a running container
* volume management
* image management
* etc.

---

## Last Remarks

### There's More

Docker help messages are very useful:

```bash
docker --help
docker [subcommand] --help
```

---

## Last Remarks

### Differences between Linux, macOS, Windows

* Non-Linux systems don't have the same capability / namespace features
    * Docker creates a Linux VM, manages it for you
    * _root_ inside the container == _root_ in the Linux VM
* Linux systems run containers "closer to the metal" - no VM
    * _root_ inside the container == _root_ on **YOUR COMPUTER**
    * Cannot use Docker without elevated privileges
    * _Side note:_ Linux users consider using Podman instead of Docker

---

## El Fin

That's it for now. Questions?

Perhaps in the future we can cover Docker Compose.

**Pull requests welcome!**

https://github.com/pcrockett/docker-intro
