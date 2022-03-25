# Distributing a DIVOC certificate

## Purpose&#x20;

The purpose of this document is to outline the features of DIVOC's certificate distribution service.

## **Overview**

* DIVOC offers several ways in which countries can distribute certificates at scale.&#x20;
* The platform is designed to facilitate multiple certificate distribution methods, which includes:

&#x20;     \- Printed paper certificate with QR code.

&#x20;     \- Digital certificate distribution - download and share QR code via URL link, email  attachments, smartphone with user authentication.

&#x20;     \- By integrating with a country's vaccination portal, health wallets, PHR, consumer, or travel applications.

&#x20;     \- Countries can also distribute certificates for a health event via DIVOC’s Citizen Portal.

![](<../.gitbook/assets/Screenshot 2022-03-25 at 1.05.17 PM.png>)

* After a health event such as vaccination, citizens can log in to the Citizen Portal with their registered mobile number, and they are given the option to securely download the certificate in PDF or other formats with added user authentication.
* If using DIVOC’s citizen portal, the home screen of the Citizen Portal has a “Download” button in the “Download your Vaccination Certificate” section.  Citizens can click the button and they will be asked to log in using their registered mobile number to download the certificate. To understand how it works, you can check our demo section on [**downloading certificates**](https://divoc.egov.org.in/divoc-demo/citizen-portal#2.-for-downloading-a-certificate).

## Certificate API&#x20;

The DIVOC certificate distribution service provides a get API so that certificates can be downloaded or printed for specific events. For fetching the right certificate, the get service requires a “pre-enrollment code,” and the latest certificate is fetched.

### **How does it work?**

* The get certificate receives the preEnrollmentCode (beneficiary id) as input:&#x20;

{% hint style="info" %}
GET {domain}/certificate/api/certificatePDF/{beneficaryId}
{% endhint %}

* Once it receives the input, it,

1. gets all certificates associated with preEnrollmentCode from the database.
2. gets the latest dose certificate by grouping the certificates by dose, and order\
   them by their timestamps.
3. creates the QR code from signed certificate data.
4. using the above-generated QR code and certificate information, it creates a PDF.

* Similarly, there are APIs in certificate-api service which can return the QR code as a png image, which follows the same step as above (till the third point):

{% hint style="info" %}
GET /certificate/api/certificateQRCode/{beneficaryId}
{% endhint %}

* We also have an API to check if a beneficiary has a certificate generated, which follows the same step as above (till the second point):

{% hint style="info" %}
HEAD  {domain}/certificate/api/certificatePDF/{beneficaryId}
{% endhint %}



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
