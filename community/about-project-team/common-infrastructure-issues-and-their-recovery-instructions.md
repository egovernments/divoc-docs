# Common Infrastructure Issues and their Recovery Instructions

## Levels of Support

L1: It is the initial level of support provided by the user help desk. They help to screen the issues and typically handle queries like "how to," FAQs, user creation, password resets, etc.

L2: It deals with support tickets that can be resolved by doing basic configuration in the application or suggesting workarounds. Other activities typically include environment management e.g. server monitoring, server management etc. For L2 support, we expect a team of infrastructure management-related skill sets.

L3: It deals with tickets typically requiring minor country-specific code changes (certificate templates, logo, UI, and not core platform code), analysis of changes in new/patch versions, data queries, handling environment issues that cannot be resolved by L2 staff. For L3 support, we expect a team of software engineering-related skill sets.

L4: It deals with tickets related to product enhancements or product defects. This would typically be worked on by the DIVOC team, which, in turn, will either release a hotfix, patch release, or bundle it in the next release, or defer/deprioritise.

## **Troubleshooting Guide for L2**

### 1. If you are getting the response as 401:

* Possible causes: Token has expired.

&#x20;     \- Check access token is valid or correct for API call.

* Action to be taken:

&#x20;    \- Open postman.

&#x20;    \- Create a POST request to /auth/realms/divoc/protocol/openid-connect/token endpoint.

&#x20;    \- Add the following parameters:

&#x20;       client-id as admin-api&#x20;

&#x20;       Grant-type as client-credentials&#x20;

&#x20;       Client\_secret as

&#x20;    \- Once the request is sent, you will receive the auth\_token as part of the payload.

&#x20;    \- Modify the ADMIN\_API\_SECRET parameter within divoc-config.yaml file.

&#x20;    \- Restart all the services using: kubectl rollout restart deployments -n \<namespace of divoc  installation>

### 2. If you are getting the response as 405:

* Action to be taken:

&#x20;     \- Check if the Content-Type in the header section is set as ‘application/json’

&#x20;     \- If not, set the Content-Type as ‘application/json’

### 3. If you are getting the response as 602:

* Action to be taken:

&#x20;    \- Check if the payload is missing any parameter value like ‘preEnrollmentCode’, ‘recipient.name’, etc.

&#x20;    \- If yes, add the missing parameter and check.

### **4. If you are getting the response as 400:**

* Action to be taken:

&#x20;     \- Check if the format of value in payload or json structure is as per the expected structure. For example - format of date value, dose count is number or string, etc.

&#x20;     \- If not, correct the value type in the payload.

### 5. If you are getting the response as 504:

* Action to be taken:

&#x20;    \- Check if the DIVOC system is reachable from the source system, or if the IP/domain of the DIVOC system is mapped correctly.  &#x20;

&#x20;    \- If not, correct the IP/domain name or check the network.&#x20;

### 6. If you are getting response as 502: Bad Gateway:

* Action to be taken:

&#x20;     \- Check if all the DIVOC services required for the generation of certificates are up and running.

&#x20;     \- Steps to be followed to check if required services are running:

&#x20;        Login in to the DIVOC server.

&#x20;          ****           Go to the deployment folder.

&#x20;        Run this command: kubectl get pods -n \<divoc namespace>

&#x20;     \- If any of the pods are down and do not have an active running container:

&#x20;        Restart the pod with this command: kubectl rollout restart deployment

&#x20;        \<name of the deployment which is down> -n \<divoc namespace>

&#x20;          ****           Run this command again: kubectl get pods -n \<divoc namespace>

&#x20;        Validate if all the deployments are up again.

&#x20;        Check if you are able to generate the certificate.

&#x20;       \- If you are still not able to generate the certificate, then check the logs of deployments one by one using this command: kubectl logs -f deployment/\<deployment\_name> -n \<divoc\_namespace>

&#x20;       \- If you find any errors in the logs or if the logs are not clear to you, share the logs with the L3 team for resolution of the issue.

### 7. If the gateway service is down:

* Action to be taken:

&#x20;    \- Try restarting the gateway service: kubectl rollout restart deployment gateway -n \<divoc\_namespace>

&#x20;    \- If the service does not start, look at the deployment logs and pass on the information to the L3 team: kubectl logs -f deployment gateway -n \<divoc\_namespace>

### 8. If you are trying to generate/update a certificate, check if the vaccination API service is down:

* Action to be taken:

