# PDF Template Change for Vaccine Certificates via ETCD CLI

Any template-related changes can be done by updating the HTML template using ETCD CLI. Before making any change, the PDF template will look like:

<figure><img src="../../../.gitbook/assets/Screenshot 2022-09-01 at 12.13.18 PM.png" alt=""><figcaption><p>Sample certificate</p></figcaption></figure>

### **Example:  Adding a field such as ‘nationality’ to the PDF template.**

### Steps to add **'**nationality' to the PDF template:

* Go to the specific path where etcd is configured.
* Open the file to add the new field that will get displayed in the template (vim vaccineCertificateTemplate.html).

<figure><img src="../../../.gitbook/assets/Screenshot 2022-09-01 at 12.16.34 PM.png" alt=""><figcaption></figcaption></figure>

* To reflect the change, run the updateConfigs shell script using the command: ./updateConfigs.sh. It shows "OK OK OK...." This means that etcd has been updated with the new template successfully.

<figure><img src="../../../.gitbook/assets/Screenshot 2022-09-01 at 12.18.36 PM.png" alt=""><figcaption></figcaption></figure>

* Generate the PDF again using GET API.

<figure><img src="../../../.gitbook/assets/Screenshot 2022-09-01 at 12.20.04 PM.png" alt=""><figcaption><p>Sample certificate</p></figcaption></figure>



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._ &#x20;
