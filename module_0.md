---

# 🐳 Docker Complete Guide (Theory + Practical)

> **Part 1 - Introduction | Why Docker? | What is Docker? | Docker Architecture**

---

# Welcome 👋

Welcome to this **Docker Complete Guide**.
By the end of this guide, you will be able to:

* Understand why Docker exists.
* Understand Docker Architecture.
* Install Docker.
* Create Docker Images.
* Run Docker Containers.
* Containerize a Spring Boot Application.
* Work with Docker Compose.
* Work with Docker Volumes.
* Understand Docker Networking.

---

# 📚 Course Roadmap

In this guide, we will cover the following topics:

```text
1. Why Docker Exists
2. What is Docker?
3. Docker Architecture
4. Docker Terminologies
5. Docker Installation
6. Containerizing Spring Boot Application
7. Docker Commands
8. Dockerfile
9. Port Mapping
10. Environment Configuration
11. Docker Compose
12. Docker Volumes
13. Docker Networking
```
---

# Chapter 1 — Why Docker Exists?

Before learning Docker,

we first need to understand **why Docker was created**.
Every technology exists because it solves a problem.
Docker also solves a real-world software development problem.
Let's understand that problem.

---

# Real Industry Scenario
Suppose there is a developer in your team.
His name is **Bob**.
Bob has developed a Spring Boot application.
His development environment looks like this.
```text
Developer : Bob
Operating System : Windows
Java Version : Java 25
Database : MySQL 8
Framework : Spring Boot
```

Everything is working perfectly on Bob's machine.
He successfully develops the application.

---

# Application Development Flow

```text
Bob

↓

Develop Spring Boot Application

↓

Application Runs Successfully

↓

Ready for Testing
```

Now Bob sends the application to the QA team.

---

# QA Environment
Suppose the QA engineer is **Alice**.
Alice deploys the same application on the QA server.
QA Environment
```
QA Engineer : Alice
Operating System : Linux
Java Version : Java 17
Database : MySQL 7
```
Notice something important.

The environments are completely different.

| Bob     | Alice   |
| ------- | ------- |
| Windows | Linux   |
| Java 25 | Java 17 |
| MySQL 8 | MySQL 7 |

---

# What Happens?
Alice deploys the application.
Result
❌ Application Fails
Now Alice informs Bob.
> "The application is not working in QA."

Bob replies
> "But it works perfectly on my machine."
This is one of the most common conversations in software companies.

---

# Another Scenario

Now another developer joins the project.
His name is **Charlie**.
Charlie has the following setup.

```
Operating System : macOS
Java Version : Java 21
Database : MySQL 7
Build Tool : Different Version
```

Bob pushes the project to GitHub.
Charlie clones the project.
```
Bob

↓

Push Code to GitHub

↓

Charlie

↓

Clone Repository

↓

Run Project
```

Result

❌ Application Fails

---

# Why Did It Fail?
The application failed because Charlie's environment is different.
Differences include:
* Operating System
* Java Version
* MySQL Version
* Dependency Versions
* Environment Variables
* Configuration Files
These differences create compatibility issues.

---

# How Developers Usually Fix It

Bob starts helping Charlie.
Typical conversation:

```
Bob

↓

Upgrade Java

↓

Update MySQL

↓

Install Correct Dependencies

↓

Change Configuration

↓

Run Again
```

Finally,

after upgrading and downgrading multiple software versions,
the application starts working.

---

# Problems Without Docker
Without Docker, developers face several issues.
## Environment Mismatch
Different operating systems.
Example

```
Windows

Linux

macOS
```

---

## Version Mismatch

Example
```
Developer
Java 25
↓
QA
Java 17
```

---

## Dependency Mismatch

Different dependency versions.
Example
```
Spring Boot Version
Hibernate Version
Maven Version
Gradle Version
```

---

## Configuration Mismatch
Example
```
properties
application.properties
Database URL
Username
Password
Profiles
Environment Variables
```

---

## Deployment Issues
Application works locally,
but fails on
* QA
* UAT
* Production

---

# Famous Software Industry Statement

You may have heard this many times.

> **"It works on my machine."**
This happens because every developer has a different environment.

---

# Traditional Solution

Before Docker,
teams used to create heavy documentation.
Example

```text
README.md
Installation Guide
Setup Document
Environment Variables
Java Version
Database Setup
Manual Configuration
```

Every new developer had to follow all these steps manually.

---

# Why Traditional Solution Is Not Good?
Problems
* Time consuming
* Manual setup
* Human errors
* Version mismatch
* Difficult maintenance
* Difficult onboarding
Even after following all the documentation,
there is no guarantee the application will work.

