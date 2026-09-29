# PrivacyHub 0.10.5-beta

## Security and reliability hardening

- Tightened accessibility automation so it only acts for explicitly supported browsers, netdisk hosts, and access-code input fields. It does not press confirmation or submit buttons.
- Hardened text received through Android sharing actions.
- Reduced UI blocking from database work and improved background task lifecycle handling.
- Isolated backup encryption and file work, and improved recovery for category changes spanning local stores.
- Fixed an asynchronous Settings rendering regression found during Release-to-Release upgrade validation.

## Compatibility and privacy

- No new network permissions.
- Room schema remains v9 and encrypted Backup remains format v5.
- The 0.10.4-beta to 0.10.5-beta Release upgrade was validated with synthetic test data and retained the existing vault and settings data.
- The latest audited Source Available snapshot remains 0.10.4-beta. The 0.10.5-beta source snapshot will be published after its separate audit.

The APK SHA-256, signing certificate, manifest permissions, and independently checkable package metadata are listed in [Security Evidence](SecurityEvidence.md).
