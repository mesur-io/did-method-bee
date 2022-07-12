# did-method-bee - decentralized identifiers for sustainability and regenerative ag

## did:bee - did:🐝 specification 0.1

This is version 0.1 of the mesur.io DID Method Specification for identifying entities in global supply chains, food and agricultural production, and elements related to ESG initiatives

## Introduction

The did:bee method is a did method that is in use for unique identification of digital twins of real world items, locations, and entities, especially for the purposes of identifying items in the global supply chain and items related to ESG compliance and goals.

## Status of This Document

This is a draft document. It may be periodically updated, replaced or removed by other documents at any time.

## DID Document Identififiers

The did:bee method DID identifier has three required components and one optional component that are concatenated to make a did:bee specification conformant identifier. The components are:

- DID: the hardcoded string `did`: to indicate the identifier is a DID
- DID bee method: the hardcoded string `bee` or hex encoded 🐝 `1F41D` that indicates that the identifier uses this DID Method specification.
- DID idstring: a v4 UUID that MUST be unique to the DID document itself
- [OPTIONAL] envrionment: An `envrionment` string MAY be appended, and is used to differentiate differing domains or operational environments.  If an `environment` string is appened it MUST be a FQDN.  If the `envrionment` string is omitted, a default value of `bee.mesur.io` MUST be used by the controller.

The components are assembled as follows:

`did:bee:<idstring>[:<envrionment>]`

examples of valid `bee` DIDs are:

```
did:1F41D:b54399c1-fbec-4aa8-807f-9b7ee057adb0                       # use of emoji
did:bee:990aa5bb-eaa4-43cd-9f51-bcd4f6f2576a                      # default environment
did:bee:990aa5bb-eaa4-43cd-9f51-bcd4f6f2576a:bee.mesur.io         # explicit use of default envrionment
did:bee:e304a73f-c044-475b-860f-7d7b8e9dea4a:bee-test.mesur.io    # an explicit use of a test environment
```

## CRUD Operations

The URL(s) listed in the section below may change in future versions of this document as the service evolves over time. 

### Create

DIDs and DID documents are created upon system or manual discovery of an entity or item that is related to global supply chains, food and agricultural production, and elements related to ESG initiatives

DIDs and DID documents MAY also be created via use of APIs or other services provided as a part of the Earthstream platform, for example with an HTTP POST request to `https://bee.mesur.io/did/{did}`. The request payload of such a POST request is a DID document that matches the DID to be created.

The creator must have the OAuth Scope of `create:dids` for authorization to perform a create operation

### Retrieve

A registered DID may be retrieved by an HTTP GET request against `https://bee.mesur.io/did/{did}`. The result of the query is a DID document that matches the queried DID, if it exists, and if the requestor is authorized to access that DID document

The requestor must have the OAuth Scope of `resolve:dids` for authorization to retrieve a DID document

### Update

A registered DID may be updated by an HTTP PUT request to `https://bee.mesur.io/did/{did}`. The request payload is a DID document that matches the DID to be updated, if it exists, or created if it does not, and if the requestor is authorized to perform that operation

The requestor MUST have the OAuth Scope of `update:dids` for authorization to update a DID document
If the did document does not exist, the requestor MUST also have the OAuth Scope of `create:dids` for authorization to update a DID document

### Delete (Deactivate)

A registered DID may be deleted by an HTTP DELETE request against `https://bee.mesur.io/did/{did}`. The operation will only be performed if the requestor is authorized to perform that operation

The requestor must have the OAuth Scope of `delete:dids` for authorization to retrieve a DID document

## Security Considerations

This section provides the security consideration for the DID method implementation.

- In case of a key compromise, the participant MUST deactivate existing DID immediately.
- Authentication, key storage, encryption in transport, and other security considerations are documented in the [W3C Traceability Interop Specification](https://w3id.org/traceability/interoperability) 
- The DID controller MUST ensure that the application architecture is secure and abides by all industry best practices, especially in regards to fraud, impersonation, and control of critical infrastructure
- The DID controller is responsible for generating and storing keys securely on cryptographic storage such as Hardware Security Module (HSM) in their infrastructure and utilize secure sources of randomness.
- The DID controller MUST ensure that the application is periodically tested according to industry best practices for security vulnerabilities and ensure that no exploitable vulnerabilities are present
- The DID controller SHOULD utilize best practices regarding a secure software supply chain for any libraries or other software components in use
- The DID controller MUST ensure that there is no re-use the same cryptographic material or sources of randomness for multiple purposes.
- The DID controller MUST implement security auditing, logging, and proactive monitoring according to industry best practices

## Privacy Considerations

This section provides the privacy consideration for the did:bee method implementation.

- No personaly identity information may be stored in a DID document.
- The DID controller MUST ensure to protect integrity and confidentiality of user personal data. The DID controller MUST comply with all applicable privacy and data protection laws, regulations and principles as apply to DID controller hosting environment.
- If required, DID controller MUST ensure that necessary security controls are in place to protect user personal data.
- The DID controller MUST ensure that no personal data or personally identifying information is written on any system memory, or log at the system or application level.
- The DID controller MUST have confidentiality protections to prevent surveillance of the content of communications in active or passive manners as well as technical components to protect against surveillance to the best of the DID controller's ability.
- The DID controller MUST comply with the [mesur.io privacy policy](https://mesur.io/privacy)
- The mesur.io Earthstream platform complies with the security and attack surface components as noted in the [W3C Traceability Interop Specification](https://w3id.org/traceability/interoperability)
