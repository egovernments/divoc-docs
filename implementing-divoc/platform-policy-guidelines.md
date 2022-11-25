# Platform Policy Guidelines

## Data backup policy recommendations

The following checklist should be followed for data protection:

* Implement least privilege, restrict users to only data and system information that is required to perform their tasks.
* The full backup of data should be taken once a day:

&#x20;      \- Postgres DB&#x20;

&#x20;      \- Redis cache

&#x20;      \- Kafka&#x20;

&#x20;      \- ETCD

* The full backups are retained for two weeks.
* Incremental backups (hourly) are retained for one day.
* Once the full backup is taken successfully, incremental backups can be purged.
* Backup files will be kept in a separate environment.
* Backup files will be encrypted before storing on another environment/server.

## **Authentication and password management**

Authenticating the identity of a principal and verifying its authorisation to act are foundational controls that other security controls are built upon. Organisations should standardise on an approach to both authentication and authorisation. Consider the following authentication and password management:

* The communication channels need to be encrypted to protect authentication tokens. Use only HTTPS POST/GET requests to transmit authentication credentials.
* All keys, passwords, and certificates must be properly stored and protected.
* Disk level encryption should be implemented.
* All authentication controls must be enforced on a trusted system (such as the server). Partition site by anonymous, identified, and authenticated areas.
* Establish and use standard, tested, authentication services whenever possible.
* Use a centralised implementation for all authentication controls, including libraries that call external authentication services.

## Error handling and logging

Exception handling is a programming concept that allows an application to respond to different error states (such as network down, database connection failure, etc.) in various ways. Handling exceptions and errors correctly are critical to making your code reliable and secure.

Error and exception handling occur in all areas of an application, including critical business logic as well as security features and framework code. Error handling is also important from an intrusion detection perspective. Certain attacks against your application may trigger errors, which can help detect attacks in progress. Consider the following:

* All logging controls should be implemented on a trusted system (such as the server).
* Restrict access to logs to only authorised individuals.
* All the system and system access logs should be enabled.

## **System configuration**&#x20;

The following checklist should be followed for system configurations:

* Ensure servers, frameworks, and system components are running the latest approved version.
* Ensure servers, frameworks, and system components have all patches issued for the version in use.
* Restrict the web server, process, and service accounts to the least privileges possible.
* When exceptions occur, fail securely.
* Remove unnecessary functionality and files.
* Remove test code or any functionality not intended for production, before deployment.
* Remove unnecessary information from HTTP response headers related to the OS, web-server version, and application frameworks.
* Implement a software change control system to manage and record changes to the code/ configuration/scripts in both development and production.



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
