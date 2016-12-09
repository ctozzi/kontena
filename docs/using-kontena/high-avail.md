---
title: Summary
---

# Setting Up a High Availability Kontena Master

A high availability Kontena Master will distribute its Services across different Nodes. This helps to assure that an application remains available in the event that some Nodes go offline.

## Setting Up and Configuring the Master

To set up a high availability Master, first install a Master by following the [installation instructions](../getting-started/installing/README.md) for the platform you are using. Once the Master is installed, start it.

## Setting High Availability mode on the Master

After the Master is running, you can configure high availability by defining a [Deploy Strategy](deploy.md) within its Service definitions as follows:

```
deploy:
  strategy: ha
```

Restart the Master for the change to take effect.
