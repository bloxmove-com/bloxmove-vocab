# Vocabulary for Verifiable Credentials in the bloXmove platform

Editors:

- Harry Behrens ([bloXmove](https://bloxmove.com))
- Hartmut Obendorf ([Chainstep GmbH](https://chainstep.com))
- Jan-Paul Buchwald ([51 Nodes](https://51nodes.io))

Authors:

- Kevin Kuhfeldt ([Chainstep GmbH](https://chainstep.com))

## Status of this Document

This document is a preliminary draft.

## Introduction

THe bloXmove platform uses [Verifiable Credentials](https://www.w3.org/TR/vc-data-model/) for communication
betweeen participants. This document describes the types of credentials and their respective subjects.

The machine-readable form of this description is using [JSON-LD](https://json-ld.org/) format and can be found [here](https://raw.githubusercontent.com/bloxmove-com/bloxmove-vocab/master/v1-draft).

## IdentityCredential

The IdentityCredential is used by a user-participant of the bloXmove platform when
interacting with a service that requires a verifiable identity for operation.

| CredentialSubject Field | Description                                                    |
| ----------------------- | -------------------------------------------------------------- |
| id                      | ID (DID) of the participant                                    |
| minAge18                | true if the participant is at least 18 years of age (optional) |
| minAge21                | true if the participant is at least 21 years of age (optional) |
| minAge25                | true if the participant is at least 25 years of age (optional) |
| identifier              | ID of the document source for the credential (optional)        |
| familyName              | family name of the participant (optional)                      |
| givenName               | given name of the participant (optional)                       |
| birthCountry            | birth country of the participant (optional)                    |
| birthDate               | birth date of the participant (optional)                       |
| age                     | age of the participant (optional)                              |
| streetAddress           | street address of the participant (optional)                   |
| postalCode              | postal code of the participant (optional)                      |
| country                 | country of residence of the participant (optional)             |
| validUntil              | date until the credential is valid (optional)                  |
| issueDate               | date when the credential was issued (optional)                 |
| issuerName              | name of the entity issuing the credential (optional)           |

Example credential:

```
{
    "credential": {
        "@context": [
            "https://www.w3.org/2018/credentials/v1",
            "https://raw.githubusercontent.com/bloxmove-com/bloxmove-vocab/master/v1-draft"
        ],
        "type": [
            "VerifiableCredential",
            "IdentityCredential"
        ],
        "issuer": {
            "id": "did:web:doorman-pre-prod.wallet.eu.spherity.io:uuid:4f7d2251f7c34e829971a1ad8c41c6d2"
        },
        "issuanceDate": "2020-03-10T04:24:12.164Z",
        "expirationDate": "2022-03-10T04:24:12.164Z",
        "credentialSubject": {
            "id": "did:web:doorman-pre-prod.wallet.eu.spherity.io:uuid:3ac0fcd36f0a42878d2c108314ddd45c",
            "minAge18": true,
            "minAge21": true,
            "minAge25": true,
            // additional attributes for the id card
            "identifier": "U7SB2WKX",
            "familyName": "Max",
            "givenName": "Mustermann",
            "birthCountry": "Austria",
            "birthDate": "1636992690647",
            "age": 29,
            // alternatively "yearOfBirth": "1976",
            // not required IMO "image": "asdoiou adiiodasiDOHDISAHDOIDIODSaodiAiodhsöIHDöaoshdas)=(/DA=DOZPB§)(R§)(b79e8bb0BZD/)ADSAODODpi",
            // not required IMO "gender": "female",
            "streetAddress": "Bergweg 2",
            "postalCode": "80889",
            "country": "Germany",
            "validUntil": "1636992690647",
            "issueDate": "1636992690647",
            "issuerName": "Stadt Bonn"
        }
    },
    "options": {
        "type": "Ed25519Signature2018",
        "issuer": "did:web:doorman-pre-prod.wallet.eu.spherity.io:uuid:4f7d2251f7c34e829971a1ad8c41c6d2"
    }
}
```

## DrivingLicenseCredential

The DrivingLicenseCredential is used by a user-participant of the bloXmove platform when
reserving or booking a vehicle that requires a driving license for operation.

| CredentialSubject Field | Description                                                    |
| ----------------------- | -------------------------------------------------------------- |
| id                      | ID (DID) of the participant                                    |
| validDrivingLicense     | true if a valid driving license for the participant was issued |
| identifier              | ID of the document source for the credential (optional)        |
| validUntil              | date until the credential is valid (optional)                  |
| issueDate               | date when the credential was issued (optional)                 |
| issuerName              | name of the entity issuing the credential (optional)           |

Example credential:

```
{
    "credential": {
        "@context": [
            "https://www.w3.org/2018/credentials/v1",
            "https://raw.githubusercontent.com/bloxmove-com/bloxmove-vocab/master/v1-draft"
        ],
        "type": [
            "VerifiableCredential",
            "DrivingLicenseCredential"
            ],
        "issuer": {
            "id": "did:web:doorman-pre-prod.wallet.eu.spherity.io:uuid:4f7d2251f7c34e829971a1ad8c41c6d2"
        },
        "issuanceDate": "2020-03-10T04:24:12.164Z",
        "expirationDate": "2022-03-10T04:24:12.164Z",
        "credentialSubject": {
            "id": "did:web:doorman-pre-prod.wallet.eu.spherity.io:uuid:3ac0fcd36f0a42878d2c108314ddd45c",

            "validDrivingLicense": true,
            "identifier": "HUJNZT52Y",
            "validUntil": "1636992690647",
            "issueDate": "1636992690647",
            "issuerName": "Stadt Bonn",
        }
    },
    "options": {
        "type": "Ed25519Signature2018",
        "issuer": "did:web:doorman-pre-prod.wallet.eu.spherity.io:uuid:4f7d2251f7c34e829971a1ad8c41c6d2"
    }

}
```

## TopicCredential

The TopicCredential is used by a user-participant or agent-participant of the bloXmove
platform when requesting an action from a service that requires a verifiable credential
proving the request on this topic is authentic.

| CredentialSubject Field | Description                                           |
| ----------------------- | ----------------------------------------------------- |
| id                      | ID (DID) of the participant                           |
| vehicleDID              | DID of the vehicle subject of the request (optional)  |
| contractDID             | DID of the contract subject of the request (optional) |
| topic                   | string describing the request                         |

Example credential:

```
{
    "credential": {
        "@context": [
            "https://www.w3.org/2018/credentials/v1",
            "https://raw.githubusercontent.com/bloxmove-com/bloxmove-vocab/master/v1-draft"
        ],
        "type": [
            "VerifiableCredential",
            "TopicCredential"
        ],
        "issuer": {
            "id": "did:web:doorman-pre-prod.wallet.eu.spherity.io:uuid:4f7d2251f7c34e829971a1ad8c41c6d2"
        },
        "issuanceDate": "2020-03-10T04:24:12.164Z",
        "expirationDate": "2022-03-10T04:24:12.164Z",
        "credentialSubject": {
            "id": "did:web:doorman-pre-prod.wallet.eu.spherity.io:uuid:3ac0fcd36f0a42878d2c108314ddd45c",

            "vehicleDID": "did:eth:0x3089247237312984731289473298",
            "contractDID": "did:eth:0x3089247237312984731289473298",
            "topic": "/confirmBooking",

        }
    },
    "options": {
        "type": "Ed25519Signature2018",
        "issuer": "did:web:doorman-pre-prod.wallet.eu.spherity.io:uuid:4f7d2251f7c34e829971a1ad8c41c6d2"
    }
}
```
