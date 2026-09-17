# Canonical verifier required

Before publishing this GitHub Action, copy the **canonical current LoopGrid v0.8**
offline verifier into this directory with the exact filename:

`loopgrid_verify.py`

Do not use the website's synthetic-demo verifier (`verify_synthetic.py`) here.
The Marketplace action must verify the real LoopGrid evidence-bundle format.

Expected invocation, based on the current LoopGrid product documentation:

```bash
python3 verifier/loopgrid_verify.py evidence.zip
```

The verifier should exit with code 0 only when verification succeeds and with a
non-zero code when integrity/signature/chain verification fails.

If the current verifier does not yet use exit codes this way, adapt the wrapper
only after inspecting the real verifier's output contract.
