# Adding a New Vaccine and ICD-11 Mapping

There are different International Classification of Diseases (ICD) codes based on the category of vaccines. To add a new vaccine, identify the ICD-11 code to which the vaccine belongs. Once you have mapped the vaccine to the relevant ICD-11 code, you can update the vaccine name and its ICD-11 mapping in etcd.

### Steps to update the vaccine name and its ICD-11 mapping:

* Go to the Manage keys tab of the etcd-manager app. To add or update mappings, two keys must be updated: “VACCINE\_ICD” and “ICD.”
* To add the vaccine name, ICD-11 code, and description VACCINE\_ICD, go to VACCINE\_ICD and click on the Edit key.&#x20;

&#x20;      \- Example of VACCINE\_ICD value for Covaxin:&#x20;

&#x20;        {“vaccineName”: “covaxin”, “icd11Code”: “XM1G90”}

* Click on Save. A popup will appear as “operation successful.” Click on Close.

![](<../../../../.gitbook/assets/Screenshot 2022-06-17 at 7.58.12 AM.png>)

* Click on the edit button of the “ICD” key to add ICD-11 code and click on the Edit key.

&#x20;     \- Example of ICD value for Covaxin:

&#x20;      {“XM1G90”: {“vaccineType”: “inactivated virus”, “icd11Term”: “COVID-19 vaccine, inactivated virus”\}}

* Click on Save. A popup will appear as “operation successful.” Click on Close.

![](<../../../../.gitbook/assets/Screenshot 2022-06-17 at 8.05.04 AM.png>)

* Make the certificate generation request call and fetch the certificate to test the changes. Once updated, any new certificate can be issued using the new vaccine name.

![This is a sample certificate generated with the new vaccine type, with ICD-11 code XM6JD5 and ICD-11 term: ‘COVID-19 vaccine, live attenuated virus.’](<../../../../.gitbook/assets/Screenshot 2022-06-17 at 8.07.20 AM.png>)

__

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._                                 &#x20;
