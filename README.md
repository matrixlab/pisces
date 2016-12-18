# Pisces - selfreproductive operating system

I want to start from the observations that are very clear for me.

First, many things that were buzz words even at beginning of this year are reality now. The IoT is one of them. The others are: 
- a blending of augmented reality and IoT;
- streaming processing is getting traction with implementation of general computing engines like Spark, Flink, Storm, Samza;
- container orchestration frameworks like Kubernetes, Swarm, rtk created an execution environment that is similar to Amazon Cloud, but based on containers instead of VM;
- new breed of operating systems like CoreOS created a new paradigm in IT, replacing application servers and frameworks that were thrive on them (Java EE, Spring, and even micro-services).

All features of current application's building blocks are moving down to the operating system level. Basically, we are getting back to the early days of operating systems (DOS or UNIX) when each program executed by itself and it was running directly on the operating system level. 

Now containers are generic substitutes of the plain old programs of that time, but the modern operating systems is serving the same role for the containers that they did back at that days for the individual programs. They are taking care about everything related to the running containers (programs) and to the the managing communications between them.

Situation is similar, but not the same. Now we can support an upgrade of the running program/applications/containers in run-time without stopping system. Multiple techniques can be used to achieve this. Some of them are widely used  with micro-services (Netflix, for example) or, in case of Java programs, OSGi and Karaf provide support for replacing old version of Java libraries with a new ones in run-time without stopping application.

Similar patterns implemented in operating system. Google Chrome and CoreOS are two operating systems that are running on two partitions: active and passive. The active partition is running operating system, on the other hand, the passive partition is serving as a playground for building a next version of the OS. As soon as the new version of OS would be completed the partitions would be switched and the active partition will get the passive partition status and passive will turn into active.

All of these elements actually can be used as building blocks of the John von Neumann Self Reproductive System (SRS).

Here is a very quick introduction into JvN SRS. The original model supposed to mathematically prove the possibility of building Self Reproductive System.

JvN introduced the system that composed from three modules S(A, B, C):
A - universal constructor;
B - universal copier;
C - universal controller.

The C is just a simple state machine with very simple behavior.

The B is a module that can replicate any other object, including itself. The copy could be a real object or a blue-print that is detailed enough to reproduce the new instance of the object.

The A is the module that can build any object based on the copy (blue-print) of the building object as an input.

Now is a whole process. 

C (controller) asking B to make copies of all modules: B: A --> copy(A); B: B --> copy(B ); B: C --> copy(C).

Then C will order A to use created copies and build new instances: A: copy(A) --> A1; A:copy(B ) --> B1; A: copy(C) --> C1.

And finally C will combine new instances into a new system S1(A1, B1, C1). Now this system is ready to continue self reproduction process.

CoreOS is created as a container management system from the ground. The following are objectives:
- All applications run as Containers on top of OS.
- Base OS should be small and fast to bootup.
- Services are managed by Init system. eg: Systemd
- OS need to have auto-update strategy like web browsers.
- Systems needs to be managed as a cluster rather than individual node.
- Built-in support should be present for Service discovery, Container networking and Orchestration.

CoreOS has support for many things that self reproduction needs. The only missing part in the CoreOS is self-description (meta-information) module. This module should extend the list of core elements of CoreOS that already includes:
- systemd as Init system;
- etcd as distributed database (like S3 on AWS);
- fleet as Cluster service scheduler;
- flannel for container networking;
- docker, rkt for containers.

So, the concept of a new CoreOS (lets call it Pisces)  is to implement all mechanisms that will allow self reproduction of the operating system.

Metadata management system (service) is a first step. MMS would serve a very similar role as etcd (or S3 in AWS), but for metadata.

On the phase 1 we can implement the basic support for metadata management on OS level:
- the mmsgraph would hold and manage all meta information about resources of the OS;
- the mmsagent the agent that intercept all changes in the state of the OS resources;
- the mmsconsole the CLI and web interface to the MMS.

Phase 1 can be completed in a few months and it will let us to be the first company that will introduce self reproduction on the operating system level.

On the phase 2 we can extend self reproduction by providing mechanisms of self reproduction on the user application level. 

This development of the Pisces project has to be an Open Source project. The reason for that is to mark our right on product as copyright holders. OS may survive only if it used by a very big community. One of the reasons of the success of the Docker is the fact of being Open Source with a very permissive license (Apache v. 2).

By introducing self reproductive OS we would be the facto IP holders of the totally new kind of operating systems.

Pisces project is an ultimate operating environment for the IoT applications. 
