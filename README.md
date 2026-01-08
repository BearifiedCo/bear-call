# Bear Call

Voice escalation for AI agents. When Claude needs immediate human attention, Bear makes it happen with a phone call.

**By BearifiedCo** | MIT License

## The Problem

AI agents working autonomously sometimes need urgent human input:
- Production is down and rollback decision needed
- Security issue detected requiring immediate action
- Budget approval blocking critical work
- Complex judgment call that can't wait

Slack messages get lost. Emails pile up. But a phone call? That gets attention.

## The Solution

Bear Call lets Claude Code make actual voice calls using ElevenLabs AI voice synthesis and Twilio telephony.

```
/bear-call "Production API returning 500 errors, need rollback approval" --urgency critical
```

Bear's calling! The human's phone rings with a professional AI voice explaining the situation.

## How It Works

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Claude Code   │────▶│  ElevenLabs AI  │────▶│  Twilio Voice   │
│   (Bear Call)   │     │  (Voice Agent)  │     │  (Phone Bridge) │
└─────────────────┘     └─────────────────┘     └─────────────────┘
                                                        │
                                                        ▼
                                                ┌─────────────────┐
                                                │  Human's Phone  │
                                                └─────────────────┘
```

## Prerequisites

Bear Call requires a configured voice calling backend:

1. **ElevenLabs Account** - AI voice synthesis
2. **Twilio Account** - Phone call infrastructure
3. **bearco-voice-ai Service** - Orchestration (Railway deployment)

See `~/claude-cto/voice-calling/README.md` for backend setup.

## Installation

### From Source

```bash
# Clone the plugin
git clone https://github.com/bearifiedco/bear-call.git

# Use with Claude Code
claude --plugin-dir /path/to/bear-call
```

### Add to Your Project

```bash
cp -r bear-call ~/.claude/plugins/
```

## Commands

### `/bear-call <reason> [--urgency level]`

Make a voice call with the specified reason and urgency.

```
/bear-call "Database connection pool exhausted" --urgency critical
/bear-call "Weekly sync ready" --urgency low
```

**Urgency Levels:**

| Level | Behavior |
|-------|----------|
| `critical` | Immediate call, retry 3x if no answer |
| `high` | Call within 5 minutes |
| `normal` | Call within 30 minutes |
| `low` | Queue for business hours |

### `/bear-call-test`

Test the voice system without making an actual call.

```
/bear-call-test
```

### `/bear-call-history`

View recent call history and queued calls.

```
/bear-call-history
```

## Escalation Skill

Bear Call includes an escalation guidance skill that helps Claude decide when a voice call is appropriate vs other communication methods.

### When to Call

- Production down
- Security breach
- Data at risk
- Blocking issue with time pressure

### When NOT to Call

- Status updates (use Slack)
- Questions that can wait (use email)
- Non-urgent blockers (use ClickUp/Linear)

## Configuration

Bear Call uses the voice-calling backend at `~/claude-cto/voice-calling/`.

Required environment variables (in `.env`):
- `VOICE_SERVICE_URL` - bearco-voice-ai Railway URL
- Twilio and ElevenLabs credentials (backend-side)

## Architecture

```
bear-call/
├── .claude-plugin/
│   └── plugin.json       # Plugin manifest
├── commands/
│   ├── bear-call.md      # Main call command
│   ├── bear-call-test.md # Test command
│   └── bear-call-history.md # History command
├── skills/
│   └── escalation-guidance/
│       └── SKILL.md      # When to escalate
└── README.md
```

## Requirements

- macOS/Linux
- Node.js (for voice-calling backend)
- Claude Code
- Configured voice-calling backend

## Comparison with CallMe

| Feature | Bear Call | CallMe |
|---------|-----------|--------|
| **Voice Quality** | ElevenLabs (premium) | OpenAI TTS |
| **Architecture** | Cloud-hosted (Railway) | Local + ngrok tunnel |
| **Reliability** | Production-grade | Depends on local uptime |
| **Urgency Levels** | 4 levels (critical/high/normal/low) | Single level |
| **Business Hours** | Auto-respected (override available) | Not handled |
| **Retry Logic** | 3x automatic for critical | Manual |
| **Multi-turn Chat** | Callback system | Built-in |
| **Escalation Guidance** | Skill included | Not included |
| **Cost** | ~$0.02-0.03/min | ~$0.03-0.04/min |
| **Setup** | Backend required | Self-contained |

### When to Choose Bear Call

- Production environments needing reliability
- Teams with existing infrastructure (Railway, etc.)
- When voice quality matters (ElevenLabs)
- Need for urgency-aware escalation logic
- Business hours awareness

### When to Choose CallMe

- Quick local testing
- Minimal setup preference
- Don't want to manage backend services
- Need multi-turn conversations built-in

## Bear Suite Integration

Bear Call works with Bear Pair for complete AI-human collaboration:

```
Human receives Bear Call
        ↓
"Start a Bear Pair session"
        ↓
/bear-call-spawn-pair "Fix the API errors"
        ↓
Driver + Navigator work on fix
        ↓
Navigator catches issue → Bear Call alerts human
        ↓
Human guides → Bears continue
```

**Commands:**
- `/bear-call-spawn-pair <task>` - Spawn Bear Pair from a call context

**Install both for full Bear Suite:**
```bash
claude --plugin-dir ~/plugins/bear-call --plugin-dir ~/plugins/bear-pair
```

## Future Plans

- [ ] Two-way conversation support
- [ ] Callback handling
- [ ] SMS fallback for low urgency
- [ ] Multi-recipient calls
- [ ] Call transcription

## License

MIT License - Free to use, modify, and distribute.

## Credits

**BearifiedCo** - Making AI development friendlier, one bear at a time.

Built with:
- [ElevenLabs](https://elevenlabs.io) - AI Voice Synthesis
- [Twilio](https://twilio.com) - Voice Infrastructure

---

*"When the bear calls, you answer."*
