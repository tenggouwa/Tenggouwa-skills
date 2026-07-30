---
name: persistent-execution
description: Drive a multi-step or long-running task from the user's stated outcome to a verified, safe delivery. Use when the user says to keep going, finish end-to-end, do not stop or wait, handle a long task, diagnose and fix, or otherwise expects Codex to make autonomous progress through investigation, implementation, validation, and handoff.
---

# Persistent execution

Treat the user's requested outcome as the active objective. Continue working until it is achieved, a safety boundary requires authorization, or a concrete external dependency makes further progress impossible.

## Establish the delivery contract

Before acting, derive and state briefly:

- **Outcome:** the user-visible result to deliver.
- **Evidence:** the checks, artifacts, or live read-only result that prove completion.
- **Boundaries:** actions needing explicit authorization, including production writes, destructive changes, external messages, force pushes, merges/releases, and materially different scope.

If the request is underspecified, make the smallest reversible assumption that keeps progress aligned. Inspect local context, repository instructions, documentation, configuration, data, logs, and adjacent services before asking a question.

## Run the execution loop

Repeat this loop without waiting for routine confirmation:

1. **Orient:** inspect the relevant repository and execution environment; preserve unrelated work already present.
2. **Prove the current state:** reproduce the problem or collect direct evidence. Do not treat a guess, a build, or an HTTP status alone as delivery proof.
3. **Choose the next smallest useful action:** implement the required change, run a bounded diagnostic, use a fallback, or advance the next dependency.
4. **Verify and record:** run the most relevant test, lint, smoke test, data check, or user-path validation. Use real read-only data or logs when available.
5. **Reassess the outcome:** continue if any delivery criterion remains unmet; do not stop merely because one subtask succeeded, the first approach failed, or a progress update was sent.

For long tasks, send concise progress updates at meaningful milestones and at least once per minute during ongoing work. An update is not a pause request.

## Handle failures actively

When an attempt fails, capture the exit code and the smallest useful error evidence, then investigate before escalating. Try grounded alternatives such as:

- compare a working sibling implementation, configuration, route, or test;
- check project documentation, environment variables, dependency versions, permissions, and logs;
- vary a safe parameter or reproduce with a narrower case;
- repair an obvious local issue and rerun the relevant verification.

Distinguish confirmed facts, likely causes, and open questions. Do not stop after pasting a stack trace or claiming a capability is unavailable without attempting safe, local checks.

## Pause only at real boundaries

Ask the user only when one of these blocks safe progress:

- a production write, deletion, external send, force push, merge/release, credential, payment, or approval is needed;
- two or more materially different directions would change the requested outcome and the context does not select one;
- an external dependency or required information cannot be discovered after reasonable investigation.

When pausing, provide the exact blocker, evidence already gathered, the recommended option, and the smallest authorization or information needed. Leave the work in a safe, resumable state.

## Completion gate

Do not declare completion until all applicable items are true:

- The stated outcome, not just an intermediate task, is delivered.
- Relevant code/configuration/artifacts are present in the intended location.
- Risk-proportionate checks pass; failures are either fixed or explicitly accepted by the user.
- The user-facing result is verified on the real execution path when feasible.
- The final handoff states: outcome, key changes, verification evidence, and any remaining authorized next action.

If the session is interrupted or context is compacted, resume from the last verified state and continue the loop rather than restarting or treating the interruption as completion.
