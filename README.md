# LoopGrid Evidence Verify

Verify a LoopGrid evidence bundle directly in GitHub Actions.

The action runs LoopGrid's offline verifier and fails CI when evidence integrity
verification fails.

## Quick start

```yaml
name: Verify LoopGrid evidence

on:
  workflow_dispatch:

jobs:
  verify:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v7

      - name: Verify evidence
        uses: loopgridio/loopgrid-evidence-verify@v1.0.0
        with:
          evidence: ./evidence/evidence.zip
```

## Pin signer identity

An embedded public key can establish integrity under that key, but it does not by
itself establish that the key belongs to the signer you intended to trust.

For stronger signer identity verification, pass either `expected-key-id` or an
out-of-band trusted public key:

```yaml
- name: Verify evidence with trusted signer
  uses: loopgridio/loopgrid-evidence-verify@v1.0.0
  with:
    evidence: ./evidence/evidence.zip
    trusted-public-key: ./keys/loopgrid-production-public-key.pem
```

## Inputs

| Input | Required | Description |
|---|---|---|
| `evidence` | Yes | Path to a LoopGrid evidence ZIP |
| `expected-key-id` | No | Expected signer key id |
| `trusted-public-key` | No | Path to a trusted PEM public key |
| `tsa-ca-file` | No | CA bundle for RFC3161 timestamp signer validation |

## What verification checks

Depending on what is present in the evidence bundle, the canonical LoopGrid
verifier checks cryptographic signatures, content commitments, hash-chain
continuity, signer identity metadata, disclosures, checkpoints, and optional
RFC3161 timestamp evidence.

## Test fixtures

This repository includes two **synthetic CI fixtures** generated only to test the
public verifier:

- `test-fixtures/valid-evidence.zip` — expected to verify successfully
- `test-fixtures/tampered-evidence.zip` — contains a modified protected payload and
  is expected to fail verification
- `test-fixtures/trusted-public-key.pem` — public key for the synthetic fixture

These are not customer data and are not production evidence samples.

## Trust boundary

Successful verification proves the integrity/provenance properties implemented
by the verifier for the evidence supplied. It does not prove that an AI decision
was correct, lawful, or that every real-world event was captured.

## License

Apache-2.0.
