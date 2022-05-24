# Verifying a DIVOC Certificate

The verification component of the DIVOC certificate service checks for two things:

1. An issued certificate is valid (that is, the document is currently ‘live’ and is not a revoked document).&#x20;
2. The document is authentic (that is, the document has not been tampered with).

## **For verifying authorities**

### **Offline verification:**

DIVOC supports offline verification of the QR code-based digital certificates to support verification of certificates in connectivity restricted regions and make it more user-friendly.&#x20;

The QR code can be verified by third-party authorised verifier applications to enable domestic and cross-border verification of DIVOC-issued certificates.&#x20;

Use the following steps to verify a DIVOC certificate:

1. Scan to detect the QR code.
2. The verification component uses the QR code reader libraries to read the contents of the QR code embedded in the certificate.
3. Once the QR code is detected by the camera, it reads the binary data encoded in the QR code. (the binary data will be in zipped format).
4. The decompressed Json in the QR code is authenticated using a signing method mentioned in the proof section of the QR code content
5. After unzipping it, you will get a certificate.json file (certificate.json will have the signed, json-ld formatted VaccineCertificate).
6. Json-ld signature will be verified against the public key that is issued by the issuing authority.
7. On successful verification, the revoked API is called to check if a certificate has been revoked or not.
8. Once the signature and revocation are verified, the success screen is shown with beneficiary and vaccine details.
9. Since it is offline verification, the verifier will need to download the CRL within the verifier application. The verification service will also go through the CRL and check for the certificate's revoked status.
10. Please note: In addition to supporting verification by third-party verifiers, DIVOC also provides a verification portal. The portal works on a web browser as well as on a mobile phone browser, and it can be also used by verifying authorities to verify DIVOC-certificates in an “offline” capacity.

### **Online verification:**

* DIVOC provides a public portal that allows verifiers (including self-verification by beneficiaries) to verify certificates.
* Certificates can be scanned and verified on the following URL: [**https://demo-divoc.egov.org.in/**](https://demo-divoc.egov.org.in/) **** and clicking on “Verify.”

![](<../.gitbook/assets/Screenshot 2022-02-11 at 4.28.36 PM.png>)

Next,

* Scan the QR code.
* On successful verification, certificate details will be shown on the screen.
* On unsuccessful verification (unauthenticated/fraudulent certificates), the message will be shown as “Certificate Invalid.”

![](<../.gitbook/assets/Screenshot 2022-02-11 at 4.35.16 PM.png>)



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
