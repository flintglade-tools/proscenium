# Proscenium

Proscenium is a local-first deterministic webhook reliability lab for Windows. It lets developers capture synthetic webhook traffic on loopback, build repeatable response sequences, inspect redacted events, replay them only to local receivers, and run scenario checks without placing payloads in a hosted service.

## Download

[Download the latest Windows x64 release](https://github.com/flintglade-tools/proscenium/releases/latest), then verify the ZIP against its published `.sha256` sidecar before extracting it.

Windows may show an unrecognized-publisher warning because the initial release is not Authenticode-signed. The archive is deterministically packaged and checksum-verified in Flintglade's release process, and it is accompanied by a CycloneDX SBOM and third-party notices. Read [Installation](docs/INSTALL.md) before first launch.

## Free and Pro

Free includes two endpoints and the newest 100 redacted events.

Pro is a **$49 one-time, single-user license for the 0.x release family**. It adds advanced signature fixtures, schema assertions, mutation matrices, scenario CI/JUnit output, larger local retention, unlimited endpoints, and hash-chained evidence export.

[Buy Pro securely through Stripe](https://licenses.flintglade.com/buy/proscenium)

Activation periodically refreshes a signed entitlement lease. Refunds and payment disputes revoke the entitlement; ordinary network outages retain access only through the signed offline lease, for at most fourteen days.

## Safety boundaries

- Proscenium binds to `127.0.0.1` only.
- Control requests require a random per-launch bearer token.
- Replay is limited to validated HTTP(S) loopback destinations.
- Configured sensitive headers and JSON pointers are redacted before persistence.
- Scenario files cannot execute scripts, load remote schemas, or contain signature secrets.
- Captured data stays on the current machine unless you explicitly export it.

See [Security](SECURITY.md), [Privacy](docs/PRIVACY.md), and [Data removal](docs/DATA-REMOVAL.md) for the exact boundaries.

## Repository scope

This repository distributes customer documentation and verified release artifacts. It does not publish the proprietary source code. The compiled application is governed by [LICENSE.txt](LICENSE.txt).

## Support

Email [support@flintglade.com](mailto:support@flintglade.com) for product, billing, refund, accessibility, privacy, or security help. Never send a full card number, password, token, private key, license key, or real customer payload.
