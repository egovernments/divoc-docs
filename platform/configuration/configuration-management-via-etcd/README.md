# Configuration Management Via ETCD

## Making changes to DIVOC’s certificate module via etcd

We have added etcd as a configuration management tool for DIVOC. This makes it easier for implementing partners to add new vaccines, edit templates or the QR code payload, as well as add new configurations without deploying any components. Use any etcd client that you like - for example, the [**etcd-manager**](https://www.electronjs.org/apps/etcd-manager). Following are the steps to set up the etcd-manager:

* Open the URL: **** [**https://www.electronjs.org/apps/etcd-manager**](https://www.electronjs.org/apps/etcd-manager) **** and click on Download.
* To configure the host and port number: open the etcd manager app → go to settings → click on etcd → enter the respective host IP and port.
* If authentication is configured for etcd, enter the authentication credentials. Go to      Settings -> Auth -> enter username and password.
* Click on test connection to confirm connectivity and click on save.
* Next, go to the Manage keys tab on the left, and you should be able to see all the configurations already setup.

Once the etcd manager app is installed, the following can be seamlessly managed within DIVOC:

* [Adding a new vaccine and International Classification of Diseases or ICD-11 mapping.](adding-a-new-vaccine-and-icd-11-mapping/)
* [PDF template change for vaccine certificates.](pdf-template-change-for-vaccine-certificates/)&#x20;
* [EU vaccine configurations.](eu-vaccine-configurations/)&#x20;
* [Payload changes in the QR code.](payload-changes-in-the-qr-code/)&#x20;



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
