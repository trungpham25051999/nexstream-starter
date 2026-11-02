# Sprint 02 — Frame Decoder + epoll Gateway

## Prerequisites
Sprint 01 contracts generated and tests passing.

## Scope
1. Implement bounded incremental `FrameDecoder` with 4-byte BE length prefix.
2. Implement RAII nonblocking listener/socket, `accept4`, epoll LT loop, `EPOLLIN` / `EPOLLOUT`, `EAGAIN`, `EINTR`, FIN, ERR/HUP.
3. Implement `TcpConnection` state machine and per-connection budget/timeout; initially auth via deterministic fake verifier; never allow telemetry before authorization.
4. Test fragmented headers/payloads, coalesced frames, malformed frame length/Protobuf, rapid connect/disconnect, fairness under noisy client, fd reuse, shutdown.
5. Add local test client harness; no Kafka yet (delivery stub must **not** masquerade as confirmed Kafka ACK in docs).

## Requirements
No blocking I/O in Reactor. No unbounded allocations. No raw pointer callbacks crossing async lifetimes. Set 64 KiB max frame and 50 samples/batch as initial flags. Document memory budget and observed test results.

## Tests
TC-TCP-001..011 in `tests/TEST_CASES.md`.

## Scope guard
Implement only Sprint 02 with unit + integration tests. Explain ownership, state machine, event loop fairness and all deadlines; run sanitizers where feasible and record outputs.
