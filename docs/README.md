---
title: What is Kontena?
toc_order: 1
---

# What is Kontena?

[Kontena](http://www.kontena.io) is an open source project for orchestrating and running containerized workloads on a cluster using multiple containers. The Kontena system is comprised of a number of **Kontena Nodes** (meaning servers or virtual machines that run containerized workloads) and a **Kontena Master** (which controls and monitors the Nodes).

With Kontena, you can construct your application using the **Kontena Service** definition. A Service definition describes the container images, networking, scaling and stateful/stateless attributes associated with your application. Services may be linked together to create the desired architecture. Each service is automatically assigned an internal DNS address, which can be used inside your application for communications between different Services.

Kontena's key features include:
* Scheduler with affinity filtering
* Built-in private Docker image registry
* Remote VPN access for workload services
* Ready-made load-balancing service
* Log and statistics aggregation with streaming
* Access control and roles for Kontena users

Kontena is administered via the Kontena command line interface, **Kontena CLI**. At the moment, there is no graphical UI for Kontena.

![Kontena Overview](https://github.com/ctozzi/kontena/blob/master/docs/core-concepts/System%20Overview.png?raw=true)

## Learn More

If you are new to Kontena, we recommend that you first read through the [quick start](getting-started/quick-start.md) guide.

This documentation is a work in progress. Any feedback and requests are welcome. If you feel like something is
missing, please [open an issue](https://github.com/kontena/kontena/issues) on GitHub.
