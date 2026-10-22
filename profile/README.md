# FractalSQLabs

**Sovereign, Agentic AI Databases.**
Vector Search. In-Database Reasoning. Production-Safe Agency.
All beside your data.

Native extensions and plugins for the databases and key-value stores below:

| Factory | Host | Artifact | License |
|---|---|---|---|
| [fractalsql-postgresql](https://github.com/FractalSQLabs/fractalsql-postgresql) | PostgreSQL 14 / 15 / 16 / 17 / 18 | Extension (`CREATE EXTENSION`) | Apache 2.0 (v2.x) / MIT (v1.x) |
| [fractalsql-sqlite](https://github.com/FractalSQLabs/fractalsql-sqlite) | SQLite 3.x | Loadable extension (`.load`) | Apache 2.0 (v2.x) / MIT (v1.x) |
| [fractalsql-mariadb](https://github.com/FractalSQLabs/fractalsql-mariadb) | MariaDB 10.6 / 10.11 / 11.4 LTS / 12.3 | Plugin + Daemon | Apache 2.0 (v2.x) |
| [fractalsql-duckdb](https://github.com/FractalSQLabs/fractalsql-duckdb) | DuckDB 1.2 / 1.4 / 1.5 | `.duckdb_extension` | MIT (v1.x) |
| [fractalsql-valkey](https://github.com/FractalSQLabs/fractalsql-valkey) | Valkey 7.2 / 8.0 / 8.1 | Module | MIT (v1.x) |
| [fractalsql-couchdb](https://github.com/FractalSQLabs/fractalsql-couchdb) | CouchDB | (early) | MIT (v1.x) |

Every factory ships the same SQL / command surface:

```
fractal_search(corpus, query, k, params)  → JSON document
fractal_edition()                         → 'Community'
fractal_version()                         → e.g. '2.0.0' (postgresql) — each factory versions independently
```

## Zero-dependency posture

- **Static LuaJIT** compiled PIC-style into each binary — no
  `libluajit-5.1.so` dependency.
- **Static C/C++ runtime** via `-static-libgcc -static-libstdc++` on
  Linux and `/MT /GL /LTCG` on Windows — no MSVC redistributable.
- **One `.so` per Linux arch, one `.dylib` per macOS arch** (Apple
  Silicon + Intel), one `.dll` on Windows — every supported host major
  links the same statically-vendored core archive per platform. The
  UDF / extension / module ABIs are stable across versions (proven by
  CI smoke-tests against multiple live server containers per tag).

## Compliance

- **Apache 2.0** factories (postgresql, sqlite, mariadb; v2.x line):
  every release artifact ships with a **Syft-generated SBOM**, a
  **Sigstore/cosign signature**, and a **GitHub build-provenance
  attestation**.
- **MIT** factories (duckdb, valkey, couchdb; v1.0.0 line).
- **BSD-2 / BSD-3 / MIT** third-party notices travel with every
  binary distribution (see each repo's `THIRD-PARTY-NOTICES.md`).
- **NIST SSDF** and **NTIA SBOM Minimum Elements** aligned (Apache-2.0
  tier). Corporate OSS-review packs available on request:
  `compliance@fractalsqlabs.com`.
