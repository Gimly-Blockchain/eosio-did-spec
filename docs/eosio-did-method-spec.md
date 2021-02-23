
# Status of This Document
This document is not a W3C Standard nor is it on the W3C Standards Track. This is a draft document and may be updated, replaced or obsoleted by other documents at any time. It is inappropriate to cite this document as other than work in progress.

Comments regarding this document are welcome. Please file issues directly on Github.

# 1. Introduction

## 1.1 Motivation and rationalle

https://github.com/eosio-ecosystem/chains

interoperability

transparency

security

## EOSIO general


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


## Examples

```
Equivalent DIDs on EOS:
did:eosio:eos:eoscanadacom
did:eosio:aca376f206b8fc25a6ed44dbdc66547c36c6c33e3a119ffbeaef943642f0e906:eoscanadacom

Equivalent DIDs on Telos:
did:eosio:telos:eosio.token
did:eosio:4667b205c6838ef70ff7988f6e8257e8be0e1284a2f59699054a018f743b1d11:eosio.token
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

# 5. Privacy considerations

# Referrences