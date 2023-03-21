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
3. At least 2 available LoadBalancer IP addresses for CWMP and FS services
4. Mongodb community operator, which will create the mongo database for persistance
5. At least 1 storage provider (e.g. OpenEBS) and a default Storage Class.
6. Optionally a genieACS tester running outside the cluster.

Pre-installation
-----------------

You can install both **Mongodb community operator** (mandatory) and **OpenEBS** (optional) from the Marketplace with few changes to default values.

For **Mongodb community operator**, set `operator.watchNamespace: '*'` in YAML values.

For **OpenEBS**, in **NDM Sparse Disk Settings**, disable `Create a cStor Pool on Sparse Disks` checkbox.

Installation
-----------------

Just fill the form with the required values and click on **Install**.

After the installation you will see 4 deployments and 4 services running. 
UI and NBI will be exposed through an ingress, CWMP and FS through Load Balancer IP addresses.

In order to test the installation, perform the following:

1. Go to the URL you set as the UI, check that the page loads and bootstraps the application succesfully
2. Launch the genieACS tester with the following command from any external host that can reach CWMP Load Balancer IP: 
    ```bash
    docker run -d --name genieacs-sim --network host drumsergio/genieacs-sim ./genieacs-sim -u http://<CWMP Load Balancer IP>:7547
    ```
3. Go to the UI and click on the Devices tab. You should see the device status.
4. In the UI, go to the Admin tab -> Files -> New , and upload any file. Set the OUI, Product Class and Version according 
to the genieACS tester parameters (device tab). Click on **save**
5. From any external host that can reach the UI URL, execute the following curl command:
    ```bash
     curl -i 'http://<UI URL>/devices/<device ID>/tasks?timeout=9000&connection_request' -X POST --data '{"name": "download", "file": "test_file.sh"}'
    ```
6. Check that there are no errors in the Device section