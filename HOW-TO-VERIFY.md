# Offline verification

0. Before running anything, check the download is the one released. **First, confirm the signing key is
   ours.** `allowed_signers` arrives with the release, so on its own it proves nothing about who signed:
   ```
   ssh-keygen -lf allowed_signers
   ```
   The fingerprint must read **SHA256:2IRv4ycANEkqBJSYK3l5obP55I+a62/iji9yNpPYbFA** — the fingerprint of
   the one-purpose release key, published here and on inducingfriction.com for cross-checking. If it reads anything else, stop: the files did not come from the
   key we publish. A signature that verifies against a key you have not confirmed this way proves the
   bytes match that key — it does not prove the publisher. Then check the sums and the signature:
   ```
   sha256sum -c SHA256SUMS
   ssh-keygen -Y verify -f allowed_signers -I 831-chain-check-release -n 831-chain-check-release \
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

---

**Erratum (Nov-8, 2026, the day of release):** as first published, this file's verify line named the
principal `-I 831-company`; the published `allowed_signers` carries the principal
`831-chain-check-release`, and the line as printed fails (exit 255) against a good release. The line
above is corrected. The copy inside the v0.1.1 ZIP carries the original line; this repository copy,
and the erratum on the release page, govern. The correction was found by re-running the printed
instructions exactly as a stranger would, after an outside review pressed the key-binding point.
