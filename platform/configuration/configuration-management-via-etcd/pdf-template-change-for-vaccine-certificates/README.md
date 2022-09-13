# PDF Template Change for Vaccine Certificates

Any template-related changes can be done by updating the HTML template in the etcd manager. Supported fields include the following:&#x20;

| Beneficiary Details     | Vaccination Details    | Previous Dose Details     |
| ----------------------- | ---------------------- | ------------------------- |
| name                    | vaccine                | vaxEvents\[].dateOfVax    |
| age                     | vaccinationDate        | vaxEvents\[].doseType     |
| gender                  | vaccineBatch           | vaxEvents\[].vaxName      |
| identity (masked value) | vaccineICD11Code       | vaxEvents\[].vaxType      |
| nationality             | vaccineProphylaxis     | vaxEvents\[].vaxBatch     |
| beneficiaryId           | vaccineType            | vaxEvents\[].countryOfVax |
| recipientAddress        | vaccineManufacturer    |                           |
|                         | vaccineValidDays ****  |                           |
|                         | vaccinatedBy           |                           |
|                         | vaccinatedAt           |                           |
|                         | certificateId          |                           |
|                         | dose                   |                           |
|                         | totalDoses             |                           |

### **Example: Adding a field such as ‘nationality’ to the PDF template.**

### Steps to add ‘nationality’ to the PDF template**:**

* Go to the Manage keys in etcd-manager.&#x20;
* Go to the “vaccineCertificateTemplate” key and click on the Edit key to update the template. **** In this case, the ‘nationality’ field is being added. The value expected for this “vaccineCertificateTemplate” configuration is html and can be customised as per your needs.&#x20;
* The same will be reflected in the PDF of the vaccination certificate. Click on Save. A popup will appear as “operation successful.” Click on Close.

![](<../../../../.gitbook/assets/Screenshot 2022-06-17 at 5.54.33 PM (1).png>)

* Call “GET VaccineCertificate API,” which will return the PDF certificate template. Verify if the new field ‘nationality’ is getting reflected.

![Sample certificate](<../../../../.gitbook/assets/Screenshot 2022-06-17 at 5.57.09 PM.png>)



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._    &#x20;
