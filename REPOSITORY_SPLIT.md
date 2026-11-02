# Multi-Repo Split Guide

This starter kit is a **documentation blueprint**, not six code repositories. Use the following map when initializing repositories:

| Files | Destination |
|---|---|
| Shared architecture, ADRs, benchmark/runbook/security docs | `nexstream-deploy/docs/` |
| Contracts Sprint 01 guidance + relevant test vectors | `nexstream-contracts/` |
| Ingest Sprint 02 guidance + network tests | `nexstream-ingest/` |
| SQLite/collector/publisher guidance | `nexstream-publisher/` |
| Analytics documentation | `nexstream-processor/`, `nexstream-query/` |
| Top-level portfolio README and recruiter guide | `nexstream-deploy/` or a public `nexstream` overview repo |

Each repo must have its own README tailored to scope, BUILDING, test results and CI. Avoid cross-repository symlinks that will break when split.
