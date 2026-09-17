# LoopGrid Evidence Verify

Verify a LoopGrid evidence bundle inside GitHub Actions.

> **Important before publishing:** this starter repository intentionally does **not**
> include a reconstructed verifier. Copy the canonical `verifier/loopgrid_verify.py`
> from the current LoopGrid v0.8 source release into `verifier/loopgrid_verify.py`.
> This avoids accidentally publishing a Marketplace action that verifies a different
> format from the real LoopGrid evidence bundle.

## What this action does

The action runs the canonical LoopGrid offline verifier against an evidence bundle
and lets the verifier's exit code control the CI result:

- verification succeeds -> workflow passes
- tamper/signature/chain verification fails -> workflow fails
- missing bundle/verifier -> workflow fails with configuration error

LoopGrid's current evidence bundle is documented as containing artifacts such as:

- `manifest.json`
- `decision.json`
- `events.jsonl`
- `chain-witness.jsonl`
- `public-key.pem`
- `report.html`

## Usage

```yaml
name: Verify LoopGrid evidence

on:
  workflow_dispatch:

jobs:
  verify:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Verify LoopGrid evidence
        uses: cybertechsoft/loopgrid-evidence-verify@v1
        with:
          evidence: ./evidence/evidence.zip
```

## Testing before Marketplace publication

1. Copy the canonical LoopGrid verifier:
   `verifier/loopgrid_verify.py`
2. Put one known-good evidence bundle at:
   `test-fixtures/valid-evidence.zip`
3. Put one intentionally tampered bundle at:
   `test-fixtures/tampered-evidence.zip`
4. Update `.github/workflows/test.yml` if the paths differ.
5. Push to GitHub and confirm:
   - valid bundle job passes
   - tampered bundle job fails *inside the verification step*
6. Only after those tests pass, create a release and publish to GitHub Marketplace.

## Security / trust boundary

This action verifies the evidence format implemented by the bundled canonical
LoopGrid verifier. It does not prove that an AI decision was correct, lawful, or
that every real-world event was captured.

## License

Apache-2.0. See `LICENSE`.
