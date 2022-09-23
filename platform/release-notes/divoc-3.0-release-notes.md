# DIVOC 3.0 Release Notes

## Version release date

* September 19, 2022

## Release summary

The basis of the DIVOC 3.0 release is to move away from COVID-19 vaccination-specific functionality and transition to a more generic verifiable credential generation platform.

## Release features

This platform has the following functionalities:

* **Multi-tenant functionality:** This enables a single installation to support multiple tenants (or source applications that need verifiable credentials to be issued).
* **Ability to onboard a tenant onto the DIVOC platform:** This will onboard an administrator from a tenant and provide credentials to this administrator to do the following:

&#x20;     \- Create a schema. A schema is a list of attributes that need to be certified and part of a verifiable credential.

&#x20;    \- Add a context. Context refers to the public schema which lets the various systems know the structure of a verifiable credential.

&#x20;    \- Create a verifiable credential: The tenant will send an HTTP request to the DIVOC platform to generate the verifiable credential based on the schema.

&#x20;    \- Download a verifiable credential: The platform provides the ability to generate a template using HTML and CSS, and download the verifiable credential based on the template. DIVOC supports multilingual templates. It can also download the QR code instead of a flat file.&#x20;

&#x20;    \- The platform allows the tenant to revoke a certificate.

&#x20;    \- The platform enables the tenant to suspend a certificate for a given period.&#x20;

&#x20;    \- The platform lets the tenant update and delete the verification context, schema, and the verifiable credential itself.

* **Multi-tenancy, authorisation, and authentication:** They are built using KeyCloak (an open source Identity and access management software).



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
