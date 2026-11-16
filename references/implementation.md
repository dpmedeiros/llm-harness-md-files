# Independent implementation

Use test-driven development (TDD): write the test first, run it, and observe it fail for the expected reason before beginning the corresponding production implementation or fix. Repeat this sequence for each behavior change. A test that has not been run, already passes, or fails because of an unrelated setup error does not satisfy this requirement.

- The coordinating agent defines scope, passes the specification and agreed test interfaces to each agent, manages handoffs, and verifies results. Delegate test and production code edits to the agents below.
- The test-writing agent owns test creation and changes. It derives expected behavior from the specification and hands off the test command, failing result, and explanation of why the failure demonstrates the required missing behavior.
- The implementation agent begins production code changes only after the coordinating agent verifies the failing-test evidence. It writes code to pass those tests and must not change tests or expected results to make its implementation pass.
- A third, distinct fixing agent handles production code corrections after implementation, including test failures and review findings. Send any necessary test corrections back to the test-writing agent, with evidence that the test conflicts with the specification; preserve required behavior.
- Keep these roles in distinct agent instances with separate contexts. Pass the specification, relevant code, and observed results explicitly at each handoff. Preserve the roles through repeated test and implementation cycles, and keep any required independent review agents separate. If agent tools are unavailable, report the limitation instead of silently combining roles.
