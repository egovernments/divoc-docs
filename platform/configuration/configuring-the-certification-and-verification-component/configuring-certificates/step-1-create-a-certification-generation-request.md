# Step 1: Create a certification generation request

## Example

Include the beneficiary’s parent name in the certificate. The parent’s name is “Sam Mandosa”. This is a mandatory field.

## **Steps**

**Step 1: Create a certification generation request**

a. Open this file: [**https://github.com/egovernments/DIVOC/blob/main/backend/vaccination\_api/pkg/certify\_handler.go**](https://github.com/egovernments/DIVOC/blob/main/backend/vaccination\_api/pkg/certify\_handler.go)****

b. Add a parameter in the function “convertToCertifyUploadFields” called RecipientParentName.

```
func convertToCertifyUploadFields(data *Scanner) *db.CertifyUploadFields {
	return &db.CertifyUploadFields{
		PreEnrollmentCode:         data.Text("preEnrollmentCode"),
		RecipientName:             data.Text("recipientName"),
RecipientParentName:        data.Text("recipientParentName"),
		RecipientMobileNumber:  data.Text("recipientMobileNumber"),
		RecipientDOB:              data.Text("recipientDOB"),
		RecipientGender:           data.Text("recipientGender"),
		RecipientNationality:      data.Text("recipientNationality"),
		RecipientIdentity:         data.Text("recipientIdentity"),
		RecipientAge:              data.Text("recipientAge"),
		RecipientAddressLine1:  data.Text("recipientAddressLine1"),
		RecipientAddressLine2:  data.Text("recipientAddressLine2"),
		RecipientDistrict:         data.Text("recipientDistrict"),
		RecipientState:            data.Text("recipientState"),
		RecipientPincode:          data.Text("recipientPincode"),
		VaccinationBatch:          data.Text("vaccinationBatch"),
		VaccinationDate:           data.Text("vaccinationDate"),
		VaccinationDose:           data.Text("vaccinationDose"),
		VaccinationTotalDoses:   data.Text("vaccinationTotalDoses"),
	VaccinationEffectiveStart:data.Text("vaccinationEffectiveStart"),
	VaccinationEffectiveEnd:data.Text("vaccinationEffectiveEnd"),
	VaccinationManufacturer:   data.Text("vaccinationManufacturer"),
		VaccinationName:           data.Text("vaccinationName"),
		VaccinatorName:            data.Text("vaccinatorName"),
		FacilityName:              data.Text("facilityName"),
		FacilityAddressLine1:      data.Text("facilityAddressLine1"),
		FacilityAddressLine2:      data.Text("facilityAddressLine2"),
		FacilityDistrict:          data.Text("facilityDistrict"),
		FacilityState:             data.Text("facilityState"),
		FacilityPincode:           data.Text("facilityPincode"),
	}
}
```

c. Add RecipientParentName in the function “createCertificate” to make the field mandatory.

```
recipient := &models.CertificationRequestRecipient{
		Name: &certifyData.RecipientName,
		Age:  recipientAge,
		Address: &models.CertificationRequestRecipientAddress{
			AddressLine1: &certifyData.RecipientAddressLine1,
			AddressLine2: certifyData.RecipientAddressLine2,
			District:     &certifyData.RecipientDistrict,
			Pincode:      &certifyData.RecipientPincode,
			State:        &certifyData.RecipientState,
		},
		Contact:     contact,
		Dob:         dateAdr(strfmt.Date(dob)),
		Gender:      &certifyData.RecipientGender,
		Nationality: &certifyData.RecipientNationality,
		ParentName: &certifyData.RecipientParentName,
		Identity:    &certifyData.RecipientIdentity,
	}
```

d. If the data is uploaded via CSV, then add this column to the CSV template for this field. Open “[**application-default.yml**](https://github.com/egovernments/DIVOC/edit/main/backend/vaccination\_api/config/application-default.yml)” and update the certificate section in this file.

![](<../../../../.gitbook/assets/Screenshot 2021-12-27 at 9.44.26 AM.png>)

**Note:**

* As a standard practice, we recommend you to update the informative files mentioned in Step 1 of this section.
* Make sure the name matches exactly with the name convertToCertifyUploadFields function that you edited in step 1.

****

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
