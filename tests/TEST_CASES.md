# NexStream — Test Case Catalog

**Status:** All cases are PLANNED and NOT EXECUTED as of 2026-11-02. `Expected` is not actual outcome.

| ID | Area | Scenario | Expected behavior | Status |
|---|---|---|---|---|
| TC-PROTO-001 | Contracts | Encode/decode valid Frame | Semantically identical roundtrip | NOT RUN |
| TC-PROTO-002 | Contracts | Unknown optional fields | Compatible parsing | NOT RUN |
| TC-PROTO-003 | Contracts | Missing/invalid oneof | Protocol reject | NOT RUN |
| TC-PROTO-004 | Contracts | Stable message_id after retry | Identity unchanged | NOT RUN |
| TC-PROTO-005 | Contracts | Auth vs ACK distinct | No ambiguous success | NOT RUN |
| TC-PROTO-006 | Contracts | Oversized IDs/secret | Input bound reject | NOT RUN |
| TC-TCP-001 | Framing | Fragment 4B header into 1+3 bytes | Reassembly correct | NOT RUN |
| TC-TCP-002 | Framing | Fragment Protobuf payload | Frame delivered once | NOT RUN |
| TC-TCP-003 | Framing | Coalesce multiple frames | All frames decoded in order | NOT RUN |
| TC-TCP-004 | Framing | Zero/oversized frame | Reject before allocation | NOT RUN |
| TC-TCP-005 | Framing | Malformed Protobuf bytes | Reject safely | NOT RUN |
| TC-TCP-006 | epoll | EAGAIN/EINTR/short read/write | No spin / truncation | NOT RUN |
| TC-TCP-007 | epoll | FIN/HUP while receiving | Cleanup safe | NOT RUN |
| TC-TCP-008 | epoll | Thousands of concurrent clients | Bounded RSS/fds and fair progress | NOT RUN |
| TC-TCP-009 | epoll | fd reused before async completion | No wrong-connection response | NOT RUN |
| TC-TCP-010 | Protocol | BatchStart before Auth | Rejected; no Kafka publish | NOT RUN |
| TC-TCP-011 | Protocol | Batch over count/byte limit | Rejected; memory bounded | NOT RUN |
| TC-AUTH-001 | Auth | Valid secret + authorized host | Auth success | NOT RUN |
| TC-AUTH-002 | Auth | Valid secret + other host | Auth denied | NOT RUN |
| TC-AUTH-003 | Auth | Invalid/revoked/expired key | Auth denied | NOT RUN |
| TC-AUTH-004 | Auth | Auth worker DB timeout | Reactor responsive; failure bounded | NOT RUN |
| TC-AUTH-005 | Auth | Cache miss during DB outage | Fail closed | NOT RUN |
| TC-AUTH-006 | Auth | Revocation missed NOTIFY | Reconciliation fixes cache | NOT RUN |
| TC-AUTH-007 | TLS | Certificate hostname mismatch | Agent refuses and never sends secret | NOT RUN |
| TC-AUTH-008 | TLS | Direct backend access attempt | Blocked by network policy | NOT RUN |
| TC-KAFKA-001 | Kafka | produce enqueue succeeds, broker fails | No success ACK | NOT RUN |
| TC-KAFKA-002 | Kafka | Mixed per-record delivery results | Partial BatchAck | NOT RUN |
| TC-KAFKA-003 | Kafka | ACK lost after Kafka success | Retry same ID; possible duplicate | NOT RUN |
| TC-KAFKA-004 | Kafka | Queue full / outage | Bounded fast-fail and cleanup | NOT RUN |
| TC-KAFKA-005 | Kafka | Callback after disconnect | No UAF | NOT RUN |
| TC-AGENT-001 | SQLite | Crash after durable commit | Pending record recovered | NOT RUN |
| TC-AGENT-002 | SQLite | Crash before deletion commit | Safe retry same ID | NOT RUN |
| TC-AGENT-003 | SQLite | TTL >24h | Expired records removed | NOT RUN |
| TC-AGENT-004 | SQLite | Quota exceeded | Oldest dropped + metric | NOT RUN |
| TC-AGENT-005 | Agent | Kafka back online after 30m | Rate-limited backlog draining | NOT RUN |
| TC-AGENT-006 | Agent | 10s overall deadline | Connection terminates/retries | NOT RUN |
| TC-HA-001 | HA | One Gateway node killed | Clients reconnect to remaining nodes | NOT RUN |
| TC-HA-002 | HA | Registry failover | Bounded auth latency and recovery | NOT RUN |
| TC-CH-001 | ClickHouse | Duplicate Kafka event | Query/dedup strategy respected | NOT RUN |
| TC-PERF-001 | Performance | 1k snapshots/s 10 min | Report metrics and errors | NOT RUN |
| TC-PERF-002 | Performance | 10k snapshots/s 10 min | Report metrics and errors | NOT RUN |
| TC-PERF-003 | Performance | 50k snapshots/s 10 min | Stretch data (no preset PASS) | NOT RUN |

Add cases as contracts are implemented. Store executed results in a dated folder under `tests/results/`.
