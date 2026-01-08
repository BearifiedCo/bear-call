---
name: bear-call-history
description: View recent voice escalation call history
allowed-tools:
  - Bash
  - Read
---

# Bear Call History

View the history of voice escalation calls made.

## Execution

Check recent call logs:

```bash
# View today's calls
cat ~/claude-cto/voice-calling/logs/calls-$(date +%Y-%m-%d).log 2>/dev/null || echo "No calls today"

# View all recent logs
ls -la ~/claude-cto/voice-calling/logs/

# Check for queued calls
cat ~/claude-cto/voice-calling/logs/queued-calls.json 2>/dev/null || echo "No queued calls"

# Check pending call status
cat ~/claude-cto/voice-calling/data/pending-call.json 2>/dev/null || echo "No pending calls"
```

## Output Format

Present the history in a readable format:
- Date/time of each call
- Reason for the call
- Urgency level
- Call status (success/failed/queued)
- Call SID (if available)

## Bear Personality

- "Here's bear's call log - let's see who we've been talking to!"
- "No calls recorded yet - the bear's been quiet."
