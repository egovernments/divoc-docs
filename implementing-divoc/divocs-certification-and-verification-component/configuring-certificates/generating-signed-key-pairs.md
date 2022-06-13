# Generating Signed Key Pairs

## Certificate signing

### Supported key types&#x20;

1. RSA (default)&#x20;
2. ED25519 (recommended for performance)

### Environment variable configuration

{% hint style="info" %}
SIGNING\_KEY\_TYPE (possible values: RSA or ED25519)
{% endhint %}

## **Key Pair Configuration for DIVOC certificate**

### Environment variables

{% hint style="info" %}
CERTIFICATE\_SIGNER\_PRIVATE\_KEY, CERTIFICATE\_SIGNER\_PUBLIC\_KEY
{% endhint %}

The expected values for these configurations change depending on the type of key in use:

### RSA**:**&#x20;

* Private Key Format: 2048 bit, PEM
* Public key format: PEM&#x20;

### ED25519:

| Key     | Format | Type   | Encoding |
| ------- | ------ | ------ | -------- |
| Private | DER    | PKCS#8 | Base58   |
| Public  | DER    | SPKI   | Base58   |

## **Reference steps for key generation**

### **RSA key generation using openssl**

{% hint style="info" %}
openssl genrsa -out privatekey.pem 2048
{% endhint %}

{% hint style="info" %}
openssl rsa -in privatekey.pem -out publickey.pem -pubout -outform PEM
{% endhint %}

### **ED25519**

Use an external library such as **** [**ed25519-verification-key-2018**](https://github.com/digitalbazaar/ed25519-verification-key-2018/) **** to **** [**generate**](https://github.com/digitalbazaar/ed25519-verification-key-2018#generating-a-new-publicprivate-key-pair) **** a key-pair in the required format.



## **Key Pair Configuration for EU certificate**

### Generation of Key pair for signing the EU certificate&#x20;

* Copy the certificate generation script file [gen-dsc.sh](https://github.com/egovernments/DIVOC/blob/main/scripts/gen-dsc.sh) **** and put it in the desired location&#x20;
* Copy the certificate configuration file [cert.conf](https://github.com/egovernments/DIVOC/blob/main/scripts/cert.conf) and put it in the same folder where certificate generation script is copied
* Open the cert.conf file and edit it according to your requirement.&#x20;

| **C - Country Name (2 letter code)**              | The two-letter country code where your company is legally located.                                              |
| ------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **ST - State or Province Name (full name)**       | The state/province where your company is legally located.                                                       |
| **L - Locality Name (e.g., city)**                | The city where your company is legally located.                                                                 |
| **O - Organization Name (e.g., company)**         | Your company's legally registered name (e.g., YourCompany, Inc.).                                               |
| **OU - Organizational Unit Name (e.g., section)** | The name of your department within the organization. (You can leave this option blank; simply press \*Enter\*.) |
| **CN - Common Name (e.g., server FQDN)**          | The fully-qualified domain name (FQDN) (e.g., [http://www.example.com](http://www.example.com) ).               |

* &#x20;Run the [gen-dsc.sh](https://github.com/egovernments/DIVOC/blob/main/scripts/gen-dsc.sh) file to generate the key pair for signing the EU certificate
* For generation of RSA key pair - `./gen-dsc.sh RSA CSR`&#x20;
* For generation of ECDSA key pair - `./gen-dsc.sh ECDSA CSR`
* The script will generate following 3 files:

1. _private key filename - DSC01privkey.key_&#x20;
2. _CSR filename - DSC01csr.pem CERTIFICATE key filename - DSC01cert.pem_
3. _Public key format: PEM_

### **Configuring EU certificate retrieval from certificate-api service**

1. Generate key pair required for signing the EU certificate and Share the CSR file for signing with CA&#x20;
2. In the `divoc-config` configMap set the following environment variables:&#x20;

* `EU_CERTIFICATE_PRIVATE_KEY`  - private key for signing EU payload (in PKCS8 format)
* `EU_CERTIFICATE_PUBLIC_KEY`  - certificate provided by CA after signing the CSR
* `EU_CERTIFICATE_EXPIRY`  - expiry of certificate in months (for ex - 12)



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