&#x20;     \- Try restarting the vaccination api service: kubectl rollout restart deployment vaccination-api -n \<divoc\_namespace>

&#x20;      \- If the service does not start, look at the deployment logs and pass on the information to the L3 team: kubectl logs -f deployment vaccination-api -n \<divoc\_namespace>

### 9. If the certificate signer service is down:

* Action to be taken:

&#x20;    \- Try restarting the certificate signer service: kubectl rollout restart deployment certificate-signer -n \<divoc\_namespace>

&#x20;     ****      - If the service does not start, look at the deployment logs and pass on the information to the L3 team: kubectl logs -f deployment certificate-signer -n \<divoc\_namespace>

### 10. If the registry services are down:

* Action to be taken:

&#x20;    \- Try restarting the registry service: kubectl rollout restart deployment registry -n \<divoc\_namespace>

&#x20;    \- Try connecting to the database directly using the following command: psql -h \<DB\_ADDRESS> -U

&#x20;        a. If you are able to access the registry, look at the deployment logs and pass on the information to the L3 team: kubectl logs -f deployment registry -n \<divoc\_namespace>

&#x20;        b. If you are unable to connect to the database, restart the database and try connecting again. If the problem persists, reach out to the L3 team.

### 11. If you are trying to fetch the certificate, check if the certificate API services are down:

* Action to be taken:

&#x20;    \- Try restarting the certificate api service: kubectl rollout restart deployment certificate-api -n \<divoc\_namespace>

&#x20;   \- If the service does not start, look at the deployment logs and pass on the information to the L3 team: kubectl logs -f deployment certificate-api -n \<divoc\_namespace>

### 12. If the SMS/notification services are down:

* Action to be taken:

&#x20;    \- Regenerate a new SMS Auth Key from the SMS provider.

&#x20;    \- Update SMS\_AUTH\_KEY property in divoc-config.yaml.

&#x20;    \- Restart notification service: kubectl rollout restart deployment notification-service -n \<divoc\_namespace>

### 13. If the services are taking a long time to return:

* Possible causes: Indexes not present in database.
* Action to be taken:

&#x20;     \- Check if the following indexes are present for the following columns in VaccinationCertificate DB table in the database:&#x20;

&#x20;       a. OSID

&#x20;       b. certificateId

&#x20;       c. Contact

&#x20;       d. Mobile

&#x20;       e. preEnrollmentCode in

&#x20;   \- If they are not present, run the following commands:

&#x20;      a. CREATE INDEX CONCURRENTLY "public\_V\_VaccinationCertificate\_preEnrollmentCode\_sqlgIdx" ON "public"."V\_VaccinationCertificate" ("preEnrollmentCode");

&#x20;      b. CREATE UNIQUE CONCURRENTLY INDEX "public\_V\_VaccinationCertificate\_certificateId\_sqlgIdx" ON "public"."V\_VaccinationCertificate" ("certificateId");

&#x20;      c. CREATE INDEX CONCURRENTLY "public\_V\_VaccinationCertificate\_contact\_sqlgIdx" ON "public"."V\_VaccinationCertificate" ("contact");

&#x20;      d. CREATE INDEX CONCURRENTLY "public\_V\_VaccinationCertificate\_mobile\_sqlgIdx" ON "public"."V\_VaccinationCertificate" ("mobile");

&#x20;      e. CREATE INDEX CONCURRENTLY "public\_V\_VaccinationCertificate\_osid\_sqlgIdx" ON "public"."V\_VaccinationCertificate" ("osid");

### 14. If signed certificates are not being created when  vaccination events occur:

* Possible causes: Redis server is down.
* Possible actions:

&#x20;     \- Check if you are able to connect to redis server using redis-cli: redis-cli -h \<IP ADDR of server>

&#x20;     \- If you are not able to connect, then restart the server.

&#x20;       a. SSH into the redis server.

&#x20;       b. List the redis-server process: sudo service redis-server status.

&#x20;       c. Fetch the process-id of redis-server.

&#x20;       d. Kill the redis-server process (sudo kill -9).

&#x20;       e. Restart redis-service process (sudo systemctl restart redis).

&#x20;       f.  Confirm that we are now able to connect to redis-server using “redis-cli” command.

## Infrastructure Issues

1. Increase the limit on the number of times a certificate could be updated:

Update the “divoc-config.yml” file with a new value (greater than the default value of 100) for “CERTIFICATE\_UPDATE\_LIMIT” property and apply it. Kubectl rollout restart deployment vaccination-api -n **\<divoc-namespace>**

