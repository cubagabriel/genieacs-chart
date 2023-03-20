# GenieACS

[GenieACS](https://genieacs.com/) is an open source TR-069 remote management solution with advanced device provisioning capabilities

For more detailed documentation please visit [here](https://docs.minio.io/)

Introduction
------------

This chart installs GenieACS on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

Prerequisites
--------------------

1. An ingress controller running in your cluster (e.g. ingress-nginx).
2. An external LoadBalancer or metallb as L4 LoadBalancer controller.
3. At least 2 available LoadBalancer IP addresses
4. Mongodb community operator, which will create the mongo database for persistance
5. Optionally a genieACS tester running outside the cluster.

Installation
-----------------

Fill the form with the appropiate values and click on install.

After the installation you will see 4 deployments and 4 services running.

In order to test the installation, perform the following:

1. Go to the URL you set as the UI, check that the page loads and bootstraps the application succesfully
2. Launch the genieACS tester. You should see the device in the list in the UI
3. 

