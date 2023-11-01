---
title: How does Spark Processing Start ?
tags:  [distributed processing, spark, application master, driver, executor]
layout: post
description: What all processes run when a jar is submitted, how is the driver created, who manages whom.
comments: true
---


- What happens when a jar is submitted through a Spark Client ?
- How does a spark job gets triggered ?

## Let's deep dive !!


1. A client program (spark-submit) submits the application, including the necessary specifications to run the application-specific __ApplicationMaster__ (for Spark Applications - SparkMaster).

2. ResourceManager gets responsibility for the allocation of a necessary container in which ApplicationMaster(SparkMaster) will be started. Then ResourceManager starts the ApplicationMaster(SparkMaster).

3. SparkMaster is created at the same time as the Driver on the same node(in case of cluster mode) when the user submits the spark application using spark-submit. The Driver informs the Application Master about the executor's requirements for the application and the Application Master negotiates the resources with the Resource Manager to host these executors.

4. ApplicationMaster registers itself in ResourceManager. Registration allows the Customer program (spark-submit) to request specific information from ResourceManager that allows it to directly interact with its ApplicationMaster.

5. ApplicationMaster asks for suitable containers from ResourceManager for the application to run. After successfully receiving the containers, ApplicationMaster launches them, providing NodeManager(s) their configurations.

6. Inside the containers, it runs the user application code. The NodeManager(s) then provides the information (execution phase, status) for ApplicationMaster.

7. During the runtime of the user application, the client interacts with ApplicationMaster to obtain the application status.

8. When the application completes and all necessary work is completed, ApplicationMaster deregisters from ResourceManager and terminates, releasing the container for other purposes.

9. Once the driver is up it runs the main program of the user application code. The first thing it does is create a SparkContext. So let us understand that in detail.