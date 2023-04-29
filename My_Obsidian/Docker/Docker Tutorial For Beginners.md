#docker

Today, we will open a new treasure of knowledge called, Docker. In this Docker Tutorial, we will see a brief introduction to Docker. Moreover, we will look at Docker architecture, engine, and platform.

Also, we will discuss Docker container and Docker example. This Docker tutorial also includes the **Docker feature** and **why we use Docker**.

So, let’s start Docker tutorial for beginners.

## What is Docker?

An open platform for developing, shipping, as well as running applications, is what we call Docker. Also, we can say, Docker is a container-management service. It enables us to separate our applications from our infrastructure hence we can deliver software quickly.

As its job, it is possible to manage our infrastructure, in the same ways we use to manage our applications, with the help of Docker.

Moreover, with the help of Docker’s methodologies for shipping, testing, and deploying code quickly, it is possible to reduce the delay between writing code remarkably or running it in production.

The main **purpose of Docker** is to easily develop applications and further ship them into containers so that they can then be deployed anywhere. This feature is very helpful to developers.

Docker has become the buzzword for modern world development, since the initial release of Docker in March 2013, especially in the face of Agile-based projects.

## Docker Tutorial – Audience

As we know, Docker has spread like destructive fire across the industry and also it is really making an impact on the development of new generation applications.

Hence, anyone who is interested in learning all the aspects of Docker or interested in learning Docker as a container service can go through this Docker Tutorial.

## Apache Docker Tutorial – Prerequisites

Well, in order to learn Docker, it is must to have knowledge of basic concepts of Windows as well as the various programs which are already available on the Windows operating system. Also, it would be a great advantage if the readers already have some exposure to Linux before learning Docker.

## Docker Tutorial – Platform

Docker offers an ability to package and run an application in a loosely isolated environment, generally, that is known as a container. It is possible to run many containers simultaneously on a given host, because of isolation and security.

Since there is no need for the extra load of a hypervisor, Containers are lightweight in nature. However, they run directly within the host machine’s kernel.

It simply signifies that we can run more containers on a given hardware combination than if we were using virtual machines. Also, we can run these containers within host machines those are actually virtual machines!

In order to manage the lifecycle of our containers, Docker offers tooling as well as a platform:

By using containers, Develop application and its supporting components.

Especially, for distributing and testing your application, the container becomes the unit.

Deploy application into a production environment, either as a container or an orchestrated service, it works the same whether the production environment is a cloud provider, a local data center, or even if a hybrid of the two.

## Docker Engine

However, a client-server application with several major components like a server, REST API and CLI Client, is what we call Docker Engine. Let’s understand its components in detail:

-   A type of long-running program called a _daemon process_ (the dockerd command), is a Server.
-   An API which specifies interfaces which programs can use to talk to the daemon as well as instruct it what to do is a _REST API_.
-   And, at last, a c_ommand line interface (CLI)_ client (the docker command).

Basically, to control or interact with the Docker daemon through scripting or direct CLI commands, the CLI uses the Docker REST API. Although, there are many Docker applications those use the underlying API and CLI.

In addition, the daemon manages and creates Docker objects, like containers, networks,  images, and volumes.

## Why we use Docker?

-   Fast, consistent delivery of your applications

By allowing developers to work in standardized environments, Docker streamlines the development lifecycle, with the help of local containers that offer our applications and services as well. Moreover, for continuous integration and continuous delivery (CI/CD) workflows, containers are great.

-   Responsive deployment and scaling

The container-based platform of Docker permits for highly portable workloads. Its containers can run on several platforms like, on physical or virtual machines in a data centre, on a developer’s local laptop, on cloud providers, or also in a mixture of environments.

In addition, due to the lightweight nature and portability of Docker, it is easy to manage workloads dynamically, scaling up or tearing down applications and services in near real time.

-   Running more workloads on the same hardware

Since Docker is fast and lightweight, it offers a viable, cost-effective alternative to hypervisor-based virtual machines. Hence, we can use much of our compute capacity in order to achieve our business goals.

Also, we can say, for high-density environments as well as for small and medium deployments especially where we need to do more with fewer resources, Docker is perfect a right choice.

## Docker Architecture

The type of architecture which Docker uses is a client-server architecture. As a process, its client talks to the daemon, that performs the heavy lifting of a building, running, and distributing our Docker containers.

