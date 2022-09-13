# Adding a New Vaccine and its Mapping via ETCD CLI

With the ETCD CLI, the same can be dynamically updated in the files (euVaccineProph.json and euVaccineCode.json) without any service deployments.

### **Steps to add the extra EU vaccine configurations**

* Go to the specific path where etcd is configured.
* Open the files to add the new vaccine or update the existing vaccine.
* Run the command: vim euVaccineCode.json.

<figure><img src="../../../../.gitbook/assets/Screenshot 2022-09-01 at 12.33.59 PM.png" alt=""><figcaption></figcaption></figure>

* Run the command:vim euVaccineProph.json.

<figure><img src="../../../../.gitbook/assets/Screenshot 2022-09-01 at 12.36.53 PM.png" alt=""><figcaption></figcaption></figure>

* Run the command:vim [euVaccineManuf.json](https://github.com/egovernments/DIVOC/blob/main/default-configuration/etcd/euVaccineManuf.json).

<figure><img src="../../../../.gitbook/assets/Screenshot 2022-09-01 at 12.39.15 PM.png" alt=""><figcaption></figcaption></figure>

* To reflect the change, run the command: ./updateConfigs.sh. It shows "OK OK OK...."This means that etcd has been updated with the new vaccine list successfully.

<figure><img src="../../../../.gitbook/assets/Screenshot 2022-09-01 at 2.00.02 PM.png" alt=""><figcaption></figcaption></figure>

* Create the certificate and generate the PDF with the new vaccine.

<figure><img src="../../../../.gitbook/assets/Screenshot 2022-09-01 at 2.02.13 PM.png" alt=""><figcaption><p>Sample certificate</p></figcaption></figure>



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._  &#x20;
