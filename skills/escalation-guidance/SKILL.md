---
name: Escalation Guidance
description: This skill should be used when the user asks about "when to call", "should I escalate", "urgency levels", "phone escalation", "voice call decision", or needs guidance on whether a situation warrants a voice call vs other communication methods.
version: 1.0.0
---

# Escalation Guidance

Determine when voice escalation is appropriate versus other communication methods.

## Decision Framework

### Voice Call (Bear Call)

Use voice escalation when:

1. **Time-Critical** - Decision needed within minutes, not hours
2. **Blocking** - Work cannot continue without human input
3. **High Stakes** - Production down, security issue, data at risk
4. **Async Failed** - Slack/email not answered, situation worsening

### DO NOT Call For

1. **Status updates** - Use Slack/email instead
2. **Questions that can wait** - Queue for next business hours
3. **Information requests** - Search docs or wait for async response
4. **Minor blockers** - Work on something else meanwhile

## Urgency Selection Guide

### Critical (Immediate Call)

- Production systems completely down
- Security breach detected
- Data loss occurring
- Payment processing failure
- User data exposed

### High (Call Within 5 Minutes)

- Deployment failed, rollback needed
- Major feature broken after release
- Third-party integration down
- Approaching deadline with blocker

### Normal (Call Within 30 Minutes)

- Decision needed on architecture
- Budget approval required
- External commitment needs confirmation
- Complex problem needs human judgment

### Low (Queue for Business Hours)

- Weekly status sync
- FYI on completed work
- Non-urgent questions
- Planning discussions

## Escalation Alternatives

Before calling, consider:

| Alternative | When to Use |
|-------------|-------------|
| Slack DM | Can wait 15-30 minutes |
| Email | Can wait hours |
| ClickUp task | Can wait days |
| Linear issue | Technical, trackable |
| human-dri-queue.md | Needs human but not urgent |

## Best Practices

1. **Be Specific** - Clear reason helps human prioritize
2. **Be Brief** - Phone calls should be quick
3. **Be Prepared** - Have details ready when they answer
4. **Follow Up** - Document the outcome

## Business Hours

Default business hours: 9 AM - 6 PM local time (avoid calling outside unless critical)

Use `--force` flag to override business hours check when truly critical.
