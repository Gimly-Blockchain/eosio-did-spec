
# Status of This Document
This document is not a W3C Standard nor is it on the W3C Standards Track. This is a draft document and may be updated, replaced or obsoleted by other documents at any time. It is inappropriate to cite this document as other than work in progress.

Comments regarding this document are welcome. Please file issues directly on Github.

// TODO delete me
https://github.com/factom-protocol/FIS/blob/master/FIS/DID.md
https://github.com/decentralized-identity/ethr-did-resolver/blob/master/doc/did-method-spec.md

# 1. Introduction

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


https://github.com/eosio-ecosystem/chains

interoperability

transparency

security

## 1.2 EOSIO accounts

## EOSIO protocol and governance layers

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