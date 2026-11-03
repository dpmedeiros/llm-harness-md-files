# Engineering writing evaluation briefs

These synthetic briefs exercise the skill's intended tasks. Run each in a fresh context, first without the new skill and then with it, keeping the brief unchanged.

Judge the observable criteria below; wording, heading choices, and bullet counts are flexible except where the brief explicitly fixes them. A baseline that already meets a criterion is a passing baseline.

## 1. Causal explanation

Given a timed lease with an explicit expiration rule, when the agent explains worker recovery, then the explanation preserves the timing and identifies the step that makes the job available again.

### Brief

Write a short explanation for an engineer new to our job service. A worker claims a job by storing its worker ID and a lease expiration timestamp in the database. It renews the lease every 10 seconds, setting expiration to 30 seconds after that renewal. A recovery scanner runs at times 0, 5, 10, 15 seconds and so on. It clears the worker ID when expiration is less than or equal to the current time. An unowned job is eligible for another worker to claim. Worker A renews at time 0 and immediately crashes. Explain when and how another worker can take over. We have no information about when another worker polls. Keep it understandable without assuming the reader knows what a lease is.

### Criteria

- Explain the stored claim and its time limit in context.
- Connect expiration at 30 seconds to the scanner clearing ownership, then eligibility for another claim.
- Distinguish eligibility at 30 seconds from the unknown actual takeover time.

## 2. Documentation for a new reader

Given a small service with a fixed startup procedure, when the agent writes a quickstart, then a new reader can perform the documented steps without invented prerequisites or service behavior.

### Brief

Write a README quickstart for a new engineer using our local event receiver. It accepts test events so engineers can try integrations without sending data to the production receiver. Docker must already be running. Start it with `docker compose up receiver`. It listens on `http://localhost:8080`. GET `/health` returns HTTP 200 with body `ok` when it can accept events. POST `/events` accepts a JSON object; the example event is `{"type":"test.ping","id":"demo-1"}`. The quickstart should let the reader confirm readiness before submitting that event. The provided facts do not describe authentication, persistence, dependencies inside the container, or production deployment.

### Criteria

- Open with what the local receiver is useful for.
- Put the Docker prerequisite and startup before readiness, then submission.
- Preserve commands, endpoint methods, and the sample JSON; avoid inventing authentication or durability guarantees.

## 3. Change summary with limited evidence

Given an implemented batching change and a compile check, when the agent writes a PR body, then the result fits the exact template and reports the available validation accurately.

### Brief

Write a PR body using exactly these headings, in this order: `## What`, `## Validation`, `## Risk`. Facts: the event importer now sends events to the repository in batches of up to 100 instead of one event per call. Event order and the existing transaction boundary are unchanged. `cargo check` passed. Tests and benchmarks were not run. There are no measured performance results. Keep the body concise and ready to paste into the PR.

### Criteria

- Use the exact requested headings and no added wrapper.
- Preserve batching, event order, and the transaction boundary.
- Identify `cargo check` as a compile check; preserve the missing tests and benchmarks without claiming verified performance or inventing a risk.

## 4. Engineering work message

Given a temporary operational choice with a deadline, when the agent drafts a team message, then the reader can identify the decision and consequence without invented urgency.

### Brief

Write a team chat message of at most 70 words. Staging's database certificate expires on November 12, 2026. Production uses a different certificate and is unaffected. We can rotate staging's certificate on November 10 during the existing maintenance window, or add a separate window on November 11. Recommend November 10 because it uses an existing window. Ask the on-call owner to choose by November 6. Keep the message calm and conversational.

### Criteria

- Preserve all dates and the scope of impact.
- Name the recommended option and its reason, while preserving the alternative.
- Ask the on-call owner for the decision by November 6 in at most 70 words.

## 5. Voice and template adaptation

Given a conversational voice sample and a fixed paragraph structure, when the agent rewrites an update, then it retains the factual limitations while following those supplied choices.

### Brief

Rewrite the update below as two short paragraphs, with no headings or bullets, matching this voice sample: "We found the retry loop. It was doing more work than it needed to. The patch is small, and I'd like another pair of eyes before we ship it." Keep the update's facts and uncertainty.

Update: "We added a cache to the schema lookup. In one local run, the importer finished in 8 seconds instead of 12 seconds. The input was 500 synthetic events on one developer's laptop. We have not measured production traffic or peak memory. We plan to run the full benchmark on Friday."

### Criteria

- Return two short paragraphs with no added headings, bullets, or critique.
- Follow the sample's direct, conversational voice without importing its retry-loop facts.
- Preserve the one-run basis, numbers, input, environment, unmeasured conditions, and planned benchmark.
