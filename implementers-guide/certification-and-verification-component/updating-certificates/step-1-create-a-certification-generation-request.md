# Step 1: Create a certification generation request

## Example

Include the beneficiary’s parent name in the certificate. The parent’s name is “Sam Mandosa”. This is a mandatory field.

## **Steps**

**Step 1: Create a certification generation request**

a. Open this file: [**https://github.com/egovernments/DIVOC/blob/main/backend/vaccination\_api/pkg/certify\_handler.go**](https://github.com/egovernments/DIVOC/blob/main/backend/vaccination\_api/pkg/certify\_handler.go)****

b. Add a parameter in the function “convertToCertifyUploadFields” called RecipientParentName.

![](<../../../.gitbook/assets/Screenshot 2021-12-27 at 9.06.46 AM.png>)

c. Add RecipientParentName in the function “createCertificate” to make the field mandatory.

![](<../../../.gitbook/assets/Screenshot 2021-12-27 at 9.15.04 AM.png>)

d. If the data is uploaded via CSV, then add this column to the CSV template for this field. Open “[**application-default.yml**](https://github.com/egovernments/DIVOC/edit/main/backend/vaccination\_api/config/application-default.yml)” and update the certificate section in this file.

{% file src="../../../.gitbook/assets/Screenshot 2021-12-27 at 9.18.06 AM.png" %}



****



****

****
