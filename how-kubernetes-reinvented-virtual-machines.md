# How Kubernetes Reinvented Virtual Machines
- Before containers, bare-metal servers or virtual machines were used to run your application
- metal servers were secure but did not allow for scaling as fast
- an analogy that describes this is pet vs cattle
- a pet server is one you would need to take care of, if it goes down it needs to be fixed, treated, like always taking care of a pet
- a cattle server if something goes wrong, can be replaced right away with another, which is what virtual machines allowed
- what containers did was much like how VMs allowed slicing a bare-metal server into several smaller machines, containers split a linux box into tens or hundreds of isolated environments
- containers give you the ability to pack an application with all its dependencies with a certain version of OS, and run wherever docker is installed greatly improved the reproducability of workloads
- the same container image runs identically on a developer's laptop, in CI/CD, and in production, eliminating 'works on my machine problems


## From Containers to Kubernetes

- Docker solved packaging and running applications
- But in production, you need to manage hundreds/thousands of containers across many servers
- Questions Docker couldn't answer:
  - What happens when a container crashes?
  - How do you distribute containers across multiple servers?
  - How do containers discover and talk to each other?
  - How do you update containers without downtime?
  - How do you scale containers up/down automatically?

**This is where Kubernetes comes in:**
- Kubernetes is a "container orchestrator"
- It manages the lifecycle of containers across a cluster of machines
- Automatically handles scheduling, scaling, networking, and recovery
- Turns a cluster of servers into one logical unit

**The Evolution:**
Bare Metal → VMs (pets) → VMs (cattle) → Containers → Orchestrated Containers (Kubernetes)
