Platform engineer building and operating ingestion pipelines that move telemetry from edge devices to queryable storage.

## Darrin Douglas

I design and operate ingestion systems that handle high-volume device telemetry, owning the full path from edge collection to durable storage. My work centers on throughput, backpressure, and data integrity—keeping pipelines healthy under load and making failure modes explicit. I accept tighter coupling in exchange for simpler operational reasoning, and I prefer boring, well-understood components over clever ones.

### 🛠 Tech & Infrastructure

- **Core**: `Go`, `gRPC`, `Kafka`, `PostgreSQL`
- **Data**: `Parquet`, `ClickHouse`, `Redis`
- **Infra**: `Kubernetes`, `Terraform`, `Prometheus`
- **Tooling**: `Grafana`, `Docker`, `Makefile`

### ⚙️ Engineering Areas

- Designing idempotent ingestion APIs that tolerate duplicate events without corrupting downstream aggregates.
- Building partition-aware consumers that rebalance cleanly and preserve ordering per device.
- Tuning schema evolution for Parquet files so queries stay fast while producers change shape.
- Automating rollouts of pipeline workers with canary checks and automatic rollback on error-rate spikes.

### 🔭 Current Focus

- Reducing tail latency in the ingestion path without adding a second queue hop.
- Making backpressure propagate from storage to producers so no single partition falls behind indefinitely.
- Cutting cold-start time for new consumers by pre-warming partition assignments.
- Moving from periodic batch compaction to incremental compaction without breaking time-range queries.

### 📌 Engineering Notes

- Tests that mock the queue are worthless; write integration tests that run real Kafka and Postgres containers.
- Migrations should be additive and reversible—never rewrite a table in place; use expand-and-contract.
- Retries are only safe when the operation is idempotent; otherwise, fail fast and let the DLQ own the problem.
- Every service needs a dashboard, a runbook, and a rollback path before it is allowed to serve traffic.

### 🧭 How I Work

- I write the smallest change that moves the system forward, then refactor once the shape is clear.
- I instrument first and optimize later—if it isn't measured, it isn't a bottleneck.
- I prefer explicit configuration over magic defaults, and I document the trade-offs in the PR.

*Reliability is not a feature; it is the absence of surprises.*