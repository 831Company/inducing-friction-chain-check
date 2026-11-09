# 831 Verifier + Evidence Kit — Chain Check

Free and open source (Apache-2.0), from The 831 Company LLC. Release v0.1.1.

Free Chain Check verifier + frozen conformance vectors + synthetic sample Evidence
Pack (PDF and JSON). The Evidence Pack **builder/templates and Agent Gateway are
not included**. Local Python 3.10+ standard library; no network account needed.

```
python3 demo.py
python3 -m unittest discover -s . -p 'test_chain_check.py' -v
python3 -m unittest discover -s tests -p 'test_*.py' -v
```

Chain Check checks the historical GENESIS/sorted-key compact-JSON linkage
contract. `CONSISTENT_ONLY` does not prove complete event capture or authorship.
An independently held count/head must be compared for end-of-chain coverage.
Whitespace-only changes may not break canonical semantic record hashes; supply
a separately trusted raw-file SHA-256 to detect those byte changes. The bundled
checkpoint and sample hashes are synthetic and cannot establish third-party trust.

Read HOW-TO-VERIFY.md first and SECURITY.md before you rely on a result. Product maturity
is established on controlled synthetic fixtures, not an external security audit.

## Why it exists

A system that keeps a log of its own decisions can be asked to prove that log was not edited afterwards.
Chain Check answers the narrow, checkable part of that question on your own machine, with no account and no
network: does every row still link to the one before it, in order, from the first. It prints what it found and
what it cannot know. It is the free first step of the 831 verifier family; it does not need any 831 service.

## Verify the download before you run it

Each release carries `831-chain-check-v0.1.1.zip`, `SHA256SUMS`, `SHA256SUMS.sig` and `allowed_signers`.
The steps are in HOW-TO-VERIFY.md, section 0. **Confirm the signing key first:** the release key's
fingerprint is **SHA256:2IRv4ycANEkqBJSYK3l5obP55I+a62/iji9yNpPYbFA**, published here and on
inducingfriction.com. `allowed_signers` travels with the files it vouches for, so check its fingerprint
(`ssh-keygen -lf allowed_signers`) against the value above before trusting a "Good" result — a verified
signature against an unconfirmed key proves the bytes, not the publisher.