However, both the Docker client and the daemon can run on the same system, else we can also connect a Docker client to a remote Docker daemon. Moreover, using a REST API, over UNIX sockets or a network interface, the Docker client and the daemon communicate.

[![Docker Architecture](file:///Users/haluk/.config/joplin-desktop/resources/79874a8dc9384232bad992e2baa54732.jpg)](https://data-flair.training/blogs/wp-content/uploads/sites/2/2018/10/Docker-Architecture-01.jpg "https://data-flair.training/blogs/wp-content/uploads/sites/2/2018/10/Docker-Architecture-01.jpg")

Docker Tutorial – Architecture of Docker

#### i. The Docker daemon

The daemon listens for the Docker API requests and also manages Docker objects. Also, it communicates with other daemons in order to manage Docker services.

#### ii. The Docker client

Many Docker users interact with Docker by using the Docker client. It is possible to communicate with more than one daemon, using the Docker client.

#### iii. Docker registries

A registry that stores **Docker images** is what we call Docker registries.

## Docker Objects

There are several types of Docker Objects we use, such as images, networks, containers, volumes, plugins, & other objects. Some of those objects are:

[![Docker Tutorial](file:///Users/haluk/.config/joplin-desktop/resources/40a3d755214342ecb1c6193b45f6b5cc.jpg)](https://data-flair.training/blogs/wp-content/uploads/sites/2/2018/10/Docker-Objects-01.jpg "https://data-flair.training/blogs/wp-content/uploads/sites/2/2018/10/Docker-Objects-01.jpg")

Docker Tutorial – Docker Objects

### i. Docker Images

A read-only template with instructions to create a Docker container is what we call IMAGES. Usually, we can say, an image is based on another image, along with some additional customization.

Let’s understand this with an example, suppose we build an image that is based on the Ubuntu image, yet installs the Apache web server, our application, and the configuration details which we might need to make our application run.

It is possible to create our own images else we can also use those which are created by others and published in a registry. Images are so lightweight, fast and small if compared to other virtualization technologies.

### ii. Docker Containers

Whereas, a runnable instance of an image is what we call a Container.  By using the Docker API or CLI, we can easily create, start, stop, move, or delete a container.

The more we can do from it is we can connect a container to one or more networks, or we can create a new image based on its current state, also we can attach storage to it.

## Components of Docker

There are several Components of  Docker:

[![Docker Tutorial](file:///Users/haluk/.config/joplin-desktop/resources/a73aee2eb9254c349745d919cf92d282.jpg)](https://data-flair.training/blogs/wp-content/uploads/sites/2/2018/10/Components-of-Docker-01.jpg "https://data-flair.training/blogs/wp-content/uploads/sites/2/2018/10/Components-of-Docker-01.jpg")

Docker Tutorial – Components of Docker

**i. Docker for Mac **

This one grants permission to run Docker containers on the Mac OS.

**ii. Docker for Linux **

Similarly, this component grants permission to run Docker containers on the Linux OS.

**iii. Docker for Windows **

While we need to run Docker containers on the Windows OS,  this component grants permission for that.

**iv. Docker Engine **

In order to build Docker images and to create Docker containers, Docker Engine helps us.

**v. Docker Hub **

Basically, to host various Docker images, **Hub** is the registry which we use.

**vi. Docker Compose **

And, to define applications using multiple Docker containers, we use Docker Compose.

## Docker Tutorial – Features

Here we are listing some best Docker Features:

-   By providing a smaller footprint of the operating system via containers, Docker can reduce the size of the development.
-   For teams across different units, such as development, QA and Operations, Containers makes easier to work seamlessly across applications.
-   It is possible to deploy **Docker containers** anywhere, like on any virtual machines and physical and even on the cloud.
-   Docker containers are very easily scalable since they are pretty lightweight.

So, this was all in Docker Tutorial. Hope you like our explanation.

## Conclusion – Docker Tutorial

Hence, in this Docker tutorial, we have seen a comprehensive introduction to Docker. Also, this includes the brief introduction to its architecture, its objects, engine and many more. However, there are many more Docker tutorials in a queue.

So, stay tuned to DataFlair, for more detailed articles on Docker for the better understanding of the Topic. Still, if you have any query regarding Docker tutorial, ask in the comment tab.
