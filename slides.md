author: ""
---

# Introduction to Docker and Containers

Source for this presentation can be found at:

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

* Like living in a jail cell
* _Very low_ overhead
    * it's just a normal process, with restrictions
* _Pretty good_ compartmentalization
    * tighter integration with physical machine

---

## Background

### What is a (Linux) container?

* "container" != "Docker"
* A regular Linux process
* Runs directly on top of the Linux kernel
* Has a "restricted view" of the world
    * capabilities and namespaces

---

## Background

### What is a container runtime?

Container runtimes are simply tools that make it easy to run processes inside namespaces / with restricted capabilities.

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

### Dockerfile Example

Quiz: What do you think happens when we add this?

```docker
# Remove the first file we created
RUN rm some-file
```

---

## Docker

### Practical Example

Let's create a personal sandbox container.

---

## Docker

### Differences between Linux, macOS, Windows

* Non-Linux systems don't have the same capability / namespace features
    * Docker creates a Linux VM, manages it for you
    * `root` inside the container == `root` in the Linux VM
* Linux systems run containers "closer to the metal" - no VM
    * `root` inside the container == `root` on **YOUR COMPUTER**
    * Cannot use Docker without elevated privileges
    * _Side note:_ Linux users consider using Podman instead of Docker

---
