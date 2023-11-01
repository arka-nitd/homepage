---
title: Spark on Yarn
tags:  [distributed processing, spark, yarn]
layout: post
description: Apache Spark on Yarn
comments: true
---


What it is like to run Apache Spark on a  **Yarn Cluster** ?
How does it increase the efficiency of the nodes and reduces the cost ?
What is Yarn for that matter ?

Let's find out through some visuals and pointers !

### Important Concepts and their relations
<img src="https://snipboard.io/gkaB82.jpg" alt="drawing" width="600"/>

### How are Resource Manager and Node Manager related ?

In cluster-mode, the resource allocation has the structure shown below.

<img src="https://snipboard.io/aMeilB.jpg" alt="drawing" width="400"/>

### Concepts in bits !

#### Resource Manager
ResourceManager is the ultimate authority that decides the allocation of resources between all applications in the system. It has minions that run on all nodes of the cluster called NodeManager. Also, ResourceManager has a plug-in component scheduler that is responsible for allocating resources for various running applications.
The yarn container which runs the Spark Driver is also called Spark AM (Application Master)

#### Yarn Container
Containers are computing units, a kind of wrappers for node resources to perform tasks of a user application. They are the main computing units that are managed by YARN. Containers have their own parameters that can be configured on-demand (e.g. ram, CPU, etc.).

#### Node Manager
Containers on each node are controlled by NodeManager daemon

#### Application Master
When launching a new application on a cluster, ResourceManager allocates one container for ApplicationMaster. ApplicationMaster for each application is a framework-specific entity that is tasked with negotiating resources with ResourceManager and working with NodeManager(s) to perform and monitor component tasks
ApplicationMaster will be responsible for the entire lifecycle of the distributed application.

#### Language Agnostic
ResourceManager, NodeManager, and the container do not care about the type of application or task. All application framework code is simply transferred to the ApplicationMaster so that any distributed framework can be supported by YARN — as long as someone implements a suitable ApplicationMaster for it.

<img src="https://snipboard.io/1lQXPE.jpg" alt="drawing" width="400"/>




