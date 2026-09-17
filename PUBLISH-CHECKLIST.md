# Marketplace publication checklist

1. Upload this repository content to `loopgridio/loopgrid-evidence-verify`.
2. Confirm the `.github/workflows/test.yml` workflow appears under Actions.
3. Wait for the test workflow to finish successfully.
4. Confirm:
   - known-good fixture verifies;
   - tampered fixture is rejected;
   - final assertion step passes.
5. Open `action.yml` on GitHub.
6. Use the Marketplace publication banner / draft a release.
7. Enable **Publish this Action to the GitHub Marketplace**.
8. Choose the closest available category (Security is a natural fit if offered).
9. Create release tag `v1.0.0`.
10. Publish the release.
11. Create/update a floating `v1` tag pointing to the same commit.
12. Test from a separate repository using:
    `uses: loopgridio/loopgrid-evidence-verify@v1`

Do not publish if the test workflow is red.
