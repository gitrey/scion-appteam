---
name: locust
description: Execute automated Locust load tests headlessly to verify performance and scalability
---

# /locust — Execute Automated Locust Load Tests

## Trigger

User invokes `/locust` with a target host, number of concurrent users, and specification ID (e.g., `/locust "http://localhost:3000" 100 "F-0031"`).

## Instructions

1. **Design or Update the Locustfile** — Create or audit the Locust script under `tests/perf/locustfile.py`. Ensure it defines realistic task behaviors (e.g., hitting `/api/checkout`, `/api/products` with realistic payload structures).
2. **Run Headless Locust** — Execute the load test headlessly using the `--headless` and `--html` flags to prevent interactive hangs:
   ```bash
   locust -f tests/perf/locustfile.py \
     --headless \
     --users <concurrency> \
     --spawn-rate 10 \
     --run-time 1m \
     --host <target-host> \
     --html docs/perf-reports/<spec-id>-locust.html
   ```
3. **Analyze Performance Metrics** — Inspect the generated report or CLI logs to extract:
   - **RPS (Requests Per Second):** Verify the system handles the target load.
   - **Latency distribution:** Check if `p95` and `p99` latency are within acceptable boundaries (e.g., < 200ms).
   - **Failure Rate:** Verify the error rate is `0.0%` (no 500 errors under load).
4. **Groom & Commit Reports** — Stage and commit the visual HTML reports and the updated Locust file:
   ```bash
   git -c user.name="Scion Agent" -c user.email="scion@users.noreply.github.com" add tests/perf/ docs/perf-reports/
   git -c user.name="Scion Agent" -c user.email="scion@users.noreply.github.com" commit -m "perf: add Locust load test reports for <spec-id>"
   ```
5. **Performance Audit Summary** — Present a clear performance summary report back to the team:
   - Peak throughput (RPS) achieved.
   - Response time latency details (p50, p95, p99).
   - Failure rate details.
   - A relative markdown link to the saved HTML report in `docs/perf-reports/`.

## Project Context

- **Project:** appteam
