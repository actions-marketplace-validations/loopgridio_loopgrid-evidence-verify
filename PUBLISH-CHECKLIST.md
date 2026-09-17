# GitHub Marketplace publication checklist

## Prerequisites
- [ ] GitHub account has 2FA enabled.
- [ ] Create a **separate public repository** named `loopgrid-evidence-verify`
      (recommended).
- [ ] Accept the GitHub Marketplace Developer Agreement when prompted.
- [ ] No separate web hosting is required.
- [ ] Copy the canonical LoopGrid v0.8 `verifier/loopgrid_verify.py` into this repo.
- [ ] Add one known-valid real v0.8 evidence fixture.
- [ ] Add one deliberately tampered fixture.
- [ ] Confirm GitHub Actions tests pass.
- [ ] Confirm the Marketplace name `LoopGrid Evidence Verify` is accepted as unique.

## Publish
- [ ] Commit and push all files.
- [ ] Open `action.yml` on GitHub.
- [ ] Use the Marketplace banner / **Draft a release**.
- [ ] Check **Publish this Action to the GitHub Marketplace**.
- [ ] Choose the closest available primary category (Security is a good fit if offered).
- [ ] Create tag `v1.0.0`.
- [ ] Publish the release.
- [ ] Create/update floating major tag `v1` to point to the same commit.
- [ ] Test from a second repository using:
      `uses: cybertechsoft/loopgrid-evidence-verify@v1`

## After publication
- [ ] Add Marketplace link to the main LoopGrid README.
- [ ] Add it to loopgrid.io Integrations/Docs.
- [ ] Track external workflow runs / issues / stars, not just listing views.
