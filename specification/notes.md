# Notes

This page is not cannonical. It is intended to capture ideas that may eventually
be reflected in the specification before they have been vetted sufficiently for
inclusion.

---

- Logical similarity to OpenID Connect is desirable
- ID tokens must be self-issued by the identified person using keys they
  control, as attested to by what I'm currently calling notaries: witnesses that
  verify the identity of the user and the public key is related to a private key
  proveably controlled by the user. It may be the case that new one-time use
  public keys are generated for each token.
- the actual token sent by the user may look a lot like an OIDC ID Token or
  access token, but contains claims that are actually the witness signatures of
  the issuing public key
- it is critical that witness signatures not rely on the same root certificate,
  directly or indirectly, without some additional verification mechanism.
  Otherwise a single compromised root certificate could be used to impersonate
  the whole chain of trust.
- while this specification is intended to be functional with or without a
  blockchain, it is likely valuable for signed public keys to be stored on a
  block chain in a manner that they can be retrieved and verified by any
  trustworthy notary / witness using something like
  [Open Person Matching](https://github.com/PortobelloAuth/open-person-matching)
  and a document identifier
  - a non-blockchain version
    - likely requires a certification authority to certify trustworthy notaries
    - might require ephemeral signing keys, making it hard to use for
      [Independent Identity Endorsements](https://github.com/PortobelloAuth/independent-id-endorsements)
    - doesn't leave hashes of demographic information in a public location that
      could be used to deduce it
  - a blockchain version
    - should not store non-public information (anything other than public keys)
      on the blockchain
    - creates a long term ledger of public keys that is potentially usable as
      long as their are participants on the chain
    - allows better portability between notary / witnesses as any witness with
      the right search parameters can potentially find the public key
