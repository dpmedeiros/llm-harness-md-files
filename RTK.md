# Command output

Command output here is condensed to save tokens, keeping every signal and
dropping costly noise. Treat it as the complete result: run commands
normally, and batch related commands into one call to avoid extra turns.
Truncated results state their recovery path in their own output. Re-run a
command as `rtk bypass <cmd>` only when its result is unusable: empty when
output was clearly expected, contradicting its exit code, or garbled.

When the RTK hook is active, shell commands are rewritten automatically. Use these direct commands when needed:

```sh
rtk gain               # Show token savings analytics
rtk discover           # Analyze Claude Code history for missed opportunities
rtk proxy <cmd>        # Execute a raw command without filtering (for debugging)
```
