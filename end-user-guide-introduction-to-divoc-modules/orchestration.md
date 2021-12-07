# Orchestration

Using this module you can create and maintain program, facility, vaccine, and vaccinator registries. Countries that do not have digital health registries can use this module to create digital infrastructure/resources for any kind of public health program. Countries can also create appointment schedules and daily rates of vaccination for different facilities.

|    Program Registry   |   Vaccine Registry   |    Facility Registry   |         Vaccinator Registry         |   |
| :-------------------: | :------------------: | :--------------------: | :---------------------------------: | - |
|  Vaccination programs |   Approved vaccines  |   Approved facilities  |  <p>Trained </p><p>vaccinators</p>  |   |
|     Active status     |     Active status    |        Location        |            Active status            |   |
|    Allowed vaccines   | Vaccination schedule |      Active status     |  <p>Training </p><p>certificate</p> |   |
|  Start and end dates  |    Batch deny list   | Vaccination daily rate | <p>Associated </p><p>facilities</p> |   |
| Certificate templates |   Max retail price   |      Total supply      |  <p>Rating and </p><p>feedback</p>  |   |
|                       |  Vaccination method  |   Rating and feedback  |                                     |   |

### Who would typically use this module?&#x20;

DIVOC comes with **three default roles**:

1. **System admin**&#x20;
2. **Controller**&#x20;
3. **Facility admin**

### Each has specific functions and logins assigned to them -&#x20;

### Steps to follow:

### **1. System Admin**&#x20;

A system admin can be a user from the IT department of the country responsible for setting up initial rules, configuration, and master data upload for the specific program/programs in question.

Use the following URL: [**https://demo-divoc.egov.org.in/portal**](https://demo-divoc.egov.org.in/portal). Log in using 2111111111 and OTP 1234

![](<../.gitbook/assets/Screenshot 2021-12-07 at 1.00.52 PM.png>)

**A. Program setup**

1\. Click on **Vaccine Programs**. Register a new vaccine/immunisation program by clicking on **REGISTER NEW VACCINE PROGRAM**.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 1.03.52 PM.png>)

2\.  Add the program name, program description, program logo, start and end dates, and select vaccine. Click on SAVE. You will see a list of all vaccine programs currently active in your country.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 1.05.59 PM.png>)

**B. Vaccine registration**

1\. Click on **Vaccines**. **** You can register a new vaccine, as well as existing ones by clicking on **REGISTER NEW VACCINE.**

![](<../.gitbook/assets/Screenshot 2021-12-07 at 1.09.44 PM.png>)

2\. Fill in details such as the name of the vaccine, manufacturer, administration type,\
price, duration dose (if there are multiple doses), and vaccine validity. Next, click on\
**SAVE**. It will show all the vaccines active in your country.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 1.13.40 PM.png>)

**C. Facility setup**

1\. Click on **Facilities.** Create a list of vaccination centres as per the given CSV template and save it on your laptop/desktop. You can add details such as facility code, facility name, contact, email, operating hour (start/end), category, type, status, address, website URL, admin name, and admin mobile.

2\. Click on **UPLOAD CSV** to upload this list.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 1.17.02 PM.png>)

**D. Recipient pre-enrollment**

1\. Click on **Pre-Enrollment**. Create a list of the number of recipients successfully enrolled as per the given CSV template. You can add details such as phone number, identity, date of birth, gender, name, email, address, and dose number, among others. Once the list is ready, save it on your laptop/desktop. Click on **Select a Program.**

2\. Next, click on **UPLOAD CSV** to upload the list.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 1.21.00 PM.png>)

**E. Set up vaccinators**

1\. Click on **Vaccinators.** Create and save a list of vaccinators that have been identified and trained for the vaccination program/campaign as per the suggested CSV template on your  laptop/desktop. Add details such as code, name, mobile number, email id, status, and facility id.

2\. Click on **UPLOAD CSV** to upload the list.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 1.24.26 PM.png>)

### 2. Controller&#x20;

The controller user role can be utilised by a program administrator who manages facility enrollment and oversees the facility operations aligned with the program objective. The person would be responsible for setting up per day facility vaccination rate, and activating/deactivating the facilities, etc.

Use the following URL: [**https://demo-divoc.egov.org.in/portal**](https://demo-divoc.egov.org.in/portal). Log in using 1111111170 and OTP 1234

**A. Facility activation/deactivation**&#x20;

Go to **Facility Activation**. Select Program, Region, and Type of Facility. Select the facilities you want to activate from the list. Click on **Make Active**. To deactivate a facility, follow the same steps and select the facilities you want to deactivate. Click on **Make Inactive** to deactivate a facility.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 1.45.43 PM.png>)

**A. Facility activation/deactivation**

1\. Go to **Facility Activation**. Select Program, Region, and Type of Facility. Select the facilities you want to activate from the list. Click on **Make Active**. To deactivate a facility, follow the same steps and select the facilities you want to deactivate. Click on **Make Inactive** to deactivate a facility.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 1.50.55 PM.png>)

**B. Adjusting vaccination rate**

Go to **Adjusting Rate**. Select Program Name, Region, Type of Facility. Select one or more facilities to set/modify daily vaccination rates. Click on **SET RATES**.

**C. Notify Facilities**

1\. Go to **All Facilities**. Select Program, Region, Type of Facility. Select the facility. Click on **NOTIFY**.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 1.57.51 PM.png>)

2\. Write the subject matter and the message. Click on **SEND**.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 1.58.45 PM.png>)

### 3. Facility Admin

Use the following URL: [**https://demo-divoc.egov.org.in/portal**](https://demo-divoc.egov.org.in/portal). Log in using 3333333341 and OTP 1234.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 2.00.33 PM.png>)

**A. Set up appointment schedules**

1\. Go to **Program Overview**. Click on **CONFIGURE SLOTS**.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 2.02.59 PM.png>)

2\. Select **Appointment Hours** to set/change the timings, and set up/change the **Maximum number of appointments allowed**. Select **Walk-in Hours** to set up /change the timings, and set up/change the **Walk-in Days**. Click on **SAVE.**

![](<../.gitbook/assets/Screenshot 2021-12-07 at 2.05.07 PM.png>)

**C. Add/Remove Vaccinators**

1\. Go to **Vaccinator Details**. Click on **ADD NEW VACCINATOR**.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 2.07.23 PM.png>)

2\. Add details such as name, mobile number, email id, license number, and certification, if any. Click on **ADD**.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 2.08.31 PM.png>)

**C. Setup facility staff role**

1\. Go to **Role Setup**. Mention role type, name, mobile number, and employee id. Select Enabled to activate status. Click on **SAVE**.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 2.10.12 PM.png>)

**D. Create recipient vaccination details**

1\. Go to **Upload Vaccination Details**. Create a list of recipients as per the given CSV template and save it on your laptop/desktop. You can add details such as pre-enrollment code, recipient name, mobile number, age, gender, identity, address, vaccination batch, vaccination date, vaccination dose, vaccination name, vaccinator name, facility name, and address, among others.

2\. Click on **UPLOAD CSV** to upload this list.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 2.12.01 PM.png>)

**E. Check beneficiary list (past, current and upcoming)**

Go to **Beneficiaries**. Select Program, Start Date, and End Date. Click on **SEARCH**.

![](<../.gitbook/assets/Screenshot 2021-12-07 at 2.14.09 PM.png>)





