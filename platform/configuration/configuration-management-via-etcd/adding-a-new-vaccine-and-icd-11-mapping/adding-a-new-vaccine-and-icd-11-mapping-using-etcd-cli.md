# Adding a New Vaccine and ICD-11 Mapping Using ETCD CLI

Using ETCD CLI, the same can be dynamically updated in 2 files (VACCINE\_ICD.json and ICD.json) without any service deployments.

### **Steps to update the vaccine name and its ICD-11 mapping:**

* Go to the specific folder where etcd files are available.
* Open the files to add the new vaccine.
* Run the command: vim VACCINE\_ICD.json.

<figure><img src="../../../../.gitbook/assets/Screenshot 2022-09-01 at 11.57.38 AM.png" alt=""><figcaption></figcaption></figure>

* Run the command: vim ICD.json.

<figure><img src="../../../../.gitbook/assets/Screenshot 2022-09-01 at 11.59.02 AM.png" alt=""><figcaption></figcaption></figure>

* To reflect the change, run the command: ./updateConfigs.sh. It shows "OK OK OK...." This means that the etcd has been updated with new vaccine list successfully.

<figure><img src="../../../../.gitbook/assets/Screenshot 2022-09-01 at 12.00.19 PM.png" alt=""><figcaption></figcaption></figure>

* Create the certificate and generate the PDF with the new vaccine.

<figure><img src="../../../../.gitbook/assets/Screenshot 2022-09-01 at 12.01.43 PM.png" alt=""><figcaption><p>Sample certificate</p></figcaption></figure>



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._&#x20;
