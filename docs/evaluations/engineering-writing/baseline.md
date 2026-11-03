# Baseline writing samples

These are the unedited responses to the [five briefs](scenarios.md), collected on 2026-11-03 before the new skill was written. Each brief ran in a fresh agent context instructed to use only the brief, without tools or skills. Fenced contents are evaluation data.

## 1. Causal explanation

````text
Another worker can claim the job once the scanner clears Worker A’s ID at time 30 seconds. The actual takeover time depends on when another worker polls, which we don’t know.

At time 0, A renews its claim by setting the expiration timestamp to time 30. That timestamp is the deadline for A’s ownership unless it renews again. A crashes immediately, so no further renewals happen. The scanner leaves A’s ID in place on scans before time 30. At time 30, the expiration equals the current time, so the scanner clears A’s ID. The job is then unowned and eligible for another worker to claim.
````

## 2. Documentation for a new reader

````text
Use the local event receiver to try integrations with test events without sending data to the production receiver. Make sure Docker is running before you start.

Start the receiver:

```sh
docker compose up receiver
```

In a second terminal, check whether it is ready to accept events:

```sh
curl -i http://localhost:8080/health
```

Wait until the response has HTTP status `200` and body `ok`. Then submit the test event:

```sh
curl -X POST http://localhost:8080/events \
  -H 'Content-Type: application/json' \
  -d '{"type":"test.ping","id":"demo-1"}'
```

The `/events` endpoint accepts a JSON object.
````

## 3. Change summary with limited evidence

````text
## What

Send imported events to the repository in batches of up to 100 instead of one event per call. Event order and the existing transaction boundary are unchanged.

## Validation

`cargo check` passed. Tests and benchmarks were not run.

## Risk

Performance impact has not been measured.
````

## 4. Engineering work message

````text
Staging’s database certificate expires on November 12, 2026. Production uses a different certificate and is unaffected.

I recommend rotating staging’s certificate on November 10 because we already have a maintenance window scheduled. We can also add a separate window on November 11.

Could the on-call owner choose a window by November 6?
````

## 5. Voice and template adaptation

````text
We added a cache to the schema lookup. In one local run, the importer finished in 8 seconds instead of 12. That was 500 synthetic events on one developer's laptop.

We haven't measured production traffic or peak memory yet. We plan to run the full benchmark on Friday.
````
