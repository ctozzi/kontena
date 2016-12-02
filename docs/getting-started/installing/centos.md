---
title: CentOS
---

# Running Kontena on CentOS (and Red Hat Enterprise Linux)

- [Prerequisites](centos#prerequisites)
- [Installing Kontena Master](centos#installing-kontena-master)
- [Installing Kontena Nodes](centos#installing-kontena-nodes)

## Prerequisites

- [Kontena CLI](cli)

## Installing Docker Engine

Kontena requires [Docker Engine](https://docs.docker.com/engine/) to be installed on every host (Master and Nodes).

Docker Engine can be [installed on CentOS](https://docs.docker.com/engine/installation/linux/centos/) with the following commands:

$ sudo yum update
$ sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
$ [dockerrepo]
$ name=Docker Repository
$ baseurl=https://yum.dockerproject.org/repo/main/centos/7/
$ enabled=1
$ gpgcheck=1
$ gpgkey=https://yum.dockerproject.org/gpg
$ EOF
$ sudo yum install docker-engine
$ sudo systemctl enable docker.service

```

## Installing Kontena Master

Kontena Master is an orchestrator component that manages Kontena Grids/Nodes. Installing Kontena Master to Ubuntu can be accomplished by installing the kontena-server package using the appropriate commmands for your version of Ubuntu:


#### Ubuntu Xenial (16.04)

```
$ wget -qO - https://bintray.com/user/downloadSubjectPublicKey?username=bintray | sudo apt-key add -
$ echo "deb http://dl.bintray.com/kontena/ubuntu xenial main" | sudo tee -a /etc/apt/sources.list
$ sudo apt-get update
$ sudo apt-get install kontena-server
```

#### Ubuntu Trusty (14.04)

```
$ wget -qO - https://bintray.com/user/downloadSubjectPublicKey?username=bintray | sudo apt-key add -
$ echo "deb http://dl.bintray.com/kontena/ubuntu trusty main" | sudo tee -a /etc/apt/sources.list
$ sudo apt-get update
$ sudo apt-get install kontena-server
```

At the end of the installation the process master will ask for a initial admin code for the Master. This is used to authenticate the initial admin connection of Kontena CLI in order to configure the Master properly. The code can be any random string.

If using automation the value can be overwritten in the file `/etc/default/kontena-server-api` on Ubuntu Trusty or `/etc/kontena-server.env` on Ubuntu Xenial.

### Setup SSL Certificate


#### Ubuntu Xenial (16.04)

```
$ sudo vim /etc/kontena-server.env

# HAProxy SSL certificate
SSL_CERT=/path/to/certificate.pem

$ sudo systemctl restart kontena-server-haproxy
```

#### Ubuntu Trusty (14.04)

```
$ sudo stop kontena-server-haproxy
$ sudo vim /etc/default/kontena-server-haproxy

# HAProxy SSL certificate
SSL_CERT=/path/to/certificate.pem

$ sudo start kontena-server-haproxy
```


### Login to Kontena Master


After Kontena Master has started you can authenticate as the Kontena Master internal administrator using the `INITIAL_ADMIN_CODE` you provided. Refer to [authetication](../../using-kontena/authentication.md) for instructions on configuring [Kontena Cloud](https://cloud.kontena.io) as the authentication provider.

```
kontena master login --name some-name --code <admin code> https://master_ip:8443
```

## Installing Kontena Nodes

Before you can start provisioning Nodes you must first switch the CLI scope to a Grid. A Grid can be thought as a cluster of Nodes that can have members from multiple clouds and/or regions.

Switch to an existing Grid using the following command:

```
$ kontena grid use <grid_name>
```

Or create a new Grid using the command:

```
$ kontena grid create test-grid
```

Remember to grab the token for the Grid, you'll need it when setting up Node(s).

```
$ kontena grid show --token test-grid
```

Now you can go ahead and install the kontena-agent Ubuntu package using the appropriate commands for your Ubuntu version:

#### Ubuntu Xenial (16.04)

```
$ wget -qO - https://bintray.com/user/downloadSubjectPublicKey?username=bintray | sudo apt-key add -
$ echo "deb http://dl.bintray.com/kontena/ubuntu xenial main" | sudo tee -a /etc/apt/sources.list
$ sudo apt-get update
$ sudo apt-get install kontena-agent
```

#### Ubuntu Trusty (14.04)

```
$ wget -qO - https://bintray.com/user/downloadSubjectPublicKey?username=bintray | sudo apt-key add -
$ echo "deb http://dl.bintray.com/kontena/ubuntu trusty main" | sudo tee -a /etc/apt/sources.list
$ sudo apt-get update
$ sudo apt-get install kontena-agent
```

At the end of the installation the process agent will ask for a couple of configuration parameters:

* The address of the Kontena master. **Note:** You must use WebSocket protocol: ws or wss for secured connections
* The Grid token from the Kontena master

After installing all the agents, you can verify that they have joined a Grid:

```
$ kontena node list
```
