🐳 Docker Complete Guide
Part 2 – Docker Architecture, Installation & First Practical
Chapter 3 – Docker Architecture (Complete)

In the previous chapter, we learned:

Why Docker was created
What Docker is
Docker Image
Docker Container

Now let's understand how Docker works internally.

Docker Architecture

Docker consists of multiple components working together.

                Developer
                    │
                    │
          Docker CLI / Docker Desktop
                    │
                    ▼
             Docker Daemon
                    │
                    ▼
             Docker Engine
                    │
        ┌───────────┴────────────┐
        │                        │
        ▼                        ▼
 Docker Images              Docker Containers
        │
        ▼
 Docker Registry (Docker Hub)

Let's understand each component one by one.

1. Docker CLI (Command Line Interface)

Docker CLI is the command-line tool used to communicate with Docker.

Whenever we execute a Docker command,

Example

docker images

docker ps

docker pull nginx

docker run nginx

the command is sent to Docker Daemon.

Responsibilities

Docker CLI is responsible for

Pulling Images
Creating Containers
Starting Containers
Stopping Containers
Removing Containers
Managing Networks
Managing Volumes

CLI itself doesn't execute anything.

It simply sends requests.

Flow
Developer

↓

docker run nginx

↓

Docker CLI

↓

Docker Daemon
Docker Desktop

Docker Desktop provides a graphical interface.

Using Docker Desktop we can

View Containers
Stop Containers
Delete Containers
View Images
Manage Volumes
Manage Networks

Docker Desktop internally uses the same Docker Engine.

CLI and Docker Desktop perform the same work.

Only the interface is different.

Docker Daemon

Docker Daemon is the background service.

It continuously runs in the background waiting for Docker commands.

Whenever Docker CLI receives a command,

it forwards it to Docker Daemon.

Responsibilities

Docker Daemon performs all actual work.

It can

Build Images
Pull Images
Create Containers
Run Containers
Stop Containers
Delete Containers
Create Networks
Create Volumes

Without Docker Daemon,

Docker commands will not work.

Example

Suppose you execute

docker run nginx

The following happens internally.

Developer

↓

docker run nginx

↓

Docker CLI

↓

Docker Daemon

↓

Checks Image

↓

Image Available?

↓

YES

↓

Create Container

↓

Run Container
What if Image Doesn't Exist?

Suppose nginx image is not available.

Docker automatically downloads it.

Internal Flow

docker run nginx

↓

Image Found?

↓

No

↓

Download Image

↓

Docker Hub

↓

Store Image Locally

↓

Create Container

↓

Run Container

This is why Docker is very easy to use.

Docker Engine

Docker Engine is the core runtime of Docker.

It consists of

Docker CLI
Docker Daemon
REST API

It is responsible for running containers.

Think of Docker Engine as the heart of Docker.

Without Docker Engine,

nothing can execute.

Docker Registry

Docker Registry is a storage location for Docker Images.

There are two types.

Public Registry

Example

Docker Hub

Contains thousands of ready-made images.

Examples

nginx
mysql
redis
postgres
ubuntu
openjdk
eclipse-temurin
Private Registry

Many companies maintain their own Docker Registry.

Reasons

Security
Private Images
Company Applications

Example

Company Registry

↓

Employee Service

↓

Order Service

↓

Payment Service

↓

Notification Service
Docker Hub

Docker Hub is the default public registry.

Whenever Docker cannot find an image locally,

it automatically downloads it from Docker Hub.

Example

docker pull mysql

Docker downloads

MySQL Image

↓

Stores Locally

↓

Ready to Use
Complete Internal Working
Developer

↓

docker run mysql

↓

Docker CLI

↓

Docker Daemon

↓

Image Exists?

↓

No

↓

Docker Hub

↓

Download Image

↓

Save Image

↓

Create Container

↓

Run Container

↓

Application Running
Chapter 4 – Docker Installation

Docker supports

Windows
Linux
macOS

For Windows and macOS,

Docker Desktop is recommended.

