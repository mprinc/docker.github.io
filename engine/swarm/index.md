---
description: Docker Engine swarm mode overview
keywords: docker, container, cluster, swarm
title: Swarm mode overview
---

To use Docker in swarm mode, install Docker. See
[installation instructions](../../get-docker.md) for all operating systems and platforms.

Current versions of Docker include <span class='definition'>*swarm mode*</span> for natively managing a cluster
of Docker Engines called a *swarm*. Use the Docker CLI to create a swarm, deploy
application services to a swarm, and manage swarm behavior.

## Feature highlights

* **Cluster management integrated with Docker Engine:** Use the Docker Engine
CLI to create a swarm of Docker Engines where you can deploy application
services. <span class='important'>You don't need additional orchestration software to create or manage
a swarm</span>.

* **Decentralized design:** Instead of handling differentiation between node
roles <span class='important'>at deployment time</span>, the Docker Engine handles any specialization <span class='important'>at
runtime</span>. You can deploy both kinds of nodes, managers and workers, using the
Docker Engine. <span class='important'>This means you can build an entire swarm from a single disk
image</span>.

* **Declarative service model:** Docker Engine uses a <span class='important'>declarative</span> approach to
let you define the desired state of the various services in your application
stack. For example, you might describe an application comprised of a web front
end service with message queueing services and a database backend.

* **Scaling:** For each service, you can declare the <span class='important'>number of tasks</span> you want to
run. When you scale up or down, the swarm manager automatically adapts by
adding or removing tasks to maintain the desired state.

* **Desired state reconciliation:** The swarm manager node constantly monitors
the cluster state and reconciles any differences between the actual state and your
expressed desired state. For example, if you set up a service to run 10
<span class='definition'>replicas</span> of a container, and a worker machine hosting two of those replicas
<span class='important'>crashes</span>, the manager creates two new replicas to replace the replicas that
crashed. The swarm manager assigns the new replicas to workers that are
running and available.

* **Multi-host networking:** You can specify an <span class='definition'>overlay network</span> for your
services. The swarm manager automatically assigns addresses to the containers
on the overlay network when it initializes or updates the application.

* **Service discovery:** Swarm manager nodes assign each service in the swarm a
<span class='important'>unique DNS name</span> and <span class='important'>load balances running containers</span>. You can <span class='definition'>query</span> every
container running in the swarm through a DNS server embedded in the swarm.

* **Load balancing:** You can expose the ports for services to an
<span class='definition'>external load balancer</span>. Internally, the swarm lets you specify how to distribute
service containers between nodes.

* **Secure by default:** Each node in the swarm enforces <span class='definition'>TLS mutual
authentication and encryption</span> to secure communications between itself and all
other nodes. You have the option to use self-signed root <span class='definition'>certificates</span> or
certificates from a custom root CA.

* **Rolling updates:** At rollout time you can apply <span class='definition'>service updates</span> to nodes
<span class='important'>incrementally</span>. The swarm manager lets you control the <span class='important'>delay</span> between service
deployment to different sets of nodes. If anything goes wrong, you can
<span class='important'>roll back</span> to a previous version of the service.

## What's next?

### Swarm mode key concepts and tutorial

* Learn swarm mode [key concepts](key-concepts.md).

* Get started with the [Swarm mode tutorial](swarm-tutorial/index.md).

### Swarm mode CLI commands

Explore swarm mode CLI commands

* [swarm init](../reference/commandline/swarm_init.md)
* [swarm join](../reference/commandline/swarm_join.md)
* [service create](../reference/commandline/service_create.md)
* [service inspect](../reference/commandline/service_inspect.md)
* [service ls](../reference/commandline/service_ls.md)
* [service rm](../reference/commandline/service_rm.md)
* [service scale](../reference/commandline/service_scale.md)
* [service ps](../reference/commandline/service_ps.md)
* [service update](../reference/commandline/service_update.md)
