# Setting up DIVOC development environment

This will cover the following:&#x20;

* [Running DIVOC on a local machine](setting-up-divoc-development-environment.md#running-divoc-on-a-local-machine)&#x20;
* [DIVOC walkthrough](setting-up-divoc-development-environment.md#divoc-walkthrough)

## Running DIVOC on a local machine&#x20;

In this section, we will walk you through how to run DIVOC on a local machine.&#x20;

### Steps

**Step 1:** Install Docker Compose&#x20;

* You can find the instructions [**here**](https://docs.docker.com/compose/install/).&#x20;
* Basic Docker Compose commands:&#x20;

&#x20;      \- Staring services [**docker-compose up**](https://docs.docker.com/compose/reference/up/).&#x20;

&#x20;      \- Restarting services [**docker-compose restart**](https://docs.docker.com/compose/reference/restart/).&#x20;

&#x20;      \- Checking Status of services [**docker-compose ps**](https://docs.docker.com/compose/reference/ps/).&#x20;

&#x20;      \- Monitoring service logs [**docker-compose logs**](https://docs.docker.com/compose/reference/logs/).

**Step 2:** Clone DIVOC repository onto your local machine and navigate to the DIVOC directory:&#x20;

```
git clone git@github.com:egovernments/DIVOC.git && cd DIVOC
```

**Step 3:** Start all services in the detached mode.

```
docker-compose up -d
```

* [**Verify the state of containers**](https://github.com/egovernments/DIVOC/blob/main/docs/developer-docs/index.md#docker-compose-ps)**.** All containers should be up.
* Some services might fail to start because the dependent service may not be ready yet. [**Restarting the failed service**](https://github.com/egovernments/DIVOC/blob/main/docs/developer-docs/index.md#docker-compose-restart) should start it successfully in this case.
* On Mac/Windows, services may crash with exit code:137, if sufficient memory is not set for docker. This can be changed in the Docker desktop preferences, resources tab, as shown[ **here**](https://docs.docker.com/docker-for-mac/#resources).

**Step 4:** Explore DIVOC

* The following are the routes to access local apps. The remaining routes can be found in `nginx/nginx.conf.`

|         Address         |  Application |
| :---------------------: | :----------: |
|        localhost        |  public app  |
|     localhost/portal    |  portal app  |
| localhost/facility\_app | facility app |

## DIVOC walkthrough

In this section, we will go through the steps involved in a typical flow, starting from setting up facilities to generating a certificate after vaccination.

### Set up Keycloack

* Login to Keycloak console (`localhost/auth/admin`) as `admin` (password : `admin`)
* Hover on `Master` on the left top corner and click on `Add realm.`
* Click on `Select File` button (import option).
* Select `realm-export.json` in the keycloak directory. `path:DIVOC/keycloak.`
* Click on create.

### Set up CLIENT\_SECRET for `admin-api`

* Login to Keycloak console (`localhost/auth/admin`) as `admin` (password:`admin`).
* Click on `Clients` in the configure section on the left pane and click on `admin-api.`
* Go to the credentials tab, click on `Regenerate Secret` and copy the new secret.
* Change the `ADMIN_API_CLIENT_SECRET` to the copied secret in `docker-compose.yml.`
* Rebuild and restart the services that use `ADMIN_API_CLIENT_SECRET.`

```
docker-compose up -d --build --no-deps <service1> <service2>...
 docker-compose restart nginx
```

### Flagr configuration

The following steps configure notification templates for the app (**this can skipped if you do not want to test notifications**).

* Visit `localhost/config`.&#x20;
* Enter `notification_templates`in the flag description field and click on `Create New Flag.`
* Click on the new flag created to configure it.
  * In the Flag section, change flag key to `notification_templates`
  * In the Variant section, create new variant with key as `default`, below attachment

```
{
    "facilityPendingTasks": {
    "html": "<h4>Dear Facility Administrator,</h4>Request you to upload / complete all details pertaining to this facility prior to execution of the Vaccination Program. <br/>Failing to do so, this facility: <br/><b>- will not be accessible to citizen during the pre-enrolment phase <br/>- will not be able to use the Vaccination App or generate digital certificates. </b><br/>Please submit the missing details at the earliest.DIVOC System Administrator",
    "message": "Dear Facility Administrator,Request you to upload / complete all details pertaining to this facility prior to execution of the C19 VaccinationProgram. Failing to do so, this facility: - will not be accessible to citizen during the pre-enrolment phase - will not be able to use the Vaccination App or generate digital certificates. Please submit the missing details at the earliest.DIVOC System Administrator",
    "subject": "DIVOC - Facility Pending Tasks"
    },
    "facilityRegistered": {
    "message": "Welcome {{.FacilityName}}. Your facility has been registered under divoc. You can login at https://divoc.xiv.in/portal using {{.Admins}} contact numbers.",
    "subject": "DIVOC - Facility Registered"
    },
    "facilityUpdate": {
    "message": "Dear Facility Administrator. Your facility {{.field}} is been updated to {{.value}}",
    "subject": "DIVOC - Facility Updated"
    },
    "preEnrollmentRegistered": {
    "message": "{{.Name}}, you have been registered to receive {{.ProgramId}}. Please proceed to the nearest vaccination center. Please show the Pre Enrollment Code: {{.Code}} to the center admin.",
    "subject": "DIVOC - Pre-Enrollment"
    },
    "recipientCertified": {
    "message": "{{.Name}}, your {{.VaccineName}} vaccine certificate can be viewed and downloaded at: https://divoc.xiv.in/certificate/ ",
    "subject": "DIVOC - Vaccination Certificate"
    }
}
```

* In the Segment section, create a new segment with `default` key and a default distribution of 100%.

### Create `admin` and `controller` users in Keycloak

* Login to Keycloak console (`localhost/auth/admin`) as `admin` (password : `admin`).
* Click on `Users` in the Manage section on the left panel and click on `Add User.`
* Give the username as 0000000000 and click on save.
* In the `Attributes` section, Add new key as `mobile_number` and value as 0000000000. Click on Add and save.
* Go to Groups section, select `system admin` in the available groups and click on Join.
* Similarly, create another user with `username` and `mobile_number` as 0000000001 and join the `controller` group.

### **System admin activities**

Login to the portal as `system admin` (Mobile Number : 0000000000, OTP : 1234).

**Upload Facilities.csv:**

* Click on the Facilities tab and click on `Download Template .csv.`
* Click on `Upload CSV` button and upload the downloaded csv.
* You should see the success message for at least facility.

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

* In the Facility Activation tab, select vaccination program added in the previous step, select type of facility as Govt and mark the status as Active.
* You should be able to see at least one facility in the search results.
* Click on the checkbox for the relevant facility (make note of facility code) and click on `MAKE ACTIVE.`
* The activated facility should disappear from the search results.

### Facility admin activities

Get admin mobile number for the facility code (noted in the previous step), from the `facilities.csv` uploaded.

Login to Facility Admin portal (`localhost/portal/facility_admin`) using the mobile number and OTP: 1234.

**Add facility\_staff user:**

* Click on Role Setup tab and click on the add role icon.
* Create a role with type `facility staff` and mobile number `1111111111`. Set the status as enabled and set the rate of 50 for the vaccination program.

**Add Vaccinators:**

* Click on `Vaccinator Details` tab and Click `Add Vaccinator.`
* Fill all the details. Select the vaccination program previously created in the certification dropdown.
* Click on Add and click on Back.
* Click on `Make Active` button to activate vaccinator.

**Bulk Certification:**

* Certificates can also be issued in bulk by the facility admin by uploading a CSV file.
* Go to Upload Vaccination details tab and click on the download CSV template button.
* Now upload a CSV file, containing all the fields in the template.
* The generated certificates can be viewed on the public app (`localhost`).

### **Facility staff activities**

Login to the Facility app (`localhost/facility_app`) (`Mobile Number: 1111111111, OTP: 1234).`

**Enrolling and certifying recipients:**

* Click on enrol recipient, fill all the details and proceed.
* Click on Recipient Queue, to proceed for certification.

**Certifying pre-enrolled recipients:**

* Recipients pre-enrolled by facility admin can be certified by the facility staff.
* Go to app home and click on `Verify Recipient` to proceed for vaccination.

### Recipient activities

* In the public app (`localhost`), recipients can:
  * `Download`/ vaccination certificates
  * `Verify` certificates by scanning a QR code
  * `Report` any side effects/symptoms after vaccination
* For the above operations, you need the recipient mobile number (given during pre-enrollment/vaccination). Use OTP: 1234 for all logins.

### Deployment note

Change the admin password of Keycloak console

* Go to admin console, click on the Admin menu in the top right corner and select Manage account.
* Change the password in the password section on the right.



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
