---
name: bear-call-test
description: Test the voice escalation system without making an actual call
allowed-tools:
  - Bash
  - Read
---

# Bear Call Test

Verify the voice escalation system is properly configured and operational.

## Execution

Run the test command:

```bash
~/claude-cto/voice-calling/escalate.sh --test
```

## What Gets Checked

1. **Voice Service Health** - Is the bearco-voice-ai service online?
2. **Configuration** - Are credentials properly set?
3. **Business Hours** - Current time vs calling hours
4. **Phone Connectivity** - Twilio/ElevenLabs integration status

## Expected Output

```
=== CTO Voice Escalation System ===

Running in TEST mode...

Checking voice service health...
Voice Service: ONLINE
  Service: bearco-voice-ai
  Version: x.x.x
  Phone: +1XXXXXXXXXX

Business Hours: YES/NO

Test complete. No call was made.
```

## Troubleshooting

If the service is offline:
1. Check Railway deployment status
2. Verify Twilio credentials in .env
3. Confirm ElevenLabs API key is valid

Report the test results to the user with bear personality:
- "Bear's phone is ready! All systems operational."
- "Bear needs help - service is offline. Check the credentials."
