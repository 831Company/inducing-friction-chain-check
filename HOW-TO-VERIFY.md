# Offline verification

0. Before running anything, check the download is the one released. Put the zip, `SHA256SUMS`,
   `SHA256SUMS.sig` and `allowed_signers` from the release page in one folder, and run there:
   ```
   ssh-keygen -lf allowed_signers
   sha256sum -c SHA256SUMS
   ssh-keygen -Y verify -f allowed_signers -I 831-chain-check-release -n 831-chain-check-release \
     -s SHA256SUMS.sig < SHA256SUMS
   ```
   The first line prints the release key's fingerprint. It must read
   `SHA256:2IRv4ycANEkqBJSYK3l5obP55I+a62/iji9yNpPYbFA`. Compare it with the copies published on the
   repository and on the website; this copy travels inside the download, so it proves nothing by itself.
   The second line must end `: OK`. The third must print `Good "831-chain-check-release" signature`.
   Anything else: stop. (v0.1.1 printed the third line with the wrong signer name, `831-company`; it failed
   against a good release. Corrected in v0.1.2.)

   `allowed_signers` holds the one public key published on the release page. `EXPORT-SOURCE-RECEIPT.json`
   inside the package is the receipt of the export from the source workshop: its hashes describe that earlier
   export, not this zip; its `verifier_sha256` is the v0.1.0 checker's. This package's checker hash is
   `verifier_sha256` in `vectors/GOLDEN.json` (unchanged since v0.1.1). The release zip's hash is the one in
   `SHA256SUMS`.
1. Run the five-step `python3 demo.py` synthetic verifier walkthrough.
2. Run all unit and frozen-vector tests under `tests/`.
3. Recompute SHA-256 for `sample-pack/manifest.json` and `report.pdf` using
   `sample-pack/HASHES.json` and check every synthetic source byte count and hash.
4. Do not mistake a locally supplied checkpoint for an independently signed head.
5. Report discrepancies with a synthetic fixture and exact reproduction command.
