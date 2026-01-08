---
name: bear-call
description: Make a voice call to escalate urgent matters. Bear's calling!
argument-hint: "<reason> [--urgency critical|high|normal|low]"
allowed-tools:
  - Bash
  - Read
---

# Bear Call - Voice Escalation Command

Initiate an outbound voice call when something truly requires immediate human attention.

## Usage

Parse the user's input for:
1. **Reason** - What needs to be communicated (required)
2. **Urgency** - One of: critical, high, normal, low (default: normal)

## Urgency Levels

| Level | When to Use | Behavior |
|-------|-------------|----------|
| `critical` | Production down, security breach, data loss | Immediate call, retry 3x |
| `high` | Major blocker, deployment failure | Call within 5 minutes |
| `normal` | Important update, decision needed | Call within 30 minutes |
| `low` | FYI, weekly sync, status update | Queue for business hours |

## Execution

Run the voice escalation script:

```bash
~/claude-cto/voice-calling/escalate.sh --reason "<reason>" --urgency <urgency>
```

## Before Calling

1. Verify this truly needs a phone call (not just a message)
2. Confirm urgency level matches the situation
3. Keep the reason concise but informative

## Example Commands

```bash
# Critical - production issue
~/claude-cto/voice-calling/escalate.sh --reason "Database connection pool exhausted, API returning 500s" --urgency critical

# High - needs decision
~/claude-cto/voice-calling/escalate.sh --reason "Third-party API rate limit hit, need approval for paid tier" --urgency high

# Normal - important but not urgent
~/claude-cto/voice-calling/escalate.sh --reason "Completed infrastructure migration, ready for review" --urgency normal

# Low - informational
~/claude-cto/voice-calling/escalate.sh --reason "Weekly CTO status update ready" --urgency low
```

## Response Format

After initiating the call, report:
- Call status (initiated/queued/failed)
- Call SID (if available)
- Any follow-up actions needed

## Bear Personality

When reporting the call:
- "Bear's calling! Reaching out to the human..."
- "Call connected! The bear has made contact."
- "No answer - bear will try again shortly."
