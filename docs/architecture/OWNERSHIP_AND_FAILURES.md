# Ownership, Lifetimes and Failure Handling

- Reactor owns socket descriptors and `TcpConnection` objects; all state transitions and socket writes on Reactor thread.
- Authentication workers and Kafka poll thread publish immutable completions keyed by `(connection_id,generation,request_id)`; never hold raw connection pointers.
- Disconnect before delivery callback: callback may still arrive, completion safely discarded or finalized in independent pending-delivery registry.
- fd reuse is normal: numeric fd alone must never index a delayed completion.
- Bound per-connection receive buffer, outbound buffer, pending delivery records, global session count, and auth queue.
- Kafka queue full / registry slow / overload: explicit retry-later or close, never false success ACK.
- Circuit breaker and jitter limit storm during outages.
- Traces/metrics must not expose credentials or unbounded host-cardinality labels.

Test each bullet using targeted failure injection before calling the relevant sprint complete.
