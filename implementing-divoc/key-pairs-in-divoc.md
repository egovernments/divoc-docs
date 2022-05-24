# Key Pairs in DIVOC

## Certificate signing

### Supported key types&#x20;

1. RSA (default)&#x20;
2. ED25519 (recommended for performance)

### Environment variable configuration

{% hint style="info" %}
SIGNING\_KEY\_TYPE (possible values: RSA or ED25519)
{% endhint %}

## **Key Pair Configuration**

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



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
