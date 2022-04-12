author: ""
---

# Introduction to Docker and Containers

Source for this presentation can be found at:

https://github.com/pcrockett/docker-intro

---

## History

The old way to host a service: **physical servers**

* Expensive
* Poor compartmentalization
* Hard to manage
* Great performance

---

## History

After physical servers: **virtual machines**

* Hardware emulation, OS within an OS
* Excellent compartmentalization
* Less expensive / better hardware utilization
* Very high overhead, performance hit

---

## History

After VMs: **containers**

* Like a compromize between physical servers and VMs
* _Pretty good_ compartmentalization
    * tighter integration with physical machine
* _Very low_ overhead

---

## What is a container?

* A regular Linux process (oversimplification...)
* Has a "restricted view" of the world
* Runs directly on top of the Linux kernel
* Docker is just one of many container tools


