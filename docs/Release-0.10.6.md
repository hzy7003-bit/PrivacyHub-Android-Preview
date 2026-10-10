# PrivacyHub 0.10.6-beta

## Link parsing and reliability

- URL extraction keeps a legally paired trailing `)` and trims surrounding punctuation.
- Mixed-case ASCII HTTP(S) schemes are accepted and only the scheme is normalized. Unicode lookalike protocol characters are rejected.
- Tracking cleanup preserves percent escapes in path parameters; Taobao routing regressions remain covered.
- Category aliases are resolved before automatic saves. Text above the existing 1 MiB per-item backup limit is rejected without truncation.
- Failure injection covers category writes, fail-closed restore, and data-access recovery.

## Compatibility and privacy

- Room schema remains v9 and encrypted backup payload remains v5; no data-format migration was introduced.
- No `INTERNET`, `ACCESS_NETWORK_STATE`, or `QUERY_ALL_PACKAGES` permission was added.
- The existing Release signing certificate is retained. A synthetic vault item remained readable after a 0.10.5-beta Release install was upgraded to this Release APK on an isolated API 35 AVD.

## Validation

- Debug and Release JVM suites each passed 276/276.
- `lintDebug` and `lintRelease` completed with zero errors (33 and 34 warnings, plus one informational finding each).
- Isolated API 35 AVD instrumentation passed 49/49 after granting notification permission only to the test AVD.
- The Release APK has no Internet or network-state permission. Its SHA-256, signer, manifest, and package metadata are recorded in [Security Evidence](SecurityEvidence.md).
- No physical-device, multi-ROM, or full third-party-app routing matrix was run.

The official APK is available from the [v0.10.6-beta GitHub Release](https://github.com/hzy7003-bit/PrivacyHub-Android-Preview/releases/tag/v0.10.6-beta).
