# Alert Watcher

## Role in the System

The Alert Watcher is responsible for continuous monitoring of market conditions and triggering alerts when predefined criteria are met. It operates independently of user interaction and analytical computation, ensuring that monitoring logic remains focused and efficient.

This workflow is invoked only after alert conditions have been defined and validated by the central controller.

---

## Monitoring Strategy

The Alert Watcher follows a polling-based monitoring approach, designed to balance responsiveness with system stability.

Key characteristics of the monitoring strategy include:
- Periodic evaluation of live or near-real-time market data.
- Comparison of observed values against stored alert thresholds.
- Execution of alert logic only when conditions transition from unmet to met.

This approach avoids repeated triggering and unnecessary computation.

---

## Threshold Evaluation & Idempotency

To prevent duplicate alerts:
- Each alert condition is evaluated against its last known state.
- Alerts are triggered exactly once per satisfied condition.
- Triggered alerts are recorded and removed or marked as completed.

This idempotent design ensures predictable system behavior even in the presence of retries or transient failures.

---

## Interaction with External Data Sources

Market data retrieval relies on external APIs and is treated as a non-deterministic dependency. The Alert Watcher:
- Handles delayed or unavailable data gracefully.
- Retries evaluation without corrupting alert state.
- Avoids triggering alerts on incomplete or stale data.

External failures do not propagate into invalid alert execution.

---

## Failure Handling & Recovery

The Alert Watcher is designed to handle:
- API timeouts or temporary unavailability.
- Partial data responses.
- Interrupted execution cycles.

In such cases, the workflow preserves state and resumes monitoring without re-triggering previously completed alerts.

---

## Design Rationale

Separating monitoring logic from analysis and orchestration:
- Reduces unnecessary recomputation.
- Improves scalability for multiple concurrent alerts.
- Simplifies debugging and alert lifecycle management.

This design ensures that alert evaluation remains efficient, reliable, and easy to extend.

---

## Summary

The Alert Watcher provides controlled, real-time condition monitoring within the system. By enforcing idempotent execution and isolating monitoring responsibilities, it supports reliable alerting without compromising system stability.
