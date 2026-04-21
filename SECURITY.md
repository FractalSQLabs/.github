# Security Policy

This policy applies to all repositories under the
[FractalSQLabs](https://github.com/FractalSQLabs) organization — the
`*-fractalsql` factories (MySQL, MariaDB, PostgreSQL, SQLite, DuckDB,
Redis, Valkey, CouchDB) and the `fractalsql-core` bytecode factory.

## Reporting a vulnerability

**Please do not open public GitHub issues for security-sensitive
reports.** We prefer coordinated disclosure. Two channels:

1. **GitHub private vulnerability reporting** (preferred). Navigate to
   the affected repo's Security tab → "Report a vulnerability." This
   opens a private advisory visible only to repo maintainers.
2. **Email.** If private reporting is unavailable or the repo is not
   a FractalSQLabs one but bundles a FractalSQL binary, email
   `security@fractalsqlabs.com` (replace with your real address).

We commit to acknowledging valid reports within **3 business days**
and to keeping you updated at least every 14 days until the issue is
resolved or the report is closed as out of scope.

## Supported versions

The current `1.x` series is supported. Security fixes are backported
to the most recent minor release.

| Version | Supported |
| ------- | :-------: |
| 1.x     | ✅        |
| < 1.0   | ❌        |

## Scope

**In scope:**
- Memory-safety issues in any `fractalsql.so` / `fractalsql.dll` UDF
  or module (buffer overflows, use-after-free, double-free).
- Authentication / authorization issues in anything FractalSQLabs
  distributes directly.
- Issues in the bytecode loader (`luaL_loadbuffer` path) that could
  be triggered by a malicious corpus or query payload.
- Supply-chain tampering in release artifacts (signed artifacts and
  SBOMs accompany every release; please report any integrity
  verification failures).

**Out of scope:**
- Vulnerabilities in the host database or server (MySQL, MariaDB,
  PostgreSQL, SQLite, DuckDB, Redis, Valkey, CouchDB) itself —
  please report those upstream to the respective vendors.
- Issues in LuaJIT itself — report to
  <https://luajit.org/> or the
  [LuaJIT/LuaJIT](https://github.com/LuaJIT/LuaJIT) maintainers.
- Social engineering, DoS from resource exhaustion with legitimate
  input sizes, or theoretical attacks requiring kernel-level
  privilege.

## Disclosure timeline

We follow a standard **90-day coordinated disclosure window**:

- **Day 0**: Report received and acknowledged privately.
- **Days 1–14**: Triage, severity assessment, reproduction.
- **Days 14–60**: Fix development, review, and validation.
- **Days 60–90**: Release prepared; coordinated advisory drafted.
- **Day 90**: Public advisory + patched release published.

We will request an extension in writing if a valid, complex fix needs
more time. We will publish the advisory on schedule if we cannot
agree with the reporter on an extension.

## What you can expect from us

- Confidentiality of your report until the coordinated disclosure
  date.
- Credit in the published advisory (optional — let us know your
  preference).
- No legal action against good-faith researchers who follow this
  policy. We explicitly support the principles of
  [Safe Harbor for Security Researchers](https://disclose.io/).

## Artifact integrity

Every release artifact (`.deb`, `.rpm`, `.msi`, `.zip`,
`.duckdb_extension`) is accompanied by:

- A **Syft-generated SBOM** in SPDX JSON format.
- A **Sigstore/cosign signature** you can verify with
  `cosign verify-blob --certificate <artifact>.pem --signature <artifact>.sig <artifact>`.
- A **GitHub build provenance attestation** you can verify with
  `gh attestation verify <artifact> --repo FractalSQLabs/<repo>`.

If you download an artifact and verification fails, **do not install
it** and report to `security@fractalsqlabs.com` immediately. Always
prefer the official GitHub Release assets over mirrors.

## Third-party components

FractalSQL factories bundle third-party components (Stochastic
Fractal Search reference code, LuaJIT, and Enterprise-edition
algorithms). The full attribution ledger lives in each repo's
`THIRD-PARTY-NOTICES.md`. Vulnerabilities in those components are
tracked separately:

- LuaJIT vulnerabilities: report upstream first, then here if you
  believe our bundling is affected.
- SFS/dFDB/QRFS/AFDB-SFS algorithmic components: academic reference
  implementations. Upstream authors may not maintain an active
  security channel; report to us and we will coordinate.

## Compliance posture

- **NIST SP 800-218 (SSDF)**: we track component provenance, sign
  release artifacts, and emit SBOMs with every release.
- **NTIA Minimum Elements for SBOM**: met via Syft-generated SPDX
  JSON attached to each release.
- **SLSA**: Level 2+ via GitHub's native build provenance
  attestations.

Questions about compliance artifacts for corporate OSS review
processes: `security@fractalsqlabs.com`.
