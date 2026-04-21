<p align="center">
  <img src="https://raw.githubusercontent.com/FractalSQLabs/.github/main/FractalSQLabs.jpg" alt="FractalSQLabs" width="720">
</p>

# FractalSQLabs

**Fractal Search, everywhere your data already lives.**

FractalSQLabs ships a LuaJIT-backed metaheuristic vector-search engine
as native extensions for every major database and key-value store:

| Factory | Host | Artifact |
|---|---|---|
| [postgresql-fractalsql](https://github.com/FractalSQLabs/postgresql-fractalsql) | PostgreSQL 14 / 15 / 16 / 17 / 18 | Extension (`CREATE EXTENSION`) |
| [sqlite-fractalsql](https://github.com/FractalSQLabs/sqlite-fractalsql) | SQLite 3.x | Loadable extension (`.load`) |
| [duckdb-fractalsql](https://github.com/FractalSQLabs/duckdb-fractalsql) | DuckDB 1.2 / 1.4 / 1.5 | `.duckdb_extension` |
| [valkey-fractalsql](https://github.com/FractalSQLabs/valkey-fractalsql) | Valkey 7.2 / 8.0 / 8.1 | Module |
| [couchdb-fractalsql](https://github.com/FractalSQLabs/couchdb-fractalsql) | CouchDB | (early) |

Every factory ships the same SQL / command surface:

```
fractal_search(corpus, query, k, params)  → JSON document
fractalsql_edition()                      → 'Community'
fractalsql_version()                      → '1.0.0'
```

## Zero-dependency posture

- **Static LuaJIT** compiled PIC-style into each binary — no
  `libluajit-5.1.so` dependency.
- **Static C/C++ runtime** via `-static-libgcc -static-libstdc++` on
  Linux and `/MT /GL /LTCG` on Windows — no MSVC redistributable.
- **One `.so` per Linux arch**, every supported host major — the UDF
  / extension / module ABIs are stable across versions (proven by CI
  smoke-tests against multiple live server containers per tag).

## Compliance

- **MIT** license for your own use.
- Every release artifact ships with a **Syft-generated SBOM**, a
  **Sigstore/cosign signature**, and a **GitHub build-provenance
  attestation**.
- **BSD-2 / BSD-3 / MIT** third-party notices travel with every
  binary distribution (see each repo's `THIRD-PARTY-NOTICES.md`).
- **NIST SSDF** and **NTIA SBOM Minimum Elements** aligned. Corporate
  OSS-review packs available on request:
  `compliance@fractalsqlabs.com`.

## Security

See [SECURITY.md](https://github.com/FractalSQLabs/.github/blob/main/SECURITY.md)
for our coordinated disclosure policy. TL;DR: use GitHub's private
vulnerability reporting on the affected repo, or email
`security@fractalsqlabs.com`.

---

Built by [@FractalSQLabs](https://github.com/FractalSQLabs). Issues
and PRs welcome on each factory repo.
