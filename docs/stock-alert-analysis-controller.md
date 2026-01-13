# Stock Alert & Analysis Controller

## Role in the System

The Stock Alert & Analysis Controller acts as the central orchestration layer of the platform. It coordinates user intent, manages workflow state, and determines which downstream components should be invoked at each stage of execution.

This workflow does not perform analysis or monitoring directly. Its responsibility is to ensure that system behavior remains controlled, predictable, and aligned with the current context.

<img width="1920" height="1080" alt="Screenshot (431)" src="https://github.com/user-attachments/assets/e7e753cc-f62e-4abc-a6e9-bff2423da42d" />

---

## Key Responsibilities

The controller is responsible for:

- Interpreting incoming user requests and commands.
- Managing workflow state and context progression.
- Validating whether required inputs are available.
- Routing execution to analysis, monitoring, or notification workflows.
- Preventing invalid or premature execution paths.

By centralizing these responsibilities, the system avoids fragmented decision logic across multiple workflows.

<img width="1920" height="1080" alt="Screenshot (418)" src="https://github.com/user-attachments/assets/3b9a2af3-a76f-4676-99de-a7810711d71f" />

---

## Input Handling & Intent Interpretation

Incoming inputs may be:
- Explicit user commands
- Follow-up responses to incomplete requests
- Requests to list, create, update, or delete alerts
- Requests for analysis or status information

The controller evaluates each input in the context of:
- Current workflow state
- Previously stored user inputs
- Required fields for the requested operation

If required information is missing, execution is paused and the system waits for additional input rather than failing or guessing.

---

## State Management Strategy

The controller uses persistent state to track:
- Current interaction stage
- Collected input parameters
- Pending actions
- Completed operations

State transitions are explicit and controlled. The controller advances the workflow only when validation conditions are satisfied, ensuring consistent behavior across sessions and retries.

---

## Execution Routing

Based on validated intent and state, the controller routes execution to one or more of the following components:

- Technical Analysis Engine for indicator evaluation.
- Alert Watcher for threshold-based monitoring.
- Data services for persistence or retrieval.
- Notification and summarization layers for output delivery.

The controller itself remains stateless in execution logic, acting only as a coordinator.

---

## Error Handling & Recovery

The controller is designed to handle:
- Partial or malformed inputs
- Repeated or duplicate commands
- Interrupted execution flows
- Downstream workflow failures

In such cases, the controller preserves state and resumes execution safely once conditions allow.

---

## Design Rationale

This orchestration-centric design was chosen to:
- Reduce duplication of decision logic.
- Improve explainability and debuggability.
- Enable future extension without reworking core flows.
- Maintain a clear separation between intent, logic, and execution.

---

## Summary

The Stock Alert & Analysis Controller serves as the system’s control plane, ensuring that all actions occur in the correct order, with the correct inputs, and under clearly defined conditions. This design enables the platform to scale in complexity without sacrificing reliability or clarity.

<img width="1920" height="1080" alt="Screenshot (419)" src="https://github.com/user-attachments/assets/c646e1bb-9430-4900-a126-ca6e80f4a155" />


<img width="1920" height="1080" alt="Screenshot (420)" src="https://github.com/user-attachments/assets/b7cd4a34-fe4f-48b9-9d64-846f1ce2fdc1" />


<img width="1920" height="1080" alt="Screenshot (421)" src="https://github.com/user-attachments/assets/bbf70fe4-59b7-4ea8-bcfe-dc860c07f136" />


<img width="1920" height="1080" alt="Screenshot (422)" src="https://github.com/user-attachments/assets/5a7c659f-9782-4556-bd27-7cd71d360a4e" />


<img width="1920" height="1080" alt="Screenshot (423)" src="https://github.com/user-attachments/assets/364ad6fd-c675-45b3-b760-8e5c11b0c318" />


<img width="1920" height="1080" alt="Screenshot (424)" src="https://github.com/user-attachments/assets/74c000d0-1cae-4e7c-ad78-a38375723add" />


