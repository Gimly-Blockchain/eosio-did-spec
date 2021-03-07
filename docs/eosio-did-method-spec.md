
# Status of This Document
This document is not a W3C Standard nor is it on the W3C Standards Track. This is a draft document and may be updated, replaced or obsoleted by other documents at any time. It is inappropriate to cite this document as other than work in progress.

Comments regarding this document are welcome. Please file issues directly on Github.

// TODO delete me
- https://github.com/factom-protocol/FIS/blob/master/FIS/DID.md
- https://github.com/decentralized-identity/ethr-did-resolver/blob/master/doc/did-method-spec.md

# 1. Introduction

## 1.1 Self Sovereign Identity (SSI)
Self sovereign identity is an evolving Internet architecture for how applications store and process identity data.  It is driven by the need for the need for data privacy over personal information.

The architecture has two layers:
1. Identity - me management of accessible public key infrastructure and identifies. [Decentralized Identifiers](https://w3c.github.io/did-core) is the W3C standard that allows this. Compliance with this standard allows application layers to interoperate without a need to understand the base layer decentralised protocols that power identities.
2. Application - use of the identity layer to interact and provide meaningful, secure and verifiable data communications and interaction. The [Verifiable Credentials](https://w3c.github.io/vc-data-model) W3C standard is the most prominent and adopted standard here which is a data structure and message protocol allowing people and organisations to securely and in a verifiable way send and verify information about themselves "credentials" to each other.

On top of the application layer, use cases in industry can be built which are then interoperable and independent of base protocols. The standards focused heavily on data privacy and security.

More information:
- [SSI Architecture Stack and Community Efforts](https://github.com/decentralized-identity/decentralized-identity.github.io/blob/master/assets/ssi-architectural-stack--and--community-efforts-overview.pdf)

## 1.2 Decentralized Identfiers
[Decentralized Identifiers](https://w3c.github.io/did-core) (DIDs) provide a standard datamodel to encapsulating unique identifiers and cryptographic material that can be used to interact, verify information from and contact entities. Each decentralised data layer protocol (such as EOSIO, Bitcoin, Hyperledger Indy) creates a DID Method Specification (not a W3C standard) which complies to the DID-core W3C standard. This DID Method Specification specifies the compliance datamodel used by the data protocol to encapsulates a unique identifier and the cryptographic material.

## 1.3 EOSIO
The EOSIO blockchain platform is the next-generation, open-source platform with industry-leading transaction speed and a flexible utility. As a blockchain platform, EOSIO is designed for enterprise-grade use cases and built for both public and private blockchain deployments. EOSIO is customizable to suit a wide range of business needs across industries with role-based permissions system and secure application transactions processing.

Building distributed applications on EOSIO follows familiar development patterns and programming languages used for developing non-blockchain applications. For application developers, familiarity with the development environment results in a seamless user experience as it allows developers to use their preferred development tools.

The EOSIO platform provides functionalities such as accounts, authentication, databases, asynchronous communication, and the scheduling of applications across multiple CPU cores and clusters. These functionalities are also common in non-blockchain software development environments.

Some of the groundbreaking features of EOSIO include:
1. WebAssembly C++ Compilation
2. High Throughput and Low Latency (0.5s block time)
3. Customizeable Resource Model
4. Efficient and Flexible Persistent Data Indexing
5. Support for Human Friendy Account Names
6. Hierarchical Role Based Transparent Permissions
7. Transparent and Syncronous Smart Contract Upgradability
8. Transparent and Syncronous Protocol Upgradability
9. On-chain Governance
10. Efficient Energy Consumption
11. Webauthn and Biometric Hardware Secured Keys Support

## 1.4 Motivation and rationalle

The EOSIO technology ecosystem has been adopted by approximately 20 public blockchain is and over 100 private blockchains ([source](https://github.com/eosio-ecosystem/chains)). This includes a wide variety of industry applications.

The growing SSI ecosystem is being adopted by industry and governments alike. Decentralised identifiers are the key layer in the SSI tech stack to be included in this ecosystem. EOSIO presents a number of unique advantages for managing self sovereign identity solutions, including its account and key structure and highly flexible governance features. This DID Method Specification allows EOSIO to enter this ecosystem through compliance with the standards, bringing the following benefits:
1. Interoperability with the rest of the SSI ecosystem. This allows EOSIO based identities to be consumed by goverments and industries alike. It provides external interoperability outside of EOSIO.
2. Interoperability with other EOSIO based identities. Due to the large number of EOSIO chains this could be a great way to strengthen the collaboration between all of these projects.
3. Provide transparency of identities through standardisation.
4. Improve security by bringing the SSI architecture model to EOSIO identity systems. This architecture ethically protects human rights while reducing cumbersome data regulation liability from organisations.

## 1.5 EOSIO accounts

The EOSIO account abstraction is unique within the blockchain industry. There are two features relevant for a DID method:
1. Accounts names are not bound to cryptographic material. Accounts names are chosen by the creator of the account, which may or may not be the entity that controls the account. Accounts names are short strings up to 13 characters making them memorisable.
2. Each account can have one or more public-private key pairs which can be used to authorise and asserts data about that account. Keys are organised in a hierarchy tree, with human friendly labels for the permission name. Key material can be delegated to another EOSIO account. A weighted multi'signature scheme can be used. See [combination.eosio.json](https://github.com/Gimly-Blockchain/eosio-did/blob/master/examples/combination.eosio.json) for an example of a typical EOSIO account's key structure that includes both delegated and multi-signature requirements in the heirachial tree.

This key material and structure needs to be expressed in the "verificationMethod" property of the EOSIO DID. Numerous conversations have and are still taking place to create a DID compatible method spec. The result of this has been to create a new [verification method](https://w3c.github.io/did-core/#verification-methods) type called "VerificationCondition" which is currently under construction [here](https://docs.google.com/document/d/1hxEMQxfNuB6Elmd6V-9bEt0kZqSx-DULycn6CjOpMYs/edit).

More information:
- [EOSIO Accounts and Permissions](https://developers.eos.io/welcome/latest/protocol-guides/accounts_and_permissions)
- [DID core issue 963: Support for threshold multi-sig verificationMethod](https://github.com/w3c/did-core/issues/693)
- [DID core issue 964: Support for delegated verificationMethods](https://github.com/w3c/did-core/issues/694)
- [DID core issue 965: Support for combination of threshold multi-sig and delegated verificationMethod](https://github.com/w3c/did-core/issues/695)
- [DID core - multisig and delegated use case](https://docs.google.com/presentation/d/1vrmdOnN1tiE54e8h7HyegkJUGyrBUITVFNsAVedUwTE)

## 1.6 EOSIO protocol and governance layers

The EOSIO protocol is the set of rules within the system cryptographically enforced and historically auditable through a peer to peer network of computer nodes (servers). Fairly unique to the EOSIO protocol is that a large degree of these rules are defined in smart contract that live on the blockchain and can be highly-customised and upgraded over time ([source](https://medium.com/coinmonks/difference-between-eosio-software-and-eos-blockchain-13bcc57d1d9d)).

In this way, each EOSIO blockchain can have significantly different rules while staying protocol compatible at the peer to peer network layer.

Account creation and updates to account permissions (keys and delegates) are part of the rules defined through smart contracts. This means that different EOSIO chains will have different [DID method operations](https://w3c.github.io/did-core/#method-operations) (Create, Read, Update, Deactivate).

To achive Design goal #1, the EOSIO DID method specification implementation SHOULD be generic and provide the default EOSIO method operation CRUD features while also allowing these to be customised by consumers of the implementation (through a constructor or options parameters in function calls). "Implementation" and "consumers" of this implementation will be the terminology used to explain how this design goal is achieved.

More information:
- [EOSIO Consensus Protocol](https://developers.eos.io/welcome/latest/protocol-guides/consensus_protocol
)
- [DID core - multisig and delegated use case](https://docs.google.com/presentation/d/1vrmdOnN1tiE54e8h7HyegkJUGyrBUITVFNsAVedUwTE)

## 1.7 Conformance

The key words MAY, MUST, MUST NOT, OPTIONAL, RECOMMENDED, REQUIRED, SHOULD, and SHOULD NOT in this document are to be interpreted as described in [BCP 14](https://tools.ietf.org/html/bcp14) when, and only when, they appear in all capitals, as shown here.

# 2. Design goals

The design goals of the EOSIO DID Method Specification are to:
1. Create a method spec that can be used for all blockchain powered by the non-modified EOSIO protocol.
2. Support all relevant and non-depreciated features of EOSIO from version 2.0 (time weight permissions are not supported).
3. Support public, private and hybrid permission EOSIO blockchains.
4. Blockchains that have modified the EOSIO protocol are not explicitly supported, but may still be compatible and use this method spec if there have not been any changes to the EOSIO account, permissions and key protocol.

# 3. DID Method Schema: did:eosio

The [DID Method](https://w3c.github.io/did-core/#methods) schema can be consumed in either of the following two formats:
1. Registered chain name schema
2. Chain-id schema

These two methods are mutually exclusive and will not clash with other DID methods as they are prefixed by the `did:eosio` method always. Is useful to have the registered chain name for popular chains that can be easily recognised, as well as a generic hash based identifier for used in the ever expanding ecosystem of many EOSIO blockchains.

These are the properties that make up of the DID:
- `{registered_eosio_eame}` is a pre-registered short name of the EOSIO chain that complies to the [EOSIO account name type](https://developers.eos.io/welcome/latest/protocol-guides/accounts_and_permissions/#21-account-schema) (one to thirdteen lowercase English characters a-z or digits 1-5). This should be registered in the below table and additionally in the [EOSIO DID chain method json registry](https://github.com/Gimly-Blockchain/eosio-did/blob/master/docs/eosio-did-chain-registry.json), including at least one service.
- `{account_ame}` is the name of the account on the chain, also of [EOSIO account name type](https://developers.eos.io/welcome/latest/protocol-guides/accounts_and_permissions/#21-account-schema) type.
- `{chain_id}` is the hash of the genesis block of the chain, expressed in a 64 character string representing a hexidemimal number.

All propertie schemas are provided with a Regex specification.

## 3.1 Registered chain name schema

```
did:eosio:{registered_eosio_name}:{account_name}
registered_eosio_name = ([a-z][1-5]){1,13}
account_name          = ([a-z][1-5]){1,13}
```

e.g. `did:eosio:telos:example`

Registered EOSIO chain summary:

| Registered EOSIO Name | Chain Id |
| ------------- |-------------| 
| eos | aca376f206b8fc25a6ed44dbdc66547c36c6c33e3a119ffbeaef943642f0e906 |
| telos | 4667b205c6838ef70ff7988f6e8257e8be0e1284a2f59699054a018f743b1d11 |


## 3.2 Chain id schema

```
did:eosio:{chain_id}:{account_name}
chain_id = ([a-z][0-9]){64}
account_name= ([a-z][1-5]){1,13}
```

e.g. `did:eosio:4667b205c6838ef70ff7988f6e8257e8be0e1284a2f59699054a018f743b1d11:example`
<br>
(equivalent to `did:eosio:telos:example`)

## 3.3 DID URLs

### 3.3.1 Path

There is no standardised path schema yet, but there could be in the future.

### 3.3.2 Query

There is no standardised query schema yet, but there could be in the future.

### 3.3.3 Fragments

Fragments are used to dereference a DID URL to a specific [verification method](https://w3c.github.io/did-core/#verification-methods). Fragments for the EOSIO DID Method are used to identify the [EOSIO permission name](https://developers.eos.io/welcome/latest/protocol-guides/accounts_and_permissions/#3-permissions) primarily. They can be additionally used to specify sub verification methods within a permission with indexes.

The fragment string must begin with the permission name. You can optionally present indexes to look directly into the permission structure. Indexes are unsigned integers starting at 0.

If a fragment is provided and the permission does not exist in the resolved account, an error MUST be thrown. e.g. `#active` framement for an account with no "active" permission.

If a fragment is provided with indexes which do not exist within the permission of the resolved account, an error MUST be thrown. e.g. `#active-2` framement for an account with an "active" permission that only has one key for authorization (not two).

Fragments can be used with either of the DID methods schemas.

```
did:eosio:{chain_id}:{account_name}#permission_name}-{index_1}-{index_2}-...-{index_N}
did:eosio:{registered_eosio_name}:{account_name}#{permission_name}-{index_1}-{index_2}-...-{index_N}
registered_eosio_name = ([a-z][1-5]){1,13}
chain_id              = ([a-z][0-9]){64}
account_name          = ([a-z][1-5]){1,13}
permission_name       = ([a-z][1-5]){1,13}
index                 = (\d+)
```

e.g. `did:eosio:telos:example#active`
<br>
e.g. `did:eosio:4667b205c6838ef70ff7988f6e8257e8be0e1284a2f59699054a018f743b1d11:example#active`
<br>
(both equivalent)

e.g. `did:eosio:telos:example#active-2-0`
<br>
e.g. `did:eosio:4667b205c6838ef70ff7988f6e8257e8be0e1284a2f59699054a018f743b1d11:example#active-2-0`
<br>
(both equivalent)

# 5. DID Document

## 5.1 Identifiers

As described in the [3. DID Method Schema: did:eosio](#3-DID-Method-Schema-dideosio).

### 5.2 DID Subject

The "subject" property does not need to be specified as it is always equal to the DID.

### 5.3 DID Controller

If the top level EOSIO account permission delegates control to another account, then the DID Document "controller" MUST be the EOSIO DID of that account. e.g. if "example" account has permission "owner" which is delegated to "example2" permission "active" then the DID Document would contain:

```json
{
    "id": "did:eosio:telos:example:owner",
    "controller": "did:eosio:telos:example2:active",
}
```

If the top level EOSIO account permission contains multiple authorisation mechanisms including but not exclusively a delegation to another account, then the DID Document "controller" MAY be the EOSIO DID of that account.

If the top level EOSIO account permission does delegates control to another account, then the DID Document "controller" MUST be the same as the DID.

**QUESTION: Is this right?**

## 5.2 Verification Methods

**TODO see [Verification Conditions](https://docs.google.com/document/d/1hxEMQxfNuB6Elmd6V-9bEt0kZqSx-DULycn6CjOpMYs)**

**TODO key types: k1, r1, wa https://developers.eos.io/manuals/eosjs/latest/API-Reference/enums/_eosjs_numeric_.keytype**

## 5.3 Verification Relationships

The way in which EOSIO account permissions are used is not specified in the protocol and cannot be extracted from the EOSIO blockchain. It is expected that applications that consume an EOSIO DID Method implementation will know more information about how the verification methods are used. This also applies to specific blockchains that consume the implementations.

Consumers of the EOSIO DID Method implementation are RECOMMENDED to extend the DID Document's verification relationships with lists of fragments that point to verification methods adequate for relationships.

## 5.4 Services

At least one service SHOULD exist on a DID Document of LinkedDomains type. This can be used to resolve the DID and connect to the EOSIO chain through a supported API.

Registered EOSIO chain names should add at least one servic in the [EOSIO DID chain method json registry](https://github.com/Gimly-Blockchain/eosio-did/blob/master/docs/eosio-did-chain-registry.json).

**QUESTION: should we and how can we specify the EOSIO chain protocol version support of the DID? e.g. is the chain 2.0 or 2.4 or 1.8 compatible...**

### 5.4.1 Service Types

Multiple different APIs exist within the EOSIO ecosystem.
1. [Nodeos HTTP API](https://developers.eos.io/manuals/eos/latest/nodeos/plugins/chain_api_plugin/api-reference/index) - default provided by Block One, author of EOSIO
2. [Dfuse](https://dfuse.io) - provides websocket connection and history search features
3. [Hyperion](https://hyperion.docs.eosrio.io) - provides history search features
4. [EOSIO Light API](https://github.com/cc32d9/eosio_light_api) - provides history search features

A [service type](https://w3c.github.io/did-spec-registries/#service-types) MUST be provided to describe the type for services related to access and transaction of an EOSIO blockchain.

| API Name | Service type |
| ------------- |-------------| 
| Nodeos| EosioNodeos |
| Dfuse Http Rest API | EosioDfuseRest |
| Dfuse Websocket API | EosioDfuseWebsocket |
| Hyperion | EosioHyperion |
| EOSIO Light API | EosioLightAPI |

See the [EOSIO DID chain method json registry](https://github.com/Gimly-Blockchain/eosio-did/blob/master/docs/eosio-did-chain-registry.json) for examples.

**QUESTION: What is the "id" property of a service, what should we put?**

## 5.1 Example DID Document

**TODO key type Ed25519VerificationKey and publicKeyBase58 need to be checked.**

### 5.1.1 Simple account
```json
{
    "@context": ["https://www.w3.org/ns/did/v1", 
        "https://raw.githubusercontent.com/Gimly-Blockchain/eosio-did/master/docs/eosio-did-context.json"],
    "id": "did:eosio:telos:example",
    "verificationMethod": [{
        "id": "did:eosio:telos:example#owner",
        "controller": "did:eosio:telos:example",
        "type": "Ed25519VerificationKey",
        "publicKeyBase58": "7idX86zQ6M3mrzkGQ9MGHf4btSECmcTj4i8Le59ga7CpSpZYy5"
    }, {
        "id": "did:eosio:telos:example#active",
        "controller": "did:eosio:telos:example",
        "type": ["VerificationMethod", "VerificationConditionParent"],
        "parentIdUrl": "did:eosio:telos:example#owner",
        "verificationMethod": {
            "id": "did:eosio:telos:example#active-0",
            "controller": "did:eosio:telos:example",
            "type": "Ed25519VerificationKey",
            "publicKeyBase58": "7NFuBesBKK5XHHLtzFxm7S57Eq11gUtndrsvq3Mt3XZNMTHfqc"
        }
    }]
}
```

### 5.1.2 Multi-sig delegated account
```json
{
    "@context": ["https://www.w3.org/ns/did/v1",
        "https://raw.githubusercontent.com/Gimly-Blockchain/eosio-did/master/docs/eosio-did-context.json"],
    "id": "did:eosio:telos:example",
    "verificationMethod": [{
        "id": "did:eosio:telos:example#owner",
        "controller": "did:eosio:telos:example",
        "type": ["VerificationMethod", "VerificationConditionWeightedThreshold"],
        "threshold": 3,
        "verificationMethod": [{
                "weight": 1,
                "verificationMethod": {
                    "id": "did:eosio:telos:example#owner-0",
                    "controller": "did:eosio:telos:example",
                    "type": "Ed25519VerificationKey",
                    "publicKeyBase58": "7idX86zQ6M3mrzkGQ9MGHf4btSECmcTj4i8Le59ga7CpSpZYy5"
                }
            }, {
                "weight": 2,
                "verificationMethod": {
                    "id": "did:eosio:telos:example#owner-1",
                    "controller": "did:eosio:telos:example",
                    "type": "Ed25519VerificationKey",
                    "publicKeyBase58": "7G5AXPP4RNG5DiZACneMZVenYEQ2GmVwcYUis8YrFHorQic5h8"
                }
            }, {
                "weight": 2,
                "verificationMethod": {
                    "id": "did:eosio:telos:example#owner-2",
                    "controller": "did:eosio:telos:example",
                    "type": ["VerificationMethod", "VerificationConditionWeightedThreshold"],
                    "delegatedIdUrl": "did:eosio:telos:example2#active"
                }
            } 
        ]
    }, {
        "id": "did:eosio:telos:example#active",
        "controller": "did:eosio:telos:example",
        "type": ["VerificationMethod", "VerificationConditionParent"],
        "parentIdUrl": "did:eosio:telos:example#owner",
        "verificationMethod": {
            "id": "did:eosio:telos:example#active-0",
            "controller": "did:eosio:telos:example",
            "type": ["VerificationMethod", "VerificationConditionWeightedThreshold"],
            "threshold": 1,
            "verificationMethod": [{
                    "weight": 1,
                    "verificationMethod": {
                        "id": "did:eosio:telos:example#active-0-0",
                        "controller": "did:eosio:telos:example",
                        "type": "Ed25519VerificationKey",
                        "publicKeyBase58": "7NFuBesBKK5XHHLtzFxm7S57Eq11gUtndrsvq3Mt3XZNMTHfqc"
                    }
                }
            ]
        }
    }]
}
```

# 4. Method Operations

## 4.1 Create

EOSIO accounts are created with an on-chain transaction. The default is to call the ["newaccount" action](https://github.com/EOSIO/eosio.contracts/blob/52fbd4ac7e6c38c558302c48d00469a4bed35f7c/contracts/eosio.system/include/eosio.system/native.hpp#L178) on the system contract from an existing account on the blockchain. This action can be changed on each EOSIO chain, and upgraded over time. For some EOSIO systems, the on-chain account creation process is not openly accessible, and uses will use a different mechanism (such as an email and password request to an organisation) to create an account.

Implementations of the EOSIO DID Method SHOULD implement the create operation according to the default ["newaccount" action](https://github.com/EOSIO/eosio.contracts/blob/52fbd4ac7e6c38c558302c48d00469a4bed35f7c/contracts/eosio.system/include/eosio.system/native.hpp#L178) defined in the eosio.bios contract. This function SHOULD be polymorphic and can be overridden by a consumer of the implementation. It is recommended that the EOSIO DID implementation constructor, or an options parameter can be used to achieve this.

Consumers of a EOSIO DID Method implementation SHOULD override the default create behaviour if a different mechanism exists to create an EOSIO DID.

## 4.2 Read

Resolution of a DID Document can be done by a service API. This may be an authorised or rate limited API. There are different types of EOSIO APIs as outlined in [Service Types](#541-Service-Types).

**Question: should include description of metadata needed for authorized (permissioned) read access with private chains in mind?**

## 4.3 Update

EOSIO account's permissions are updated with an on-chain transaction. The default is to call the ["updateauth" action](https://github.com/EOSIO/eosio.contracts/blob/52fbd4ac7e6c38c558302c48d00469a4bed35f7c/contracts/eosio.system/include/eosio.system/native.hpp#L194) on the system contract from your account. This action be changed on each EOSIO chain, and upgraded over time.

Implementations of the EOSIO DID Method SHOULD implement the update operation according to the default ["updateauth" action](https://github.com/EOSIO/eosio.contracts/blob/52fbd4ac7e6c38c558302c48d00469a4bed35f7c/contracts/eosio.system/include/eosio.system/native.hpp#L194) defined in the eosio.bios contract. This function SHOULD be polymorphic and can be overridden by a consumer of the implementation. It is recommended that the EOSIO DID implementation constructor, or an options parameter can be used to achieve this.

Consumers of a EOSIO DID Method implementation SHOULD override the default update behaviour if a different mechanism exists to update an EOSIO DID.

## 4.4 Deactivate

EOSIO blockchains do not have a default mechanism to deactivate accounts.

Implementations of the EOSIO DID Method SHOULD implement a deactivate function which throws an error. This function SHOULD be polymorphic and can be overridden by a consumer of the implementation. It is recommended that the EOSIO DID implementation constructor, or an options parameter can be used to achieve this.

Consumers of a EOSIO DID Method implementation SHOULD override the default update behaviour if a different mechanism exists to deactivate an EOSIO DID.

# 5. Security considerations
https://trustbloc.github.io/did-method-orb/#security-considerations
https://did-tezos-draft.spruceid.com/#security-considerations

Consideration of privledged accounts on chain which have the power to control account permissions.

# 6. Privacy considerations
https://trustbloc.github.io/did-method-orb/#privacy-considerations
https://did-tezos-draft.spruceid.com/#privacy-considerations