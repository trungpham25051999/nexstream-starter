# Architecture Decision Register

| ADR | Decision | Status |
|---|---|---|
| ADR-008 | Kafka-confirmed ACK, at-least-once attempts, duplicates possible | Accepted baseline; detail to implement |
| ADR-009 | Length-prefixed TCP Protobuf, one authenticated batch/connection | Accepted baseline; `.proto` to finalize |
| ADR-010 | C++20 single level-triggered epoll Reactor | Accepted baseline |
| ADR-011 | Kafka & ClickHouse serialization/storage layout | Open |
| ADR-012 | Test and benchmark methodology | Accepted baseline; results pending |
| ADR-013 | Deploy/multi-node topology | Accepted baseline; HA not yet built |
| ADR-014 | SQLite WAL, 24h max TTL, drop-oldest | Accepted for MVP; quota unresolved |
| ADR-015 | HAProxy TLS + per-Agent API key, PostgreSQL cache | Accepted for MVP; revocation SLO/settings to benchmark |

Decisions are architecture commitments, **not implementation proof**. For changes create a numbered ADR describing context, choice, alternatives and trade-offs.
