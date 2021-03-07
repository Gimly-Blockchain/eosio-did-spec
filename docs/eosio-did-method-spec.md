
# Status of This Document
This document is not a W3C Standard nor is it on the W3C Standards Track. This is a draft document and may be updated, replaced or obsoleted by other documents at any time. It is inappropriate to cite this document as other than work in progress.

Comments regarding this document are welcome. Please file issues directly on Github.

// TODO delete me
- https://github.com/factom-protocol/FIS/blob/master/FIS/DID.md
- https://github.com/decentralized-identity/ethr-did-resolver/blob/master/doc/did-method-spec.md

# 1. Introduction

## Self Sovereign Identity (SSI)
Self sovereign identity is an evolving Internet architecture for how applications store and process identity data.  It is driven by the need for the need for data privacy over personal information.

The architecture has two layers:
1. Identity - me management of accessible public key infrastructure and identifies. [Decentralized Identifiers](https://w3c.github.io/did-core) is the W3C standard that allows this. Compliance with this standard allows application layers to interoperate without a need to understand the base layer decentralised protocols that power identities.
2. Application - use of the identity layer to interact and provide meaningful, secure and verifiable data communications and interaction. The [Verifiable Credentials](https://w3c.github.io/vc-data-model) W3C standard is the most prominent and adopted standard here which is a data structure and message protocol allowing people and organisations to securely and in a verifiable way send and verify information about themselves "credentials" to each other.

On top of the application layer, use cases in industry can be built which are then interoperable and independent of base protocols. The standards focused heavily on data privacy and security.

More information:
- [SSI Architecture Stack and Community Efforts](https://github.com/decentralized-identity/decentralized-identity.github.io/blob/master/assets/ssi-architectural-stack--and--community-efforts-overview.pdf)

## Decentralized Identfiers
[Decentralized Identifiers](https://w3c.github.io/did-core) (DIDs) provide a standard datamodel to encapsulating unique identifiers and cryptographic material that can be used to interact, verify information from and contact entities. Each decentralised data layer protocol (such as EOSIO, Bitcoin, Hyperledger Indy) creates a DID Method Specification (not a W3C standard) which complies to the DID-core W3C standard. This DID Method Specification specifies the compliance datamodel used by the data protocol to encapsulates a unique identifier and the cryptographic material.

## EOSIO
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

## 1.1 Motivation and rationalle

The EOSIO technology ecosystem has been adopted by approximately 20 public blockchain is and over 100 private blockchains ([source](https://github.com/eosio-ecosystem/chains)). This includes a wide variety of industry applications.

The growing SSI ecosystem is being adopted by industry and governments alike. Decentralised identifiers are the key layer in the SSI tech stack to be included in this ecosystem. EOSIO presents a number of unique advantages for managing self sovereign identity solutions, including its account and key structure and highly flexible governance features. This DID Method Specification allows EOSIO to enter this ecosystem through compliance with the standards, bringing the following benefits:
1. Interoperability with the rest of the SSI ecosystem. This allows EOSIO based identities to be consumed by goverments and industries alike. It provides external interoperability outside of EOSIO.
2. Interoperability with other EOSIO based identities. Due to the large number of EOSIO chains this could be a great way to strengthen the collaboration between all of these projects.
3. Provide transparency of identities through standardisation.
4. Improve security by bringing the SSI architecture model to EOSIO identity systems. This architecture ethically protects human rights while reducing cumbersome data regulation liability from organisations.

## 1.2 EOSIO accounts

The EOSIO account abstraction is unique within the blockchain industry. There are two features relevant for a DID method:
1. Accounts names are not bound to cryptographic material. Accounts names are chosen by the creator of the account, which may or may not be the entity that controls the account. Accounts names are short strings up to 13 characters making them memorisable.
2. Each account can have one or more public-private key pairs which can be used to authorise and asserts data about that account. Keys are organised in a hierarchy tree, with human friendly labels for the permission name. Key material can be delegated to another EOSIO account. A weighted multi'signature scheme can be used. See combination.eosio.json for an example of a typical EOSIO account's key structure that includes both delegated and multi-signature requirements in the heirachial tree.

This key material and structure needs to be expressed in the "verificationMethod" property of the EOSIO DID. Numerous conversations have and are still taking place to create a DID compatible method spec. The result of this has been to create a new [verification method](https://w3c.github.io/did-core/#verification-methods) type called "VerificationCondition" which is currently under construction.

More information:
- [EOSIO Accounts and Permissions](https://developers.eos.io/welcome/latest/protocol-guides/accounts_and_permissions)
- [DID core issue 963: Support for threshold multi-sig verificationMethod](https://github.com/w3c/did-core/issues/693)
- [DID core issue 964: Support for delegated verificationMethods](https://github.com/w3c/did-core/issues/694)
- [DID core issue 965: Support for combination of threshold multi-sig and delegated verificationMethod](https://github.com/w3c/did-core/issues/695)
- [DID core - multisig and delegated use case](https://docs.google.com/presentation/d/1vrmdOnN1tiE54e8h7HyegkJUGyrBUITVFNsAVedUwTE)

## EOSIO protocol and governance layers

The EOSIO protocol is the set of rules within the system cryptographically enforced and historically auditable through a peer to peer network of computer nodes (servers). Fairly unique to the EOSIO protocol is that a large degree of these rules are defined in smart contract that live on the blockchain and can be highly-customised and upgraded over time.

In this way, each EOSIO blockchain can have significantly different rules while staying protocol compatible at the peer to peer network layer.

Account creation and updates to account permissions (keys and delegates) are part of the rules defined through smart contracts. This means that different EOSIO chains will have different [DID method operations](https://w3c.github.io/did-core/#method-operations) (Create, Read, Update, Deactivate). To achive Design goal #1, the EOSIO DID method specification specifies that DID implementations should be generic and provide the default EOSIO method operation CRUD features while also allowing these to be customised (through a constructor or options parameters in function calls).

More information:
- [EOSIO Consensus Protocol](https://developers.eos.io/welcome/latest/protocol-guides/consensus_protocol
)
- [DID core - multisig and delegated use case](https://docs.google.com/presentation/d/1vrmdOnN1tiE54e8h7HyegkJUGyrBUITVFNsAVedUwTE)

# 2. Design goals

Generic all eosio chains. Not support for forks.
Interoperability EOSIO accounts.

# 3. DID Method Schema: did:eosio

2 allowed formats:

## Registered chain name schema
did:eosio:{registered_eosio_name}:{account_name}#{permission_name}
did:eosio:telos:example#owner

eosio did schema name registry + typescript arguments

## Chain id schema
did:eosio:{chain_id}:{account_name}#{permission_name}
did:eosio-f778….e8fe2e:example#active

## DID URLs

### Fragments

permission name
permission.perm_name


## Examples

```
Equivalent DIDs on EOS:
did:eosio:eos:eoscanadacom
did:eosio:aca376f206b8fc25a6ed44dbdc66547c36c6c33e3a119ffbeaef943642f0e906:eoscanadacom

Equivalent DIDs on Telos:
did:eosio:telos:eosio.token
did:eosio:4667b205c6838ef70ff7988f6e8257e8be0e1284a2f59699054a018f743b1d11:eosio.token

DID URL with permission "active"
did:eosio:telos:b1#permisssion.active
```


#permissions

# 5. DID Document

## Identifiers

### DID Subject

### DID Controller

## Verification Methods

type: EOSIOPermission
types for keys k1, r1, wa
https://developers.eos.io/manuals/eosjs/latest/API-Reference/enums/_eosjs_numeric_.keytype

## Verification Relationships

## Services

# 4. Method Operations

## Create

## Read
metadata for permissioned access?

## Update

## Deactivate

# 4. Security considerations
https://trustbloc.github.io/did-method-orb/#security-considerations
https://did-tezos-draft.spruceid.com/#security-considerations

# 5. Privacy considerations
https://trustbloc.github.io/did-method-orb/#privacy-considerations
https://did-tezos-draft.spruceid.com/#privacy-considerations

# Referrences