---
title: Summary
toc_order: 1
---

# Summary of Using Kontena

Kontena offers a range of functionality for configuring and managing containerized workloads. When using Kontena, you can do the following:

* Configure [Load Balancing](loadbalancer.md) and specify [Deploy strategies](deploy.md) in order to set priorities within your application.
* Set up a [high availablity Kontena Master](high-avail.md).
* Set up a cluster of Kontena Nodes by establishing a [Grid](grids.md).
* Create a private image registry for hosting container images using Kontenta's built-in [Image Registry](image-registry.md).
* Set up [Services](services.md), which are composed of multiple containers based on the same image file. A Service definition lets you define the parameters for one of the microservices that is used to compose your application. Kontena allows you to reuse Services via the [Stacks](stacks.md) feature.
* Configure access control for Kontena administrators and users via the [Users](users.md) interface.
* Configure [VPN Access](vpn-access.md) so that developers and admins can access internal services, which are not exposed to the public Internet by default.
* Manage encryption [Certificates](certificates.md) for securing communications. In Kontena, encryption management is powered by Let's Encrypt.
* Collect [Statistics](stats.md) in order to monitor Kontena Services.
* Configure [Health Checks](health-check.md) to help monitor your application and automate the resolution of incidents such as the downtime of a container.
* Manage the way Kontena handles logins by configuring [Authentication](authentication.md).
* Configure [Kontena Vault](vault.md) in order to store passwords or access tokens that your application requires to access APIs or databases.
* If desired, disable [Telemetry](telemetry.md), the anonymous usage tracking that Kontena performs to help the project's open source developers.
