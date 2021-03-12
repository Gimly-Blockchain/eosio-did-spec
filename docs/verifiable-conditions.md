# Status of This Document
This document is not a W3C Standard nor is it on the W3C Standards Track. This is a draft document and may be updated, replaced or obsoleted by other documents at any time. It is inappropriate to cite this document as other than work in progress.

Comments regarding this document are welcome. Please file issues and PRs directly on Github.

Editors:
- Jack Tanner, Blockchain and SSI Developer | Gimly jack@gimly.io

# Abstract

// TODO

# Introduction

// TODO
DID 
DID verificationMethod type

Prior work:
- [Verifiable Conditions planning doc](https://docs.google.com/document/d/1hxEMQxfNuB6Elmd6V-9bEt0kZqSx-DULycn6CjOpMYs) - several VerifiableCondition types have not been added to this draft, see conversation and if you think they are important please submit an issue or PR to add
- [DID core - multisig and delegated use case](https://docs.google.com/presentation/d/1vrmdOnN1tiE54e8h7HyegkJUGyrBUITVFNsAVedUwTE)

## Goals
Create a new verification method type that can:
- Express conditional logic required to validate verification methods
- Express additional metadata about verification methods

## Use Cases

Support for account and key models of the following protocols:
- EOSIO: [Accounts And Permissions](https://developers.eos.io/welcome/latest/protocol-guides/accounts_and_permissions)
- Hyperledger Fabric: [Endorsement policies](https://hyperledger-fabric.readthedocs.io/en/latest/developapps/endorsementpolicies.html?highlight=endorsement%20policy)
- Ripple and BigchainDB: [Composable cryptographic conditionals](https://github.com/rfcs/crypto-conditions)
- KERI: [keripy/blob/master/tests/core/test_coring.py](https://github.com/decentralized-identity/keripy/blob/master/tests/core/test_coring.py#L2523)
- Hyperledger Indy: [Indy DID Method](https://hackmd.io/@icZC4epNSnqBbYE0hJYseA/S1eUS2BQw)

# The VerifiableCondition Type

```json
{
    "id": "did:example:123#owner",
    "controller": "did:example:123",
    "type": ["VerifiableCondition", "VerifiableConditionAnd"],
    "verificationMethod": {},
}
```

// TODO

The “verificationMethod” property is a singular or array value of other verification methods. These can be any valid type including other VerifiableCondition types. In this way, a recursive structure of infinite complexity can be expressed about the cryptographic material required.

The “verificationMethod” can use a [relative DID URL](https://w3c.github.io/did-core/#relative-did-urls) to link to other “verificationMethod”s to avoid duplication in the same DID Document.

## Example
This would check that the signatures match AND( OR( #1-1-1, #1-1-2), #1-2). Note the different types.

```json
{
    "id": "did:example:123#1",
    "controller": "did:example:123",
    "type": ["VerifiableCondition", "VerifiableConditionAnd"],
    "verificationMethod": [{
        "id": "did:example:123#1-1",
        "controller": "did:example:123",
        "type": ["VerifiableCondition", "VerifiableConditionOr"],
        "verificationMethod": [{
            "id": "did:example:123#1-1-1",
            "controller": "did:example:123",
            "type": "EcdsaSecp256k1VerificationKey2019",
            "publicKeyBase58": "5JBxKqYKzzoHrzeqwp6zXk8wZU3Ah94ChWAinSj1fYmyJvJS5rT"
        }, {
            "id": "did:example:123#1-1-2",
            "controller": "did:example:123",
            "type": "Ed25519VerificationKey2018",
            "publicKeyBase58": "PZ8Tyr4Nx8MHsRAGMpZmZ6TWY63dXWSCzamP7YTHkZc78MJgqWsAy"
        }]
    }, {
        "id": "did:example:123#1-2",
        "controller": "did:example:123",
        "type": "Ed25519VerificationKey2018",
        "publicKeyBase58": "H3C2AVvLMv6gmMNam3uVAjZpfkcJCwDwnZn6z3wXmqPV"
    }]
}
```


# Subtypes of VerifiableCondition

## And
```json
{
    "id": "did:example:123#1",
    "controller": "did:example:123",
    "type": ["VerifiableCondition", "VerifiableConditionAnd"],
    "verificationMethod": []
}
```

Fulfilled if all of the verificationMethods provided are fulfilled.

Note: this subtype can be expressed through a Threshold subtype by setting the “threshold” property to the the number of verificationMethods.

## Threshold
```json
{
    "id": "did:example:123#4",
    "controller": "did:example:123",
    "type": ["VerifiableCondition", "VerifiableConditionThreshold"],
    "threshold": 3,
    "verificationMethod": [],
}
```

Fulfilled if the number of verificationMethods that are fulfilled are greater than or equal to the “threshold” property.

Note: this subtype can be expressed through a WeightedThreshold subtype by setting all the “weight” properties to 1.

## WeightedThreshold
```json
{
    "id": "did:example:123#5",
    "controller": "did:example:123",
    "type": ["VerifiableCondition", "VerifiableConditionWeightedThreshold"],
    "threshold": 3,
    "verificationMethod": [{
        "verificationMethod": {},
        "weight": 2
    }, {
        "verificationMethod": {},
        "weight": 2
    }, {
        "verificationMethod": {},
        "weight": 1
    }]
}
```

Fulfilled if the sum of the weights of the verificationMethods that are fulfilled are greater than or equal to the “threshold” property.

## Delegated
```json
{
    "id": "did:example:123#10",
    "controller": "did:example:123",
    "type": ["VerifiableCondition", "VerifiableConditionDelegated"],
    "delegatedIdUrl": ""
}
```

Fulfilled if the verificationMethod found by dereferencing the DID URL “delegatedIdUrl” is fulfilled. The dereferenced DID document MUST contain a verificationMethod found using the DID URL. The dereferenced DID document MUST NOT contain multiple verificationMethods found using the DID URL.

## Relationship
```json
{
    "id": "did:example:123#10",
    "controller": "did:example:123",
    "type": ["VerifiableCondition", "VerifiableConditionRelationship"],
    "parentIdUrl": [],
    "childIdUrl": [],
    "siblingIdUrl": [],
}
```

Has not fulfillment requirements.

Expresses a relationship between different verificationMethods. One of the properties "parentIdUrl", "childIdUrl" or "siblingIdUrl" MUST be present. Each property can be a DID URL or an array of DID URLs.

# Privacy Considerations

# Security Considerations

