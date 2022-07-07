# EU Vaccine Configurations

To add a new vaccine to an EU certificate, a country must identify the EU code to which the vaccine belongs. The coded [**value sets**](https://ec.europa.eu/health/publications/value-sets-eu-digital-covid-certificates-update\_en) used in EU vaccination certificates include:

* vp: COVID-19 vaccine or prophylaxis
* mp: COVID-19 vaccine product
* ma: COVID-19 vaccine marketing authorisation holder or manufacturer

### Steps to add the extra field in the certificate:

* Go to the specific path where etcd is configured.
* To add the extra field in the template, go to the Manage keys where etcd is configured.
* To add the vaccine code, go to euVaccineCode and click on the Edit key to add the vaccine name and code.&#x20;

&#x20;     \- Example for Covaxin:

&#x20;        {“covaxin”: “Covaxin”}

* Click on Save. A popup will appear as “operation successful.” Click on Close.

![](<../../.gitbook/assets/Screenshot 2022-06-20 at 8.29.17 AM.png>)

* To add the prophylaxis, go to euVaccineProph and click on the Edit key to add the vaccine name and code.

&#x20;     \- Example for Covaxin:

&#x20;        {“covaxin”: “J07BX03”}

* Click on Save. A popup will appear as “operation successful.” Click on Close.

![](<../../.gitbook/assets/Screenshot 2022-06-20 at 8.31.59 AM.png>)

* To add the manufacturer, go to euVaccineManuf and click on the Edit key to add the new manufacturer.

&#x20;     \- Example for Covaxin:

&#x20;        {“bharat”: “Bharat-Biotech”}

* Click on Save. A popup will appear as “operation successful.” Click on Close.

![](<../../.gitbook/assets/Screenshot 2022-06-20 at 8.37.42 AM.png>)

* Once the mappings are available in etcd, you can create the certificate and generate the PDF with the new vaccine.

![Sample certificate](<../../.gitbook/assets/Screenshot 2022-06-20 at 8.39.49 AM.png>)



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._    &#x20;
