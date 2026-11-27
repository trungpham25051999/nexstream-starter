# Contributing

## Branching model (trunk-based)

- `main` is always releasable and **protected**: no direct pushes, no force-push, no deletion.
  Every change lands through a pull request after CI passes (Debug, Release and ASan+UBSan for
  C++ repositories).
- Work on short-lived branches created from `main`, named `<type>/<short-topic>`:

  | Prefix | Use |
  |---|---|
  | `feat/` | new behaviour |
  | `fix/` | defect fix (link the issue) |
  | `perf/` | measured performance change (include before/after numbers) |
  | `refactor/` | behaviour-preserving restructuring |
  | `test/` | tests and fixtures only |
  | `docs/` | documentation, ADRs, reports |
  | `ci/`, `build/` | workflows, CMake, packaging |
  | `chore/` | maintenance |

- Keep branches small and short-lived (hours to a few days). Rebase on `main` before merging;
  branches are deleted automatically after merge.
- **Releases** are annotated SemVer tags `vMAJOR.MINOR.PATCH` on `main`. Downstream repositories
  pin tags (for example contracts `v0.1.0`, ingest `v0.5.0`), never a moving branch.
- **Hotfixes** follow the same path: `fix/` branch from `main` → PR → patch tag.

## Commits

[Conventional Commits](https://www.conventionalcommits.org/): `type(scope): imperative summary`,
for example `fix(queue): preserve FIFO for records enqueued in the same millisecond`.
Explain *why* in the body when it is not obvious; reference issues with `Fixes #N`.

## Pull requests

- One concern per PR; fill in the PR template (scope, tests actually run, failure scenarios,
  ownership/resource/security impact, known limitations).
- Positive **and** failure-path tests for every behaviour change.
- No benchmark or "works" claims without logs under `tests/results/`.
- Never commit secrets, private keys, credentials or generated binaries.

## Engineering rules

- C++20, RAII and explicit ownership; no naked `new`/`delete`; bounded buffers and queues.
- Domain and application layers stay free of Kafka, sockets, HTTP, SQL and generated Protobuf types
  except through ports; `main` is the composition root.
- Nothing blocks the epoll reactor thread.
- Build with warnings enabled and run the same configurations as CI locally before opening a PR
  (see `README.md` / `BUILDING.md` for exact commands).
