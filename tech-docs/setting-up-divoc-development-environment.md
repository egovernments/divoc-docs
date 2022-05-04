# Setting up DIVOC development environment

## This will cover the following:&#x20;

* [Running DIVOC on a local machine](setting-up-divoc-development-environment.md#running-divoc-on-a-local-machine)&#x20;
* [DIVOC walkthrough](setting-up-divoc-development-environment.md#divoc-walkthrough)

## Running DIVOC on a local machine &#x20;

### Steps

**Step 1:** Install prerequisites and dependencies

* Update package list - sudo apt-get update.
* Install docker - sudo apt install docker.io.
* Install docker-compose - sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose.
* Install git - sudo apt install git.
* For additional details on Docker, you can find the instructions **** [**here**](https://docs.docker.com/compose/install/)**.**
* You can find the basic Docker Compose commands below:

&#x20;      \- Starting services [**docker-compose up**](https://docs.docker.com/compose/reference/up/).

&#x20;      \- Restarting services [**docker-compose restart**](https://docs.docker.com/compose/reference/restart/).

&#x20;      \- Checking the status of services **** [**docker-compose ps**](https://docs.docker.com/compose/reference/ps/).

&#x20;      \- Monitoring service logs [**docker-compose logs**](https://docs.docker.com/compose/reference/logs/).

**Step 2:** Install DIVOC

* Clone DIVOC repository onto your local machine - git clone [**https://github.com/egovernments/DIVOC**](https://github.com/egovernments/DIVOC).
* Navigate to DIVOC directory - cd DIVOC.
* Configure DIVOC: Configurations are provided as environment variables and a default set of configurations is provided in the ‘.env.example’ file. Make a copy of this file named ‘.env’ that docker will pick up. Edit these configurations as per your need.&#x20;

```
   'cp .env.example .env'
```

&#x20;   **Step 3:** Start all services in the detached mode.

```
docker-compose up -d
```

* [**Verify the state of containers**](https://github.com/egovernments/DIVOC/blob/main/docs/developer-docs/index.md#docker-compose-ps)**.** All containers should be up.
* Some services might fail to start because the dependent service may not be ready yet. [**Restarting the failed service**](https://github.com/egovernments/DIVOC/blob/main/docs/developer-docs/index.md#docker-compose-restart) **** should start it successfully in this case.
* On Mac/Windows, services may crash with exit code:137, if sufficient memory is not set for docker. This can be changed in the Docker desktop preferences, resources tab, as shown[ **** ](https://docs.docker.com/docker-for-mac/#resources)[**here**](https://docs.docker.com/docker-for-mac/#resources)**.**

**Step 4:** To build docker images locally after making changes, run following commands&#x20;

```
make docker
make docker docker-compose up -d
```

**Step 5:** Explore DIVOC

* The following are the routes to access local apps. The remaining routes can be found in `nginx/nginx.conf.`

|         Address         |  Application |
| :---------------------: | :----------: |
|        localhost        |  public app  |
|     localhost/portal    |  portal app  |
| localhost/facility\_app | facility app |

## DIVOC walkthrough

In this section, we will go through the steps involved in a typical flow, starting from setting up facilities to generating a certificate after vaccination.

### Set up Keycloack

* Login to keycloak console (`localhost/auth/admin`) as `admin` (password : `admin`)
* Hover on `Master` on the left top corner and click on `Add realm.`
* Click on the `Select File` button (import option).
* Select `realm-export.json` in the keycloak directory. `path:DIVOC/keycloak.`
* Click on create.

### Set up CLIENT\_SECRET for `admin-api`

* Login to the keycloak console (`localhost/auth/admin`) as `admin` (password:`admin`).
* Click on `Clients` in the configure section on the left pane and click on `admin-api.`
* Go to the credentials tab, click on `Regenerate Secret` and copy the new secret.
* Change the `ADMIN_API_CLIENT_SECRET` to the copied secret in `docker-compose.yml.`
* Rebuild and restart the services that use `ADMIN_API_CLIENT_SECRET.`

```
docker-compose up -d --build --no-deps <service1> <service2>...
 docker-compose restart nginx
```

“For example - sudo docker-compose up -d --build --no-deps certificate-processor portal-api certificate-api gateway.

### **DIVOC application configuration**

DIVOC uses [**etcd**](https://etcd.io) as a configuration store for templates and other configurations. A default set of configurations is available in the default-configuration/etcd folder. The instructions to configure these are available [**here**](https://github.com/egovernments/DIVOC/tree/main/default-configuration/etcd).

### Create `admin` and `controller` users in Keycloak

* Login to the keycloak console (`localhost/auth/admin`) as `admin` (password : `admin`).
* Click on `Users` in the Manage section on the left panel and click on `Add User.`
* Give the username as 0000000000 and click on save.
* In the `Attributes` section, add a new key as `mobile_number` and value as 0000000000. Click on Add and save.
* Go to the Groups section, select `system admin` in the available groups and click on Join.
* Similarly, create another user with `username` and `mobile_number` as 0000000001 and join the `controller` group.

### **System admin activities**

Login to the portal as `system admin` (Mobile Number : 0000000000, OTP : 1234).

**Upload Facilities.csv:**

* Click on the Facilities tab and click on `Download Template .csv.`
* Click on `Upload CSV` button and upload the downloaded csv.
* You should see the success message for a facility.

**Create a vaccine:**

* Click on the Vaccines tab. Fill in all the fields on the form, mark the status as Active and click on save.
* You should see the new vaccine on the right pane in the list of registered medicines/vaccines.

**Create a vaccination program:**

* Click on the Vaccine Program tab. Fill in all the fields on the form, mark the status as Active, and click on save.
* You should see the new vaccine program on the right pane in the list of registered vaccine programs.

**Pre-enroll recipients:**

* Click on the Pre-Enrollment tab and click on `Downloaf Template .csv`
* Click on `Upload CSV` and upload a CSV file containing all the fields given in the template.
* You should see the number of recipients successfully enrolled and errors if there are any.

### **Controller activities**

Login to the portal as `controller` (`Mobile Number: 0000000001, OTP: 1234).`

**Activate facilities for vaccination program:**

* In the Facility Activation tab, select the vaccination program added in the previous step, select the type of facility as government and mark the status as Active.
* You should be able to see at least one facility in the search results.
* Click on the checkbox for the relevant facility (make note of facility code) and click on `MAKE ACTIVE.`
* The activated facility should disappear from the search results.

### Facility admin activities

Get admin mobile number for the facility code (noted in the previous step), from the `facilities.csv` uploaded.

Login to Facility Admin portal (`localhost/portal/facility_admin`) using the mobile number and OTP: 1234.

**Add facility\_staff user:**

* Click on the Role Setup tab and click on the add role icon.
* Create a role with type `facility staff` and mobile number `1111111111`. Set the status as enabled and set the rate of 50 for the vaccination program.

**Add Vaccinators:**

* Click on `Vaccinator Details` tab and Click `Add Vaccinator.`
* Fill in all the details. Select the vaccination program previously created in the certification dropdown.
* Click on Add and click on Back.
* Click on the `Make Active` button to activate the vaccinator.

**Bulk Certification:**

* Certificates can also be issued in bulk by the facility admin by uploading a CSV file.
* Go to the Upload Vaccination details tab and click on the download CSV template button.
* Now upload a CSV file, containing all the fields in the template.
* The generated certificates can be viewed on the public app (`localhost`).

### **Facility staff activities**

Login to the Facility app (`localhost/facility_app`) (`Mobile Number: 1111111111, OTP: 1234).`

**Enrolling and certifying recipients:**

* Click on enrol recipient, fill all the details and proceed.
* Click on Recipient Queue, to proceed for certification.

**Certifying pre-enrolled recipients:**

* Recipients pre-enrolled by facility admin can be certified by the facility staff.
* Go to the app home and click on `Verify Recipient` to proceed for vaccination.

### Recipient activities

* In the public app (`localhost`), recipients can:
  * `Download`/ vaccination certificates
  * `Verify` certificates by scanning a QR code
  * `Report` any side effects/symptoms after vaccination
* For the above operations, you need the recipient mobile number (given during pre-enrollment/vaccination). Use OTP: 1234 for all logins.

### Deployment note

Change the admin password of Keycloak console

* Go to the admin console, click on the Admin menu in the top right corner and select Manage account.
* Change the password in the password section on the right.



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
