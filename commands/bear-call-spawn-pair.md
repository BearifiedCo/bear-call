---
name: bear-call-spawn-pair
description: During or after a Bear Call, spawn a Bear Pair session to work on the issue
argument-hint: "<task-from-call>"
allowed-tools:
  - Bash
  - Read
  - Write
---

# Bear Call + Bear Pair Integration

When a Bear Call escalation identifies a task that needs immediate AI attention, spawn a Bear Pair session to tackle it.

## The Flow

```
Human receives Bear Call → "Work on this" → Bear Pair spawns
    ↓
Driver + Navigator tackle the issue
    ↓
Human gets status updates
```

## Usage

After or during a Bear Call, the user says something like:
- "Start a Bear Pair session on this"
- "Have the bears work on it"
- "Spawn a pair session for this issue"

## Execution

1. Generate a session ID based on the call context
2. Spawn the Bear Pair session with the task

```bash
# Generate session ID
SESSION_ID=$(date +%Y%m%d%H%M%S)-call

# Check if Bear Pair plugin is available
if [ -d ~/claude-cto/plugins/bear-pair ]; then
  # Spawn Bear Pair session
  ~/claude-cto/plugins/bear-pair/scripts/pair-orchestrator.sh start "$SESSION_ID" "<task-description>"
  echo "Bear Pair session spawned: $SESSION_ID"
else
  echo "Bear Pair plugin not installed at ~/claude-cto/plugins/bear-pair"
fi
```

## Context Passing

When spawning from a call:
1. Include the original call reason as the task
2. Add urgency context (critical calls get priority)
3. Reference the call SID for traceability

## Example

```bash
# From a critical call about API errors
~/claude-cto/plugins/bear-pair/scripts/pair-orchestrator.sh start "20260107-call-critical" \
  "URGENT from Bear Call: Production API returning 500 errors. Investigate and fix. Call SID: CA123..."
```

## Response

Report to the user:
- "Bear Pair activated! Driver and Navigator are on it."
- Session ID for tracking
- How to check status: `/bear-status <session-id>`
- How to stop when done: `/bear-stop <session-id>`

## Bear Suite Philosophy

Bear Call and Bear Pair work together:
- **Bear Call** = Human attention when needed
- **Bear Pair** = AI attention in parallel
- Together = Human-AI collaboration at its finest
