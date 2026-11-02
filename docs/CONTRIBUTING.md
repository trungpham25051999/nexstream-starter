# Contributing and Review Standard

- Prefer small scoped PRs per sprint and subsystem.
- Each PR adds/updates tests, README/build commands, architecture status and evidence.
- No unchecked-in keys, passwords, cert private keys, generated binary artifacts or benchmark claims without logs.
- C++20, RAII, strong ownership, bounded buffers, no Reactor blocking and explicit failure semantics.
- Provide a PR summary with affected invariants, tests executed, known gaps and follow-up.
- Run clang-format, compiler warnings, sanitizers and CTest in CI once configured.
- Open issues for unresolved architecture details instead of silently changing accepted constraints.
