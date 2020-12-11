---
description: Introducing key concepts for Docker Engine swarm mode
keywords: docker, container, cluster, swarm mode
title: Swarm mode key concepts
---

This topic introduces some of the concepts unique to the cluster management and
orchestration features of Docker Engine 1.12.

## What is a swarm?

The cluster management and orchestration features embedded in the Docker Engine
are built using [swarmkit](https://github.com/docker/swarmkit/). <span class='definition'>Swarmkit</span> is a
separate project which implements Docker's orchestration layer and is used
directly within Docker.

A <span class='definition'>swarm</span> consists of multiple Docker hosts which run in **swarm mode** and act as
managers (to manage membership and delegation) and workers (which run
[swarm services](#services-and-tasks)). A given Docker host can
be a manager, a worker, or perform both roles. When you create a <span class='definition'>service</span>, you
define its optimal state (number of replicas, network and storage resources
available to it, ports the service exposes to the outside world, and more).
Docker works to maintain that desired state. For instance, if a worker node
becomes unavailable, Docker schedules that node's tasks on other nodes. A <span class='definition'>_task_</span>
is a running container which is part of a swarm service and managed by a swarm
manager, as opposed to a standalone container.

One of the <span class='important'>key advantages of swarm services over standalone containers</span> is that
you can modify a service's configuration, including the networks and volumes it
is connected to, without the need to manually restart the service. Docker will
update the configuration, stop the service tasks with the out of date
configuration, and create new ones matching the desired configuration.

When Docker is running in swarm mode, you can still run standalone containers
on any of the Docker hosts participating in the swarm, as well as swarm
services. A <span class='important'>key difference between standalone containers and swarm services</span> is
that only swarm managers can manage a swarm, while standalone containers can be
started on any daemon. <span class='definition'>Docker daemons</span> can participate in a swarm as managers,
workers, or both.

In the same way that you can use [Docker Compose](../../compose/index.md) to define and run
containers, you can define and run [Swarm service](services.md) stacks.

Keep reading for details about concepts relating to Docker swarm services,
including nodes, services, tasks, and load balancing.

## Nodes

A <span class='definition'>**node**</span> is an instance of the Docker engine participating in the swarm. You can also think of this as a <span class='definition'>Docker node</span>. You can run one or more nodes on a single physical computer or cloud server, but production swarm deployments typically include Docker nodes distributed across multiple physical and cloud machines.

To <span class='important'>deploy your application</span> to a swarm, you submit a <span class='definition'>service definition</span> to a
**manager node**. The <span class='definition'>manager node</span> dispatches units of work called
[tasks](#services-and-tasks) to worker nodes.

Manager nodes also perform the <span class='definition'>orchestration</span> and <span class='definition'>cluster management</span> functions
required to maintain the desired state of the swarm. Manager nodes elect a
<span class='definition'>single leader</span> to conduct orchestration tasks.

<span class='definition'>**Worker nodes**</span> receive and execute tasks dispatched from manager nodes.
By default manager nodes also run services as worker nodes, but you can
<span class='important'>configure them to run manager tasks exclusively and be manager-only
nodes</span>. An <span class='definition'>agent</span> runs on each worker node and reports on the tasks assigned to
it. The worker node notifies the manager node of the <span class='important'>current state of its
assigned tasks</span> so that the manager can maintain the desired state of each
worker.

## Services and tasks

A <span class='definition'>**service**</span> is the definition of the tasks to execute on the manager or worker nodes. It
is the central structure of the swarm system and the primary root of user
interaction with the swarm.

When you create a service, you specify <span class='important'>which container image to use</span> and which
commands to execute inside running containers.

In the <span class='definition'>**replicated services** model</span>, the swarm manager distributes a specific
number of replica tasks among the nodes based upon the scale you set in the
desired state.

For <span class='definition'>**global services**</span>, the swarm runs one task for the service on every
available node in the cluster.

A <span class='definition'>**task**</span> carries a <span class='bold'>Docker container</span> and the <span class='bold'>commands</span> to run inside the
container. It is the <span class='important'>atomic scheduling unit of swarm</span>. Manager nodes assign tasks
to worker nodes according to the <span class='definition'>number of replicas</span> set in the service scale.
Once a task is assigned to a node, it <span class='important'>cannot move</span> to another node. It can only
run on the assigned node or fail.

## Load balancing

The swarm manager uses <span class='definition'>**ingress load balancing**</span> to <span class='important'>expose the services</span> you
want to make available externally to the swarm. The swarm manager can
automatically assign the service a <span class='definition'>**PublishedPort**</span> or you can configure a
PublishedPort for the service. You can specify any unused port. If you do not
specify a port, the swarm manager assigns the service a port in the 30000-32767
range.

External components, such as <span class='definition'>cloud load balancers</span>, can access the service on the
PublishedPort of any node in the cluster whether or not the node is currently
running the task for the service.  <span class='important'>All nodes in the swarm route ingress
connections to a running task instance</span>.

Swarm mode has an <span class='important'>internal DNS component</span> that automatically assigns each service
in the swarm a DNS entry. The swarm manager uses <span class='definition'>**internal load balancing**</span> to
distribute requests among services within the cluster based upon the DNS name of
the service.

## What's next?

* Read the [Swarm mode overview](index.md).
* Get started with the [Swarm mode tutorial](swarm-tutorial/index.md).
