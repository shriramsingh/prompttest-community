# PromptTest Studio v0.1.0

Unsigned build — do not redistribute as a signed commercial release.

## Artifacts

- `PromptTest Studio_0.1.0_x64-setup.exe` — Windows installer (NSIS, per-user install)
- `release-manifest.json` — build provenance (source commit, resource hashes)
- `preflight-evidence.json` — post-build artifact verification
- `SHA256SUMS.txt` — integrity hashes for every artifact

## Build provenance

- Studio commit: `fd508abbd38affb3c9b7a63de2945f7416a6eddc` (dev)
- Studio version: 0.1.0 · Tauri config version: 0.1.0
- PromptTest engine: 1.5.0 (`07de24bbeb3d`)
- Bundled engine payload: 88.5 MB
- Generated: 2026-09-23T17:23:19.538Z
- Authenticode status: NotSigned

## Verify the download

```powershell
Get-FileHash -Algorithm SHA256 "PromptTest Studio_0.1.0_x64-setup.exe"
```

Installer SHA-256: `9a0ba1e61769aef10e53f2b1c61654897c1a8470c589eae2c7ebd76be35b2c17`
