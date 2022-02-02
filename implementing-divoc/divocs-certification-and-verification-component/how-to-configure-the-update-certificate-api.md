# How to configure the update certificate API

## Overview

This section will help an implementer configure the DIVOC “Update Certificate” API.

## Intended output&#x20;

* Implementers can use the “Update Certificate” API to process the requested updates - both in the QR code and human-readable sections of a specific certificate.

## API

* The DIVOC platform provides API services for updating vaccination certificates. You can refer to the API service call ‘​/v3​/certificate’ for the method <mark style="background-color:orange;">PUT</mark> [**here**](https://egovernments.github.io/DIVOC/developer-docs/api/admin-api.html#../../india/interfaces/vaccination-api.yaml).
* The payload of the update service is the same as that of the certificate generation request. Click [**here**](https://divoc.egov.org.in/implementing-divoc/certification-and-verification-component/configuring-certificates) to know more.
* The platform provides flexibility to update values in the ‘**recipient**,’ ‘**vaccination**,’ ‘**vaccinator**,’ and ‘**facility**’ sections. Click **** [**here**](../../divocs-verifiable-certificate-features/what-information-goes-into-a-qr-code.md) **** if you want to understand the mandatory and non-mandatory information that should be there in a vaccination certificate, according to global standards.

## Methods - Get details on the API request and field validations:

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

b. An implementer has the provision to restrict the number of update requests against a specific certificate in order to avoid the misuse of this functionality (i.e. fraudulent generation of multiple certificate copies). For instance, the implementer can configure the “Update Limit” to only “5,” in which case the certificate can only be updated five times. The following steps are needed to enable this configuration:

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