2\. **** Pod is restarting frequently - If you run kubectl get pods -n and see that the number of pod restarts is high:

There can be multiple reasons why a pod restarts -&#x20;

* CPU limit is exceeded by pods: Modify the deployment by increasing the requests and limits on CPU.
* Memory limit is exceeded by pods: Modify the deployment by increasing the requests and limits on memory.
* Memory issue in the machine on which Kubernetes (worker node) is installed. We can increase the number of worker nodes or increase the memory of the worker nodes and then recreate pods if necessary.
* Code issue: Sometimes there can be an issue with the code or the config might be missing. In such cased, we need to fix the bug.

3\. Kubernetes cluster is not reachable from Kubeadm master node as SSL certs have expired:

If you encounter the following error:&#x20;

\#> kubectl version Client Version: version.Info{Major:"1", Minor:"9", GitVersion:"v1.9.0", GitCommit:"925c127ec6b946659ad0fd596fa959be43f0cc05", GitTreeState:"clean", BuildDate:"2017-12-15T21:07:38Z", GoVersion:"go1.9.2", Compiler:"gc", Platform:"linux/amd64"} The connection to the server 135.122.6.50:6443 was refused - did you specify the right host or port?

Recovery steps are as follows:

1. Check if certs have expired: kubeadm alpha certs check-expiration --config=/root/kubernetes/kubeadm-config.yaml
2. Renew Certs:

* cd /etc/kubernetes/pki/
* mv
* {apiserver.crt,apiserver-etcd-client.key,apiserver-kubelet-client.crt,front-proxy-ca.crt,front-proxy-client.crt,front-proxy-client.key,front-proxy-ca.key,apiserver-kubelet-client.key,apiserver.key,apiserver-etcd-client.crt} \~/
* kubeadm init phase certs all --apiserver-advertise-address \<Specify Master node LAN IP addr>
* cd /etc/kubernetes/
* mv {admin.conf,controller-manager.conf,kubelet.conf,scheduler.conf} \~/
* kubeadm init phase kubeconfig al

3\. Reboot server: reboot

4\. After reboot ensure docker and all Kube\* daemons are up docker ps | grep kube-apiserver

5\. Mandatorily replace the config file with newly created one, to resolve “kubectl localhost:8080 connection refused” issue -

* mkdir -p $HOME/.kube
* sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
* sudo chown $(id -u):$(id -g) $HOME/.kube/config

6\. Issue Kubectl commands

## Resources:

#### Pre-reads:&#x20;

1. [Skills needed to set up DIVOC.](../../implementing-divoc/skills-needed-to-set-up-divoc.md#what-does-this-section-cover)
2. [Implementation checklist.](../../implementing-divoc/implementation-checklist.md)
3. [DIVOC's certification and verification component.](../../platform/configuration/configuring-the-certification-and-verification-component/)

#### Links to the development process and the environments (such as Github, Testing, etc):

1. Source Code - [https://github.com/egovernments/DIVOC](https://github.com/egovernments/DIVOC)
2. [Setting up DIVOC development environment](../../tech-docs/setting-up-divoc-development-environment.md).
3. [Setting up the production environment.](../../implementing-divoc/#what-will-it-cover)

#### Modifying vaccine certificate and template; Branding changes such as UI changes; Adding a new role; Changing the content to the verification page:

1. [ETCD configuration.](../../platform/configuration/configuration-management-via-etcd/pdf-template-change-for-vaccine-certificates/pdf-template-change-for-vaccine-certificates-via-etcd-cli.md)
2. [Configure the verification component.](../../platform/configuration/configuring-the-certification-and-verification-component/how-to-set-up-the-verification-portal-for-implementation.md#overview)

#### Wiki documentation & discussion forum:

1. Documentation: **** [**https://divoc.digit.org/**](https://divoc.digit.org/)
2. Report issues: [**https://github.com/egovernments/DIVOC/issues**](https://github.com/egovernments/DIVOC/issues)****
3. Discussion forum: **** [**https://github.com/egovernments/DIVOC/discussions**](https://github.com/egovernments/DIVOC/discussions) ****&#x20;
4. Join us on slack: **** [**https://app.slack.com/client/T109J61DY/C03EC8C65SN**](https://app.slack.com/client/T109J61DY/C03EC8C65SN) ****&#x20;

__

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
