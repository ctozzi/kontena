---
title: Health checks
---

# Health checks

Kontena comes with a mechanism to define a custom health check for each service. By default Kontena will only monitor the existence of service instances (containers) and will re-deploy or reschedule a service in the case of lost instances.

Sometimes the container will exist but the application running within the container becomes unresponsive. In such cases, a custom application-level health check will detect the unresponsive application.

## Configuring a custom health check

Configuring a custom health check is done by adding the configuration in the kontena.yml file:

```
version: '2'
services:
  web:
    image: nginx
    stateful: false
    health_check:
      protocol: http
      port: 80
      interval: 20
      uri: /health
      initial_delay: 10
      timeout: 2

  mysql:
    image: mysql
    stateful: true
    deploy:
      strategy: ha
      wait_for_port: 3306
    environment:
      - MYSQL_ALLOW_EMPTY_PASSWORD=true
    health_check:
      protocol: tcp
      port: 3306
      interval: 10
      initial_delay: 10
      timeout: 2
```
Options:
* `protocol`: protocol to use, either `http` or `tcp`
* `port`: port to use for the check. This is the port the application is using within the container.
* `interval`: how often the health check is performed. Defined in seconds.
* `uri`: The relative URI to use for the health check. Only used in http mode.
* `initial_delay`: The time to wait until the first check is performed after a service instance is created. Allows some time for the application to start up.
* `timeout`: How long Kontena will wait for a response. If no response is received within this timeframe the instance is considered unhealthy.

**Note** When performing tcp mode check, Kontena will only try to open a tcp socket connection to the specified port. If the connection is successful the instance is considered healthy.


## Loadbalancer

Configuring a custom healthcheck on a service also ensures that the same health check is used by the Kontena loadbalancer, if the service is attached to one. When Kontena loadbalancer detects unhealthy instances, it will remove them from the routing. In practice this means that unhealthy instances will not get any traffic through the loadbalancer until they report being healthy again.

## Using the health status

Currently the health check status is used only to indicate a service health for the user. We are planning to use this information as well for rescheduling services so that any unhealthy instance will be rescheduled or recreated. As explained above, the same configuration is also used by Kontena loadbalancer to decide whether or not an instance should receive traffic.
