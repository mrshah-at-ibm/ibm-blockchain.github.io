---
layout: default
title:  1. Prepare & Setup
permalink: "/setup/"
category: tutorial
---

# Prepare & Setup

Before deploying the IBM Blockchain Developer Environment, you must first prepare a basic cluster on the IBM Container Service.

## Prepare required CLIs and plugins

First, we will download and add the CLIs and plugins that we need to interact with the IBM Container Service.

### 1. Download and install kubectl CLI

https://kubernetes.io/docs/tasks/kubectl/install/

### 2. Download and install the Bluemix CLI

http://clis.ng.bluemix.net/ui/home.html

### 3. Add the bluemix plugins repo

```
bx plugin repo-add bluemix https://plugins.ng.bluemix.net
```

### 4. Add the container service plugin

```
bx plugin install container-service -r bluemix
```

## Setup a cluster

Now, we will use those CLIs and plugins to create a cluster on the IBM Container Service.  Use these steps to setup a cluster named ___blockchain___ on IBM Container Service.

### 5. Point Bluemix CLI to production API

```bash
bx api api.ng.bluemix.net
```

### 6. Login to bluemix

```bash
bx login
```

If your id is federated in an SSO, you will have to run the following command to login:
```bash
bx login -sso
```

### 7. Create a cluster on IBM Container Service

This will create a __free cluster__ named _blockchain_ on the IBM Container Service.
```bash
bx cs cluster-create --name blockchain
```

### 8. Wait for the cluster to be ready

Issue the following command to ascertain the status of your cluster:
```bash
bx cs clusters
```

The process goes through the following lifecycle - ``requesting`` --> ``pending`` --> ``deploying`` --> ``normal``.  Initially you will see something similar to the following:
```
Name         ID                                 State       Created                    Workers
blockchain   7fb45431d9a54d2293bae421988b0080   deploying   2017-05-09T14:55:09+0000   0
```

Wait for the State to change to _normal_. Note that this can take upwards of 15-30 minutes. If it takes more than 30 minutes, there is an inner issue on the IBM Container Service.

You should see the following output when the cluster is ready:
```
$ bx cs clusters
Listing clusters...
OK
Name         ID                                 State    Created                    Workers
blockchain   0783c15e421749a59e2f5b7efdd351d1   normal   2017-05-09T16:13:11+0000   1

```

Use the following syntax to inspect on the status of the workers:
Command:
```bash
bx cs workers <cluster-name>
```

For example:
```bash
bx cs workers blockchain
```

The expected response is as follows:
```
$ bx cs workers blockchain
Listing cluster workers...
OK
ID                                                 Public IP       Private IP       Machine Type   State    Status
kube-dal10-pa0783c15e421749a59e2f5b7efdd351d1-w1   169.48.140.48   10.176.190.176   free           normal   Ready
```

### 9. Configure kubectl to use the cluster

Issue the following command to download the configuration for your cluster:
```bash
bx cs cluster-config blockchain
```

Expected output:

```
Downloading cluster config for blockchain
OK
The configuration for blockchain was downloaded successfully. Export environment variables to start using Kubernetes.

export KUBECONFIG=/home/*****/.bluemix/plugins/container-service/clusters/blockchain/kube-config-prod-dal10-blockchain.yml
```

### 10. Configure kubectl to use the cluster

Use the export command printed as output in [step 5](./create-cluster.md#5) to point your kubectl cli to the cluster.

_Note_: If you are on windows, you should use `set` in place of `export`. If the scripts run in a different terminal or git bash, you should start git-bash and use the export command.

* * *

## Congratulations!
You have successfully created the blockchain cluster on IBM Container Service.  Next, you will deploy the Developer Environment.  Most users will want to follow the **Simple Install** instructions (Advanced and Reference are there for those who want to e.g. only set up part of the environment).

ADD BUTTON LINKING TO SIMPLE INSTALL INSTRUCTIONS