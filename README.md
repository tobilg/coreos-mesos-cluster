# Mesos cluster on CoreOS via Vagrant

This repo provides a Vagrantfile as well as a `cloud_config` for a three-node CoreOS cluster running the latest stable versions of Mesos and Marathon using the VirtualBox software hypervisor. it was forked from [coreos/coreos-vagrant](https://github.com/coreos/coreos-vagrant) and configured to run Mesos cluster components.

## Components

The cluster runs the following components on each node:

* Apache ZooKeeper 3.4.6
* Mesos 0.27.0 (Masters / Slaves)
* Marathon 0.15.0

## General setup

1) Install dependencies

* [VirtualBox][virtualbox] 4.3.10 or greater.
* [Vagrant][vagrant] 1.6 or greater.

2) Clone this project and get it running!

```
git clone https://github.com/tobilg/coreos-mesos-cluster.git
cd coreos-mesos-cluster
```

3) Startup, status and SSH

The VirtualBox provider is the default Vagrant provider. Use this if you are unsure.

**Startup**
```
vagrant up
```

**Status check**
```
vagrant status
```

will show something like

```
Current machine states:

core-01                   running (virtualbox)
core-02                   running (virtualbox)
core-03                   running (virtualbox)
```

**Please note:**
It can take a while until all units are up and running, because each node will download four Docker images:
* Mesos Master
* Mesos Slave
* ZooKeeper
* Marathon

You can check via `docker ps` or `systemctl status <serviceName>` if the units/services are up and running. Depending on your internet connection, this can take up to 30 minutes (for the first launch).

**SSH (to one host)**
```
vagrant ssh core-01 -- -A 
```

For additional docs please have a look at the [original docs](https://github.com/coreos/coreos-vagrant)

4) Check Mesos and Marathon functionality

The Mesos Masters/Slaves will be launched on every cluster node, as well as Marathon. Check the [Mesos Master UI](http://172.17.8.101:5050) and the [Marathon UI](http://172.17.8.101:8080).

[virtualbox]: https://www.virtualbox.org/
[vagrant]: https://www.vagrantup.com/downloads.html
