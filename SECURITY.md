# Security

Report suspected vulnerabilities privately to [support@flintglade.com](mailto:support@flintglade.com). Include the affected version, reproduction steps, impact, and a safe proof of concept. Do not include real secrets or customer payloads.

<a name="release-maintenance-status--2026-10-09"></a>

## Release maintenance status

On 2026-11-23, the RustSec check of crate versions in the
[published v0.1.1 SBOM](https://github.com/flintglade-tools/proscenium/releases/download/v0.1.1/proscenium-0.1.1.cdx.json)
matched 15 advisories across six dependencies. The versions below are from that
SBOM. The listed updates cover those matches on each dependency's current version line.

| Dependency in the published SBOM | Minimum version covering the listed advisories | Upstream advisories |
| --- | --- | --- |
| quinn-proto 0.11.16 | 0.11.19 | [0338](https://rustsec.org/advisories/RUSTSEC-2026-0338.html), [0339](https://rustsec.org/advisories/RUSTSEC-2026-0339.html), [0340](https://rustsec.org/advisories/RUSTSEC-2026-0340.html), [0341](https://rustsec.org/advisories/RUSTSEC-2026-0341.html), [0342](https://rustsec.org/advisories/RUSTSEC-2026-0342.html), [0523](https://rustsec.org/advisories/RUSTSEC-2026-0523.html), [0524](https://rustsec.org/advisories/RUSTSEC-2026-0524.html) |
| quinn-udp 0.5.15 | 0.5.16 | [Truncated datagram handling](https://rustsec.org/advisories/RUSTSEC-2026-0538.html) |
| rustls 0.23.41 | 0.23.46 | [TLS handshake validation](https://rustsec.org/advisories/RUSTSEC-2026-0285.html), [Session debug output](https://rustsec.org/advisories/RUSTSEC-2026-0346.html), [Certificate decompression](https://rustsec.org/advisories/RUSTSEC-2026-0348.html), [Key exchange](https://rustsec.org/advisories/RUSTSEC-2026-0349.html) |
| rustls-webpki 0.103.13 | 0.103.16 | [Distrusted intermediate certificates](https://rustsec.org/advisories/RUSTSEC-2026-0382.html) |
| url 2.5.8 | 2.5.9 | [Nested blob URL handling](https://rustsec.org/advisories/RUSTSEC-2026-0592.html) |
| webpki-roots 1.0.8 | 1.0.10 | [Distrusted root/intermediate trust paths](https://rustsec.org/advisories/RUSTSEC-2026-0381.html) |

The audit also reported a warning for the Unix-only
[Tokio AsyncFd advisory](https://rustsec.org/advisories/RUSTSEC-2026-0386.html)
against Tokio 1.52.3 and a registry yank for chacha20 0.10.1.

The SBOM identifies dependency versions. Runtime reachability in the Windows
executable depends on compiled features and the paths the application invokes.

A **replacement Windows package is pending**. The release requires Windows
tests, a production package smoke test with a signed license lease, and a
regenerated SBOM, third-party notices and archive checksums.

## Enforced boundaries

- The server binds only `127.0.0.1`, and the default port is selected by the operating system.
- Every control API request requires a random 256-bit per-launch bearer token. Capture URLs do not expose that token.
- The UI is embedded. Its Content Security Policy denies remote scripts, remote styles, framing, forms, and external connections. User-configured hook responses receive a separate sandbox policy with all resource loading disabled.
- Replay targets must be HTTP(S) loopback URLs. Remote hosts, credentials, fragments, redirects, `CONNECT`, and `TRACE` are rejected. The final scenario URL must preserve the validated scheme, host, and port. `localhost` resolution is pinned to `127.0.0.1`, and ambient system proxy settings are disabled inside the replay client.
- Requests, responses, state, scenario packs, schemas, names, headers, mutations, delays, and nesting are bounded.
- Scenario files cannot execute scripts, load remote schemas, interpolate templates, or embed signature secrets. Secrets are read from explicitly named environment variables.
- Sensitive headers are removed or replaced with `[REDACTED]`. Configured JSON pointers are redacted before payload persistence and evidence generation. A configured pointer set fails closed to a fixed omission marker for malformed JSON, non-JSON, or binary input.
- Pro checks occur in Rust handlers and CLI paths. They are not UI-only switches.
- Persisted Pro endpoints remain on disk after a downgrade so customer data is not destroyed, but Free-mode state views, hook lookup, replay lookup, event retention, and JSON Schema evaluation apply the current signed entitlement at use time. Endpoints beyond the Free allowance are dormant until Pro is restored.
- License traffic requires HTTPS outside loopback test fixtures. Pro requires an Ed25519-signed lease bound to the product, environment, purchase key hash, issue time, and expiry. An unsigned or locally edited cache cannot grant Pro, and network failure never extends Pro past the signed expiry.
- State updates use one process-wide file lock and transactional write/rename semantics. A captured event and its response-sequence advance commit together.

## Explicit non-goals

Version 0.1 has no public tunnel, hosted payload storage, production proxying, multi-user access, arbitrary outbound host allowlist, plugins, executable response templates, or remote JSON Schema references.

## Residual risks

- Any process running as the same operating-system user can generally inspect that user's files or local process memory. Proscenium is not a sandbox against a compromised account.
- Captured payloads may contain identifiers outside configured redaction paths. Use synthetic events and configure redaction before testing sensitive shapes.
- A hash chain and full-state digest detect modification and bind the claimed generation time; they are not a trusted external timestamp or third-party signature.
- The license key is an entitlement credential, not a payment credential. It is stored in the current user's application-data directory with restrictive Unix permissions and inherited user-profile protections on Windows.
