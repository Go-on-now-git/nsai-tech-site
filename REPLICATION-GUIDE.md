# NSAI Deployment Replication Guide
## How to Set Up NSAI for a New Client

**By Not So Holdings LLC | (352) 698-7333**

---

## OVERVIEW

Total setup time: ~4–6 hours (spread across 2 days)
Client experience: Operational within 48 hours of signing

---

## STEP 1 — CONSULTATION CALL CHECKLIST

Before touching any tech, answer these questions:

**Their workflow:**
- [ ] What's their primary role/business?
- [ ] What are their top 3 time-wasters?
- [ ] What tools do they currently use? (email, CRM, calendar, Slack, etc.)
- [ ] What do they want automated first?
- [ ] What should NSAI *never* do without asking?

**Technical:**
- [ ] What device do they have available? (Android preferred, or do they want hosted?)
- [ ] Are they comfortable with Telegram? (Best primary channel)
- [ ] What other channels do they want? (WhatsApp, Discord, Signal)
- [ ] Do they have any APIs or services they want connected? (n8n, Stripe, CRM, etc.)

**Contract:**
- [ ] Which plan? (Starter / Operator / Enterprise)
- [ ] Payment method?
- [ ] Send contract via DocuSign before proceeding

---

## STEP 2 — TECHNICAL REQUIREMENTS

### Option A: Client's Own Android Device (Recommended)
- Android 10+ with at least 6GB RAM
- Install Termux from F-Droid (NOT Play Store)
- Install proot-distro: `pkg install proot-distro && proot-distro install debian`
- Enter Debian: `proot-distro login debian`
- Install Node.js: `apt update && apt install nodejs npm curl git -y`

### Option B: Provider-Hosted (VPS)
- Spin up a VPS (DigitalOcean $6/mo Droplet works)
- Ubuntu 22.04+, 1GB RAM minimum
- Client connects via Telegram only — no device needed

### Option C: Client's Laptop/PC
- Any Linux/macOS/WSL2 environment
- Same install steps as Option A after getting a shell

---

## STEP 3 — OPENCLAW INSTALLATION

```bash
# Run inside Debian/Ubuntu shell
curl -fsSL https://install.openclaw.ai | bash
# or
npm install -g openclaw

# Initialize
openclaw init

# Start gateway
openclaw gateway start
```

Configuration file: `~/.openclaw/openclaw.json`
- Set model API keys (OpenAI, Anthropic, etc.)
- Configure channel plugins

---

## STEP 4 — WORKSPACE CONFIGURATION

Create and customize these files in `~/.openclaw/workspace/`:

### SOUL.md — Personality & Behavior
Define how NSAI speaks and acts. Key things to customize:
- Tone (professional, casual, direct)
- What it should proactively monitor
- Any off-limits actions
- When to ask for confirmation vs. act independently

### USER.md — Client Profile
```markdown
# USER.md
- Name: [Client name]
- Role: [Their job/business]
- Timezone: [e.g., Eastern]
- Company: [Company name]
- Key contacts: [Who matters most]
- Priorities: [What they care about most]
```

### IDENTITY.md — Agent Identity
```markdown
# IDENTITY.md
Name: [Custom name or "NSAI"]
Emoji: ⚡
Mission: [Specific to their business]
```

### HEARTBEAT.md — Proactive Tasks
List what NSAI should check periodically:
```markdown
# HEARTBEAT.md
- Check inbox every 2 hours, flag urgent items
- Monitor [their specific watchlist]
- Alert if [specific conditions]
```

---

## STEP 5 — CHANNEL SETUP

### Telegram (Primary — do this first)
1. Message @BotFather on Telegram
2. `/newbot` → give it a name → get the token
3. Add token to `~/.openclaw/openclaw.json`:
```json
{
  "plugins": {
    "telegram": {
      "token": "YOUR_BOT_TOKEN",
      "allowedUsers": [CLIENT_TELEGRAM_USER_ID]
    }
  }
}
```
4. Client starts a conversation with their bot
5. Test: send "hello" — should respond

### WhatsApp (Optional)
- Requires linking via QR code scan
- Run `openclaw whatsapp link` and have client scan
- More setup friction — only if client specifically wants it

### Discord (Optional)
- Create a Discord bot at discord.com/developers
- Add token to openclaw.json under discord plugin
- Invite bot to client's server

---

## STEP 6 — N8N WORKFLOW DEPLOYMENT (Optional but powerful)

If client wants automation workflows:

1. Install n8n: `npm install -g n8n && n8n start`
2. Access at: `http://localhost:5678`
3. Import workflows from `/nsai-showcase/n8n/` directory
4. Configure OpenAI credentials in n8n settings
5. Activate desired workflows
6. Add webhook URL to NSAI config so it can trigger workflows

Key workflows to deploy:
- `nsai-demo-workflow.json` — personalized demo generator
- Build client-specific workflows during onboarding week

---

## STEP 7 — FIRST WEEK ONBOARDING CHECKLIST

**Day 1:**
- [ ] Telegram channel tested and working
- [ ] Client sent first message and got a response
- [ ] SOUL.md and USER.md filled with real client info
- [ ] HEARTBEAT.md configured with their first monitoring tasks

**Day 2-3:**
- [ ] First automation workflow live (their top pain point)
- [ ] Client has had 3+ real interactions
- [ ] Memory building — NSAI has learned basic preferences

**Day 4-5:**
- [ ] Check-in call with client (15 min)
- [ ] Adjust tone/behavior based on feedback
- [ ] Add 2nd and 3rd workflows based on what they're asking for most

**Day 7:**
- [ ] Client satisfaction check
- [ ] Document what's working
- [ ] Upsell additional channels or workflows if on Starter plan

---

## STEP 8 — MONTHLY MAINTENANCE

Each month, check:
- [ ] API keys still valid (OpenAI, Anthropic, etc.)
- [ ] n8n workflows running without errors
- [ ] Memory files not getting too large (archive old daily files)
- [ ] Client happy — ask for feedback and a testimonial
- [ ] New capabilities available in OpenClaw? Update if so
- [ ] Any new automation the client wants? Add to scope or upsell

**Monthly check-in:** 15-minute call or Telegram check-in. Ask:
1. What's NSAI doing well?
2. What's still taking too much of your time?
3. Anything you wish it did differently?

---

## STEP 9 — PRICING & BILLING SETUP

**Recommended:**
- Stripe (stripe.com) — set up recurring subscriptions
- Send invoice links via Telegram/email
- Plans: $297/mo (Starter), $597/mo (Operator), custom (Enterprise)

**Billing trigger:** Send invoice on Effective Date each month.
**Grace period:** 7 days before suspension warning, 14 days before suspension.

**Upsell opportunities:**
- Additional channel: +$50/mo
- Custom API integration: $200-500 one-time
- Enterprise upgrade: move to custom pricing
- Referral program: give client $50 credit per referral who signs

---

## QUICK REFERENCE: CLIENT SETUP TIME ESTIMATE

| Task | Time |
|------|------|
| Consultation call | 30 min |
| Device setup + OpenClaw install | 45–90 min |
| Workspace config (SOUL/USER/IDENTITY) | 30 min |
| Telegram bot setup | 15 min |
| First workflows configured | 60 min |
| Testing & tweaking | 30 min |
| **Total** | **~4–5 hours** |

---

*Questions: Justin Perry | (352) 698-7333 | Not So Holdings LLC*
