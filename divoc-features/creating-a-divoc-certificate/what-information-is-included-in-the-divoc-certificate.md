# What information is included in the DIVOC certificate?

DIVOC’s W3C-based digital certificate consists of three core components:

1. Credential metadata (schema version credential/certificate ID, etc).&#x20;
2. Claim (vaccination event details).&#x20;
3. Proof (issuer details, date of issue, time stamp, signature, etc).

![Credit: Figure taken from W3C Verifiable Credentials Data Model v1.1](<../../.gitbook/assets/Screenshot 2022-01-27 at 10.14.26 AM.png>)

### Data structure

The DIVOC digital certificate QR code includes the following data structure:

| Basic components                                       | Information sections         | Description                                                                                                                    |
| ------------------------------------------------------ | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| <ol><li><strong>Credential metadata</strong></li></ol> | Certificate context          | Sets the context, which establishes the special terms.                                                                         |
|                                                        | Certificate identifier       | Specifies the identifier for the credential.                                                                                   |
|                                                        | Credential type              | Declares what data to expect in the credential.                                                                                |
|                                                        |                              |                                                                                                                                |
| 2. **Claim**                                           | Credential subject           | Assertion about the subjects of the credentials.                                                                               |
|                                                        | Event block                  | When the credential was issued.                                                                                                |
|                                                        | Issuer details               | The entity that issued the credential.                                                                                         |
|                                                        |                              |                                                                                                                                |
| 3. **Proof**                                           | Signature type               | Digital proof that makes the credential tamper-evident. Cryptographic signature suite that was used to generate the signature. |
|                                                        | Date of signature            | When the signature was created.                                                                                                |
|                                                        | Digital signature value      |                                                                                                                                |
|                                                        | Identifier of the public key | That can verify the signature.                                                                                                 |

### Sample certificate payload

To further illustrate the data structure of DIVOC Certificate outputs, a sample certificate payload is outlined below:

![](<../../.gitbook/assets/Screenshot 2022-01-27 at 10.22.11 AM.png>)



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
