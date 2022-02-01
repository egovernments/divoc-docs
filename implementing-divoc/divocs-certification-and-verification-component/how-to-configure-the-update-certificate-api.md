# How to configure the update certificate API

## Overview

This document will help an implementer configure the following service:&#x20;

* Update certificates

## API

* The DIVOC platform provides API services for updating vaccination certificates. You can refer to the API service call ‘​/v3​/certificate’ for the method <mark style="background-color:orange;">PUT</mark> [**here**](https://egovernments.github.io/DIVOC/developer-docs/api/admin-api.html#../../india/interfaces/vaccination-api.yaml).
* The payload of the update service is the same as that of the certificate generation request. Click [**here**](https://divoc.egov.org.in/implementing-divoc/certification-and-verification-component/configuring-certificates) to know more.
* The platform provides flexibility to update values in the ‘recipient,’ ‘vaccination,’ ‘vaccinator,’ and ‘facility’ sections. Click **** [**here**](../../divoc-features/what-information-goes-into-a-qr-code.md) **** if you want to understand the mandatory and non-mandatory information that should be there in a vaccination certificate, according to global standards.

## Key Functionality

* Update the existing certificate along with its QR code.

## Methods: Get details on the API request and field validations:

a. The update certificate request is processed in [**this**](https://github.com/egovernments/DIVOC/blob/main/backend/vaccination\_api/pkg/handler.go#L608) function. The pre-enrollment code and dose-wise certificates will be searched in the system to make an update request. The function will trigger the subsequent process to update the certificates.

```
for _, request := range params.Body {
if certificateId := getCertificateIdToBeUpdated(request); certificateId != nil{
log.Infof("Certificate update request approved %+v", request)
	if request.Meta == nil {
		request.Meta = map[string]interface{}{
			"previousCertificateId": certificateId,
			"certificateType":       CERTIFICATE_TYPE_V3,
		}
	} else {
		meta := request.Meta.(map[string]interface{})
		meta["previousCertificateId"] = certificateId
		meta["certificateType"] = CERTIFICATE_TYPE_V3
	}
	if jsonRequestString, err := json.Marshal(request); err == nil {
		kafkaService.PublishCertifyMessage(jsonRequestString, nil, nil)
	}
} else {
	log.Infof("Certificate update request rejected %+v", request)
	return certification.NewUpdateCertificateV3PreconditionFailed()
}
}
return certification.NewUpdateCertificateV3OK()
```

b. The platform provides the flexibility to restrict the number of update requests to avoid misuse of the functionality in generating multiple certificates.

## Example:

Configure the limit of update certificate requests to only five where the user can only update a certificate five times.

## Steps

**Step 1:** Open [**this**](https://github.com/egovernments/DIVOC/blob/main/backend/vaccination\_api/pkg/handler.go#L660) file and check the function that will limit the number of certificates being updated.

```
if count < (config.Config.Certificate.UpdateLimit + 1) {
  certificateId := doseWiseCertificateIds[int(*request.Vaccination.Dose)][count-1]
	return &certificateId
} else {
	log.Error("Certificate update limit reached")
}
```

**Step 2:** Open [**this**](https://github.com/egovernments/DIVOC/blob/main/backend/vaccination\_api/config/config.go#L78) file and update the limit by configuring <mark style="background-color:yellow;">CERTIFICATE\_UPDATE\_LIMIT</mark>.

```
UpdateLimit int `env:"CERTIFICATE_UPDATE_LIMIT" default:"5"`
```



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
