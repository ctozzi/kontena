---
title: Technology
toc_order: 3
---

![Technology Stack](https://github.com/ctozzi/kontena/blob/master/docs/core-concepts/Technology%20Stack.png)

# Technology

Kontena is built using the following components:

## Docker Engine

> The Linux container engine

Docker Engine creates and runs containers.

## Weave

> An overlay network for Docker

Weave is used as a default overlay network for Nodes. Weave provides a common network fabric that works everywhere in the same way. Weave has some really nice features that are hard to implement, such as transparent network encryption.

## Etcd

> A highly-available key-value store for shared configuration and service discovery.

Etcd is used as a distributed key-value storage in Nodes. Each Kontena Grid has one internal etcd cluster that Node agents can use.

## Ruby

> Ruby is a dynamic, open source programming language with a focus on simplicity and productivity.

Ruby is our weapon of choice when it comes to server-side coding. Both master and agent daemons are written using Ruby. Ruby is really flexible and provides a large number of libraries to streamline programming.

The rubygems that we rely on include:

* roda
* puma
* mongoid
* mutations
* docker-api
* etcd
* celluloid
* rspec

## MongoDB

> MongoDB is an open-source document database designed for ease of development and scaling.

Kontena uses MongoDB to provide persistent storage for the Master daemon. We chose to use MongoDB because of its flexibility, tooling and relatively simple scaling.

## cAdvisor

> cAdvisor (Container Advisor) is a container monitoring tool.

cAdvisor provides container users with an understanding of the resource usage and performance characteristics of their running containers.
