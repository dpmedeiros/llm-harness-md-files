# Testing

## Behavior-driven tests

Use Given/When/Then style for every test, in every language.

- Name each test after its starting conditions, action, and observable outcome. Use
  `given_<context>_when_<action>_then_<outcome>` for identifier-based test names and natural-language
  equivalents for test descriptions. Name behavior rather than implementation phases.
- Separate the body into explicit Given, When, and Then sections with blank lines and comments,
  or the test framework's equivalent constructs. Given prepares the state; When performs the action;
  Then asserts its observable result. Keep the action out of the assertions.
- Cover one behavior per scenario. Split unrelated scenarios into separate tests. Table-driven
  scenarios may vary inputs for the same behavior, with a clear Given/When/Then flow for each case.

## Unit tests for new scripts

Every new script gets unit tests in the same change, whatever the language: Python, shell, JS, hook
scripts, one-off tooling. Put them wherever the repo keeps its tests, in the repo's test framework.
Cover the decision logic with real inputs, including the cases that must not trigger. Keep the
script's logic in importable functions so tests can call them without running the whole script.
When a script can't be tested as written, restructure it until it can.
