# How to Install DIVOC

## Assumptions&#x20;

* Use a Debian-based Linux distribution (preferably Ubuntu)&#x20;
* Experience in running simple shell and bash commands

## Pre-requisites&#x20;

* Debian-based OS (Ubuntu)&#x20;
* sshpass&#x20;
* Ansible&#x20;
* GIT&#x20;
* kubectl&#x20;
* List of servers and ability to access them using key-based authentication&#x20;
* Server map to list servers against software&#x20;
* Access to the DIVOC installer repository&#x20;
* Access to the implementation-specific DIVOC code

## Suggested servers for HA setup&#x20;

The sizing and count of the servers can change based on the load requirements. However,  for a truly HA setup, the following are the minimum requirements:

### Postgres and etcd&#x20;

3 servers for HA setup: one master and 2 replicas. The etcd cluster can also be set up on the same servers.&#x20;

### Kubernetes&#x20;

6 servers: 3 for control plane (or master node can be relatively smaller sized instances) and 3 worker nodes (for deploying the application).

### Kafka and Zookeeper&#x20;

3 servers containing both Zookeeper and Kafka (Ideally Zookeeper and Kafka need to be installed on separate servers but we should be fine to install both on the same machine).

### Redis&#x20;

3 servers&#x20;

### Elasticsearch&#x20;

3 servers&#x20;

#### Docker-registry&#x20;

1 server

## Overview&#x20;

There are three scripts that need to be run to complete the DIVOC installation process:

1. Installing the prerequisites and setting various hardware clusters as detailed above.&#x20;
2. Building the pushing the docker images to the appropriate registry.&#x20;
3. Deploying code from the registry into Kubernetes cluster.

## Installation dependencies

1. Clone the repository available at [**https://github.com/egovernments/divoc-installer**](https://github.com/egovernments/divoc-installer).&#x20;
2. Create an inventory file from the sample inventory file located at [**https://github.com/egovernments/divoc-installer/blob/master/inventory.example.ini**](https://github.com/egovernments/divoc-installer/blob/master/inventory.example.ini).
3. Add the inventory details as per the comments present in the file.&#x20;
4. Run the install.sh present within the divoc-installer with the elevated privileges (we can also use nohup for running in the background):

{% hint style="info" %}
sudo sh install.sh -i \<path to inventory file>
{% endhint %}

* It will install the dependencies like python3, ansible, etc.&#x20;
* It will install the applications and configure them on the servers mentioned in the inventory file.

## Build Docker images&#x20;

* Run the build.sh file with elevated privileges.&#x20;

{% hint style="info" %}
&#x20;**** sudo sh build.sh -d \<IP Address of Docker Registry> -r \<GIT REPO URL>
{% endhint %}

* Default values for the Docker repository are from dockerhub.
* The Default value for the GIT repo is the master branch of the [**https://github.com/egovernments/DIVOC.git**](https://github.com/egovernments/DIVOC).

## **Install DIVOC application**

1. The sample default Kubernetes deployment files are available at **** [**https://github.com/egovernments/divoc-installer/tree/master/kube-deployment-config-example**](https://github.com/egovernments/divoc-installer/tree/master/kube-deployment-config-example)**.**
2. Make a copy of the folder and change the internal script files to have the following configurations. It is recommended that you maintain your own configuration in a separate Github repository so that you have version control and backup (you require only the example folder, not the full repository).

&#x20;     a. Within the divoc-installer director, open the divoc-config.yaml file present within the deployment configuration directory and make the following changes:    &#x20;

&#x20;           ****            - **** DB\_HOST&#x20;

&#x20;         \- DB\_USER&#x20;

&#x20;         \- DB\_PASS&#x20;

&#x20;         \- DB\_PORT&#x20;

&#x20;         \- KAFKA\_BOOTSTRAP\_SERVERS&#x20;

&#x20;         \- REDIS\_URL&#x20;

&#x20;         \- CLICKHOUSE\_URL&#x20;

&#x20;         \- AUTH\_PRIVATE\_KEY&#x20;

&#x20;         \- AUTH\_PUBLIC\_KEY&#x20;

&#x20;         \- CERTIFICATE\_NAMESPACE&#x20;

&#x20;         \- CERTIFICATE\_NAMESPACE\_V2&#x20;

&#x20;         \- CERTIFICATE\_CONTROLLER\_ID&#x20;

&#x20;         \- CERTIFICATE\_PUBKEY\_ID&#x20;

&#x20;         \- CERTIFICATE\_DID&#x20;

&#x20;         \- CERTIFICATE\_ISSUER&#x20;

&#x20;         \- CERTIFICATE\_BASE\_URL&#x20;

&#x20;         \- CERTIFICATE\_FEEDBACK\_BASE\_URL&#x20;

&#x20;         \- CERTIFICATE\_INFO\_BASE\_URL&#x20;

&#x20;         \- CERTIFICATE\_PUBLIC\_KEY&#x20;

&#x20;         \- CERTIFICATE\_PRIVATE\_KEY&#x20;

&#x20;         \- CITIZEN\_PORTAL\_URL

&#x20;     b. Modify registry-deployment.yaml to change the following:

&#x20;         \- connectionInfo\_password&#x20;

&#x20;         \- connectionInfo\_uri&#x20;

&#x20;         \- connectionInfo\_username&#x20;

&#x20;         \- elastic\_search\_enabled&#x20;

&#x20;         \- registry\_base\_apis\_enable&#x20;

&#x20;         \- taskExecutor\_index\_queueCapacity&#x20;

&#x20;         \- auditTaskExecutor\_queueCapacity&#x20;

&#x20;         \- Signature\_enabled&#x20;

&#x20;     c. Modify keycloak-deployment.yaml to add the following information:

&#x20;         \- DB\_ADDR&#x20;

&#x20;         \- DB\_DATABASE&#x20;

&#x20;          \- DB\_PASSWORD&#x20;

&#x20;          \- DB\_PORT&#x20;

&#x20;          \- DB\_USER&#x20;

&#x20;          \- DB\_VENDOR&#x20;

&#x20;          \- KEYCLOAK\_USER&#x20;

&#x20;          \- KEYCLOAK\_PASSWORD&#x20;

&#x20;          \- ENABLE\_OTP\_MESSAGE&#x20;

&#x20;          \- KAFKA\_BOOTSTRAP\_SERVERS&#x20;

3\. Run the deploy script to deploy the application on Kubernetes.

{% hint style="info" %}
sudo sh deploy.sh -i \<path to inventory file> -p \<Directory containing Kubernetes Config files> -d \<Private Docker Registry IP> -k \<Kube Master Node IP> -s \<Key file to access Kube Master>
{% endhint %}

## Post installation

### Create indexes on database tables&#x20;

The indexes for efficient querying of the database tables do not get automatically created and hence need to be created manually. Execute registry\_index.sql is present within the DIVOC codebase on the database. A restart of the registry service is required for this change to reflect.&#x20;

**Note:** Database tables are only created when the first API request is received.  &#x20;



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
