# Offline verification

0. Before running anything, check the download is the one released:
   ```
   sha256sum -c SHA256SUMS
   ssh-keygen -Y verify -f allowed_signers -I 831-company -n 831-chain-check-release \
     -s SHA256SUMS.sig < SHA256SUMS
   ```
   `allowed_signers` holds the one public key published on the release page. `EXPORT-SOURCE-RECEIPT.json`
   inside the package is the receipt of the export from the source workshop: its hashes describe that earlier
   export, not this zip; its `verifier_sha256` is the v0.1.0 checker's. The v0.1.1 checker's hash is
   `verifier_sha256` in `vectors/GOLDEN.json`. The release zip's hash is the one in `SHA256SUMS`.
1. Run the five-step `python3 demo.py` synthetic verifier walkthrough.
2. Run all unit and frozen-vector tests under `tests/`.
3. Recompute SHA-256 for `sample-pack/manifest.json` and `report.pdf` using
   `sample-pack/HASHES.json` and check every synthetic source byte count and hash.
4. Do not mistake a locally supplied checkpoint for an independently signed head.
5. Report discrepancies with a synthetic fixture and exact reproduction command.