---

# Docker Solves This Problem

Instead of sharing
* Source Code
* Installation Guide
* Environment Setup
* Configuration
Docker packages everything together.
Everything required to run the application is bundled into one unit.
That unit is called a **Docker Image**.

---

# What Gets Packaged?

Docker packages:

```
Application Code
+
Java Runtime
+
Libraries
+
Dependencies
+
Operating System Packages
+
Configuration Files
+
Environment Settings
```

↓

Everything becomes one Docker Image.

---

# Advantages
Now developers only share the Docker Image.
Other developers don't need to install everything manually.
They simply run the image.
Benefits
* Same environment everywhere
* No version mismatch
* Easy deployment
* Easy onboarding
* Consistent execution
* Faster development

---

# Chapter 2 — What is Docker?
Now we understand the problem.
Let's understand the solution.

---
# Definition
Docker is a **Containerization Platform**.
It packages an application along with everything required to run it.
This package is called a **Docker Image**.
The image runs inside a **Docker Container**.

---

# Simple Definition

Docker is a tool that allows developers to package an application and its complete runtime environment into a single unit.

---

# What Does Docker Package?
Docker Image contains

```
Application Code
Java Runtime
Libraries
Dependencies
Operating System Packages
Configuration Files
Environment Variables
```

Everything required by the application is included inside the image.

---

# Real-Life Example

Consider a builder constructing multiple buildings.

The builder first creates a **Blueprint**.

```
Blueprint
↓
Building 1
Building 2
Building 3
```

The blueprint acts as a template.
Multiple buildings can be constructed from the same blueprint.

---

# Java Example
A Java Class is also a template.
Example
```java
class Building {

}
```

Objects are created from the class.

```java
Building b1 = new Building();

Building b2 = new Building();

Building b3 = new Building();
```

One class

↓

Multiple objects.

---

# Docker Uses the Same Concept

A Docker Image is like a Java Class.
A Docker Container is like a Java Object.

```text
Docker Image

↓

Container 1

Container 2

Container 3
```

One Docker Image can create multiple Containers.

---

# Image vs Container
## Docker Image
A Docker Image is a template.
Characteristics
* Read-only
* Immutable
* Contains application and dependencies
* Used to create containers

---

## Docker Container
A Docker Container is a running instance of an image.
Characteristics
* Executable
* Running Application
* Can Start
* Can Stop
* Can Restart
* Can Delete

---

# Practical Flow

```text
Developer

↓

Write Spring Boot Application

↓

Create Docker Image

↓

Run Docker Container

↓

Application Starts Successfully
```

---

# How Docker Solves the Problem

Earlier,

Bob shared only source code.

Now,

Bob creates a Docker Image.

```text
Bob

↓

Create Docker Image

↓

Share Image

↓

Charlie

↓

Run Docker Container

↓

Application Works
```

Charlie doesn't care about

* Java Version
* MySQL Version
* Operating System

because the Docker Image already contains everything required.

---

# Chapter 3 — Docker Architecture (Introduction)
To use Docker,
developers interact with Docker using two interfaces.
## Docker CLI
CLI stands for **Command Line Interface**.
This is the recommended way.
Example

```bash
docker images

docker ps

docker run

docker pull
```

---

## Docker Desktop
Docker Desktop provides a graphical user interface.
Useful for beginners.
However,
in production environments,
developers mostly use **Docker CLI** because cloud servers generally don't have a graphical interface.

---

# Architecture Overview

```text
                Developer
                    │
         ┌──────────┴──────────┐
         │                     │
   Docker CLI          Docker Desktop
         │
         ▼
     Docker Engine
         │
         ▼
   Docker Images
         │
         ▼
 Docker Containers
```

> **Note:** In the next part, we'll continue with the remaining Docker Architecture components (Docker Daemon, Docker Engine, Docker Hub, Images, Containers) and then move into Docker installation and the first practical.

---

# 📝 Interview Summary

By completing this chapter, you should be able to answer:
### Q1. Why was Docker created?
Docker was created to eliminate environment mismatch problems by packaging the application and all its dependencies into a Docker Image that runs consistently on any machine.

---

### Q2. What problems does Docker solve?
* Environment mismatch
* Version mismatch
* Dependency mismatch
* Configuration mismatch
* Deployment issues

---

### Q3. What is a Docker Image?
A Docker Image is a read-only template that contains the application code, runtime, libraries, dependencies, and configuration required to run an application.

---

### Q4. What is a Docker Container?
A Docker Container is the running instance of a Docker Image.

---