Step 1 – Download Docker Desktop

Visit

https://www.docker.com/

Download Docker Desktop according to your operating system.

Step 2 – Install Docker Desktop

Run the installer.

Complete the installation.

Restart your computer if required.

Step 3 – Start Docker Desktop

Open Docker Desktop.

Wait until Docker Engine starts.

You should see

Docker Engine Running
Step 4 – Verify Installation

Open Terminal or Command Prompt.

Execute

docker --version

Example Output

Docker version 28.x.x

Now verify Docker Engine.

docker ps

Expected Output

CONTAINER ID

IMAGE

COMMAND

CREATED

STATUS

PORTS

NAMES

If both commands execute successfully,

Docker has been installed successfully.

Common Error

Suppose you execute

docker ps

and receive

Cannot connect to Docker daemon

Reason

Docker Desktop is not running.

Solution

Start Docker Desktop.

Wait until Docker Engine starts.

Then execute

docker ps

again.

Chapter 5 – First Docker Practical

Let's run our first Docker container.

Step 1 – Search Image

We want to run nginx.

First pull the image.

docker pull nginx
What Happens Internally?
Docker CLI

↓

Docker Daemon

↓

Docker Hub

↓

Download nginx Image

↓

Store Locally
Output
Using default tag: latest

latest: Pulling from library/nginx

Download complete

Status: Downloaded newer image for nginx
Step 2 – Check Downloaded Images

Execute

docker images

Output

REPOSITORY      TAG

nginx           latest

Meaning

Docker has successfully downloaded the image.

Step 3 – Run Container

Execute

docker run nginx

Docker creates a container.

Internal Flow
Docker Image

↓

Create Container

↓

Assign Container ID

↓

Allocate Resources

↓

Start nginx

↓

Container Running
Step 4 – Verify Running Container

Execute

docker ps

Output

CONTAINER ID

IMAGE

STATUS

PORTS

NAMES

Now your container is running successfully.

Step 5 – View All Containers

Running containers

docker ps

All containers

docker ps -a

Difference

Command	Description
docker ps	Running Containers
docker ps -a	Running + Stopped Containers
Step 6 – Stop Container

Find the container ID.

Example

ab123cd45

Stop the container.

docker stop ab123cd45

Output

ab123cd45
Step 7 – Start Container Again
docker start ab123cd45

Container starts again.

Step 8 – Restart Container
docker restart ab123cd45

Docker stops and immediately starts the container.

Step 9 – Remove Container

A running container cannot be removed.

First stop it.

docker stop ab123cd45

Now remove it.

docker rm ab123cd45

Output

ab123cd45

Container deleted successfully.

Step 10 – Remove Image

First remove every container created from the image.

Then execute

docker rmi nginx

Output

Deleted: sha256:xxxxxxxx

Image removed successfully.

Summary

In this chapter, we learned:

✅ Docker CLI
✅ Docker Desktop
✅ Docker Daemon
✅ Docker Engine
✅ Docker Registry
✅ Docker Hub
✅ Docker Installation
✅ Verify Installation
✅ Pull Image
✅ Run Container
✅ Stop Container
✅ Restart Container
✅ Remove Container
✅ Remove Image
💡 Interview Questions
Q1. What is Docker CLI?

Docker CLI (Command Line Interface) is a command-line tool used by developers to communicate with Docker. It sends commands to the Docker Daemon, which performs the actual operations.

Q2. What is Docker Daemon?

Docker Daemon is a background service that manages Docker Images, Containers, Networks, and Volumes. It listens for Docker CLI requests and performs the requested operations.

Q3. What is Docker Hub?

Docker Hub is Docker's default public registry that stores Docker Images. When an image is not available locally, Docker automatically downloads it from Docker Hub.

Q4. What happens internally when docker run nginx is executed?
Docker CLI receives the command.
Docker Daemon checks whether the nginx image exists locally.
If not found, Docker downloads it from Docker Hub.
Docker creates a new container from the image.
Resources are allocated, and the nginx process starts inside the container.
