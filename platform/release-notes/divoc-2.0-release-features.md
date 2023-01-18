# DIVOC 2.0 Release Features

## Version release date&#x20;

* March 25, 2022.

## **Release summary**

If your country is implementing DIVOC 2.0, it is important to know the additions/changes that we have made as part of this release:

* **Configuration management via** [**etcd**](https://etcd.io/)**:** You can make configuration changes to DIVOC’s certificate module via etcd without needing a new deployment. Click [**here**](../configuration/configuration-management-via-etcd/) to know more.
* **Support for EU compliant digital certificates and Smart Health Cards:** DIVOC’s **EU-DCC** and **SHC** adapter services facilitate easy travel for residents from DIVOC’s adopter countries. Know more about DIVOC’s [**EU-DCC**](../divocs-verifiable-certificate-features/divocs-eu-dcc-adapter-service.md) and [**SHC**](../divocs-verifiable-certificate-features/divocs-shc-adapter-service.md) adapter services.
* **Print certificates at the facility:** We have added the capability to print vaccination certificates when a beneficiary walks into a facility. Click [**here**](../divocs-verifiable-certificate-features/printing-certificates-at-a-facility.md) to know more.
* **New API for revocation services:** A new Revoke API has been introduced that can be used to revoke an issued certificate for manual revocation use cases. Click [**here**](../divocs-verifiable-certificate-features/revoking-a-divoc-certificate.md) to know more.
* **Deployment activities automated reducing installation time:**&#x20;

&#x20;        \- Automating our infrastructure setup has reduced our deployment time from about 3 days  to 1 day.&#x20;

&#x20;        \- DIVOC’s [**installation process**](../installation/setting-up-divoc-in-k8-cluster/how-to-install-divoc.md) has been streamlined with the introduction of the new scripts. The details of the scripts are given below:

1. Install the prerequisites and set up the various hardware clusters.
2. Push the docker images to the appropriate registry.
3. Deploy the code from the registry into the Kubernetes cluster.

* **Enhanced performance of PDF certificate generation:** We have fine-tuned our PDF generating algorithms, which has lowered the consumption of system resources.



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
