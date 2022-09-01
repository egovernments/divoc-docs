# Payload Changes in the QR Code via ETCD CLI

Currently, only the optional fields that already exist can be removed. New fields cannot be added as of now.&#x20;

Note: Do not remove the [**mandatory**](../../../platform/divocs-verifiable-certificate-features/what-information-goes-into-a-qr-code.md) fields.

### Steps to remove an optional field:

Run the command: vim DDCC\_TEMPLATE.template

<figure><img src="../../../.gitbook/assets/Screenshot 2022-09-01 at 2.07.04 PM.png" alt=""><figcaption></figcaption></figure>

To reflect the change, run the command: ./updateConfigs.sh. It shows OK OK OK. This means that the etcd has been updated with the new QR Code template successfully.

<figure><img src="../../../.gitbook/assets/Screenshot 2022-09-01 at 2.07.24 PM.png" alt=""><figcaption></figcaption></figure>



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._  &#x20;
