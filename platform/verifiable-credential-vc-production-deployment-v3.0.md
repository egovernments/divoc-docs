# Verifiable Credential (VC): Production Deployment V3.0

## Components to be deployed:

1. DB: Postgres DB
2. Kafka & Zookeeper: The verifiable credential (VC) generation process is an asynchronous process. The initial VC generation process checks for the validity of the payload and pushes the incoming payload in Kafka queues, which then get consumed and signed asynchronously.
3. Keycloak: It is the access management service used to restrict the access of resources only to authenticated users.
4. Registry: Registry by Sunbird-RC is used for tenant creation, schema creation and VC generation, update, and revocation flows. It is also responsible for persistence in DB.
5. Sunbird-Certificate-signer: This service is used for signing the event payload and it returns a signed credential.
6. Sunbird-Certificate-API: This service is used for downloading certificates (VCs in JSON+LD format, QR codes, certificates in PDF format, etc).
7. File-Storage (MinIO): This service is used for storing the uploaded context files, and template files. Either the cloud storage or the volume mounted on the server can be attached and accessed via this service.
8. VC-Management-Service: This is a wrapper service that exposes the rest endpoints of the registry for tenant creation, schema creation, upload context, and upload template.
9. VC-Certification-Service: This is a wrapper service that exposes the rest endpoints of the registry for VC creation, VC download, VC update, VC revoke, etc.
10. VC-Certify-Consumer: This service has Kafka consumers, which consume an event payload and make a request to the registry for either signing and persisting a new VC or updating and revoking an existing VC record.

## Deployment steps:

1. Set up a DB with the name ‘registry.’ It should be accessible in the k8s cluster.
2. Set up a Redis server, which should be accessible by DIVOC services in the k8s cluster.
3. Set up the Kafka service and see if it is reachable from within the k8s cluster slave nodes

* Create topics “vc-certify”, “vc-remove-suspension”, “post-vc-certify”
* bin/kafka-topics.sh --create --topic --replication-factor 2 --partitions 8 --bootstrap-server :9092 --config retention.ms=2592000000

4\. Create a folder for MinIO storage on the server for volume mounting, (or) set up cloud storage (eg:s3) and create a bucket.

5\. Generate an RSA keypair

* openssl genrsa > private.pem
* openssl rsa -in private.pem -pubout -out public.pem

6\. Create a config map with the environment variables (Configmap YML file available in infra/Kubernetes folder).

7\. Bring up the services (All the required deployment and service files are available in the infra/Kubernetes folder):

* Bring up keycloak service using the deployment files
* Setup Ingress using ingress yml file
* Access Keycloak UI using \<ingressURL>/auth
* Import src-realm-export.json file and create a new realm sunbird-rc
* Select clients > admin-api > credentials > Regenerate Client Secret
* Update the client secret in environment variables by editing the config map
* Bring up the services in this order:

&#x20;     i. File-storage

&#x20;     ii. Registry

&#x20;     iii. SB-Certificate-Signer

&#x20;     iv. SB-Certificate-API

&#x20;     v. VC-Management-service

&#x20;     vi. VC-Certification-service

&#x20;     vii. VC-Certify-Consumer



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
