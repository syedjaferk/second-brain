
#### Episode 1: Why Message Queues Exist

- Synchronous vs asynchronous communication
- Coupling problems queues solve (producer/consumer decoupling, buffering, backpressure)
- Where RabbitMQ fits vs Kafka/SQS (brief positioning)
- Docker spin-up: RabbitMQ + management UI

#### Episode 2: Core Concepts — Producers, Consumers, Messages

- Anatomy of a message (body, properties, headers)
- Connections vs Channels (why channels matter for performance)
- First Python producer/consumer with `pika`

#### Episode 3: Queues, Exchanges, Bindings — The Routing Model

- Exchange → Binding → Queue flow
- Routing keys explained
- Default exchange behavior

#### Episode 4: Direct Exchange

- Exact routing key matching
- Use case: task routing by type (e.g., email vs SMS workers)
- Python demo: multiple bindings, one queue per worker type

#### Episode 5: Fanout Exchange

- Broadcast pattern, ignores routing key
- Use case: cache invalidation, notifications to all services
- Python demo: multiple consumers on one fanout

#### Episode 6: Topic Exchange

- Wildcard routing (`*` and `#`)
- Use case: log routing by severity/service (`logs.error.auth`)
- Python demo: pattern-based subscriptions

#### Episode 7: Headers Exchange

- Routing by message headers instead of routing key
- `x-match: any` vs `x-match: all`
- Use case: content-based routing when routing key isn't enough
- Why it's rarely used in practice (performance trade-off) — when it's actually the right call

#### Episode 8: Alternate Exchange (AE)

- What happens to unroutable messages by default (silently dropped)
- Setting `alternate-exchange` on a queue/exchange
- Use case: catching misrouted messages for audit/debugging
- Python demo: primary topic exchange + AE catching unmatched messages

#### Episode 9: Acknowledgements & Reliability

- Auto-ack vs manual ack — why auto-ack is dangerous in production
- `ack`, `nack`, `reject`, `requeue`
- Consumer crash scenarios and message redelivery
- Publisher confirms (producer-side reliability)

#### Episode 10: Prefetch & Fair Dispatch

- Round-robin default problem (fast vs slow consumers)
- `basic.qos` / prefetch count
- Tuning prefetch for throughput vs fairness

#### Episode 11: Durability — Queues, Messages, Exchanges

- Durable queues vs durable messages (both needed for persistence)
- `delivery_mode=2`
- What survives a broker restart and what doesn't
- Performance cost of durability

#### Episode 12: Dead Letter Exchanges (DLX) & Dead Letter Queues (DLQ)

- Why messages die: rejected, TTL expired, queue length limit hit
- `x-dead-letter-exchange` / `x-dead-letter-routing-key`
- Building a DLQ + retry pipeline (with backoff)
- Difference between DLX and Alternate Exchange (common confusion point — worth its own segment)

#### Episode 13: TTL, Queue Limits & Delayed Messages

- Message TTL vs Queue TTL
- Max-length and overflow behavior
- Delayed message pattern (via TTL + DLX, or the delayed-message plugin)

#### Episode 14: Building a Real Python Application

- End-to-end mini project (e.g., order processing pipeline using direct + topic exchanges + DLQ)
- Error handling, retries, idempotency basics

#### Episode 15: Clustering & High Availability

- Cluster nodes, mirrored/quorum queues
- Quorum queues (modern replacement for classic mirrored queues) — why RabbitMQ pushes these now
- Split-brain basics, partition handling

#### Episode 16: Cloud Deployment Patterns

- Self-managed RabbitMQ on cloud VMs vs managed options (AWS Amazon MQ, CloudAMQP)
- Kubernetes deployment (RabbitMQ Cluster Operator)
- Environment-based config, secrets management for credentials
- Scaling consumers horizontally in a cloud/K8s setup
- Health checks & readiness probes for RabbitMQ pods

#### Episode 17: Cloud Messaging Patterns

- Competing consumers pattern
- Publish-subscribe fan-out across microservices
- Saga pattern basics using queues (orchestration vs choreography, high level)
- Outbox pattern (avoiding dual-write problem between DB and queue)
- Circuit breaker + retry queue combo for resilient consumers

#### Episode 18: Monitoring & Production Best Practices

- Management UI + Prometheus/Grafana basics for RabbitMQ metrics
- Alerting on queue depth, unacked messages, consumer count
- Security: vhosts, user permissions, TLS
- Capacity planning checklist before going to production