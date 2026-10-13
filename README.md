# Gmail Life Admin

**Life admin for your inbox.** Stop missing bills, get your email under control, and know what actually needs you today. Just ask Claude in plain words. No coding needed.

Made for anyone who juggles bills, bank alerts, deliveries, appointments and a never-ending stream of promotions: households, freelancers and busy professionals.

## What it does for you

| | Ask Claude | What happens |
|---|---|---|
| **Clean up your inbox** | "Clean up my inbox and tell me what to unsubscribe from." | Groups your email by sender, shows what's piling up, unsubscribes you from the ones you pick and moves old promotions to Trash. |
| **Organize it for good** | "Set up labels for my Gmail." | Sorts all your mail into labels like Finance, Bills & Utilities, Government, Shopping and Travel, and keeps sorting new mail automatically. Low-priority mail can skip your inbox. |
| **Never miss a bill** | "Put my bill due dates on my calendar." | Finds bills and payment reminders, adds each due date to Google Calendar with reminders a few days before, and warns you about anything overdue. |
| **Know what needs you** | "What in my email needs me today?" | A short summary: bills due, security alerts and people waiting for a reply, with everything else just counted. Can arrive every morning. |

Start with a cleanup, organize what's left, then let the bill reminders and daily summary keep you on top of it.

### What the daily summary looks like

```
📬 Inbox digest — last 24 hours

Needs action (3)
• Electricity bill — pay by Fri 17 Oct
• New sign-in to your Google account from a new device — check it was you
• Maria (landlord) — asked when you can do the inspection

Good to know (2)
• 2 deliveries arriving tomorrow
• Streaming subscription price goes up next month

Background: 41 promotions · 6 newsletters · 9 job alerts
```

## Safe by design

- **Asks before every change.** You see the plan first and choose what to do.
- **Never permanently deletes.** Old mail only goes to Trash, so you can get it back.
- **Never pays anything** and never clicks payment links. Bill reminders are only calendar events.
- **Never types your password.** You sign in yourself.
- **Watches for scams.** Suspicious "pay now" or "verify your account" emails are flagged, not acted on.
- **Keeps details private.** Only the last 4 digits of account numbers, and no amounts in summaries unless you ask.

The daily summary only reads your email. It never changes anything.

## Get started

You need a Claude account with the **Gmail** and **Google Calendar** connectors.

1. In the Claude app or claude.ai, go to **Customize > Plugins**.
2. Choose **Add > Add marketplace** and enter `Annalog-404/gmail-life-admin`.
3. Find **Gmail Life Admin** in the list and choose **Add**.
4. In **Customize > Connectors**, connect **Gmail** and **Google Calendar** if they aren't already.

That's it. Ask in plain words in a chat or in Cowork, or type `/` and pick a skill. The plugin is saved to your account, so it also shows up in Claude Code.

**For cleanup and labels:** changing Gmail filters and bulk-deleting old mail happens in a browser where you're signed in to Gmail. Claude uses the [Claude in Chrome extension](https://chromewebstore.google.com/detail/claude/fcoeoabgfenejglbffodgkkbkcdhcgfn) or the desktop app's built-in browser for this. The bill reminders and daily summary don't need it.

## More things to try

- "Which emails should I delete?"
- "Make all my bank emails go to a Finance label."
- "Do I have any bills due this week?"
- "Give me an inbox summary every weekday at 8am."
- "What came in over the last 7 days that I should know about?"

## Questions

**Does it read all my email?** Only what the task needs: the last 24 hours for a summary, bill emails from the last 60 days, or the senders in your inbox for a cleanup.

**Can it send emails as me?** No. None of the skills send email.

**Can I undo a cleanup?** Yes. Deleted mail sits in Gmail's Trash for 30 days, and labels and filters can be removed in Gmail settings at any time.

**Does it work with Outlook or Yahoo?** Not yet. It's built for Gmail and Google Calendar.

## For developers

These are open [Agent Skills](https://agentskills.io), packaged as a Claude Code plugin. They work in Claude Code, Cowork and any agent that supports the Agent Skills standard.

| Skill | What it does |
|---|---|
| [inbox-cleanup](skills/inbox-cleanup/SKILL.md) | Groups mail by sender and volume, recommends what to unsubscribe from, delete and keep, then unsubscribes and moves mail to Trash in bulk. |
| [email-labeling](skills/email-labeling/SKILL.md) | Designs a label scheme, labels existing mail, creates filters for future mail, and sets skip-inbox and label colors. |
| [bill-reminders](skills/bill-reminders/SKILL.md) | Extracts due dates from bill emails and creates Google Calendar events with reminders, skipping paid bills and existing events. |
| [inbox-digest](skills/inbox-digest/SKILL.md) | Read-only summary of recent mail, sorted into needs action, good to know and background. |

### What's inside

```
.claude-plugin/
├── plugin.json                     # Plugin manifest
└── marketplace.json                # Lets people install it with /plugin
skills/
├── inbox-cleanup/
│   ├── SKILL.md
│   └── references/
│       └── gmail-web-ui.md         # Bulk delete and unsubscribe techniques
├── email-labeling/
│   ├── SKILL.md
│   ├── references/
│   │   └── gmail-web-ui.md         # Filter import, label removal, bulk mark-read, label colors
│   └── assets/
│       └── filters-template.xml    # Gmail filter import template
├── bill-reminders/
│   ├── SKILL.md
│   └── references/
│       └── extraction-patterns.md  # Due-date, status and amount patterns
└── inbox-digest/
    ├── SKILL.md
    └── references/
        └── buckets.md              # What counts as "needs action", with search hints
```

### Install options

Two ways to install the same four skills:

| | Plugin | Copying the skill folders |
|---|---|---|
| Install | Two commands in Claude Code | Copy folders into `.claude/skills/` |
| Updates | Automatic | Copy again by hand |
| Commands | `/gmail-life-admin:inbox-digest` | `/inbox-digest` |
| Choose which skills | All four together | Any you want |
| Works in | Claude Code and Cowork | Claude Code and any [Agent Skills](https://agentskills.io/clients) agent |
| Customizing | Fork the repo | Edit the files directly |

Pick the plugin if you just want to use them. Copy the folders if you use another agent, want only some skills, or want to edit them.

#### As a Claude Code plugin

In Claude Code, run:

```
/plugin marketplace add Annalog-404/gmail-life-admin
/plugin install gmail-life-admin@annalog-404
```

All four skills are installed together and stay up to date. Run them as `/gmail-life-admin:inbox-digest`, `/gmail-life-admin:bill-reminders`, `/gmail-life-admin:inbox-cleanup` and `/gmail-life-admin:email-labeling`, or just ask in plain words. The same plugin also installs in Cowork.

#### By copying the skill folders

Copy the skills into your project, so everyone working in the repo gets them:

```bash
mkdir -p .claude/skills
cp -r skills/* .claude/skills/
```

Or install them just for yourself, in every project:

```bash
mkdir -p ~/.claude/skills
cp -r skills/* ~/.claude/skills/
```

You can copy just the ones you need, e.g. `cp -r skills/inbox-digest ~/.claude/skills/`.

##### One-time browser setup (for email-labeling and inbox-cleanup)

These two skills change Gmail settings and run bulk actions, which needs a browser. Do this once:

1. Install the [Claude in Chrome extension](https://chromewebstore.google.com/detail/claude/fcoeoabgfenejglbffodgkkbkcdhcgfn) and sign in to it.
2. In Claude Code, run `/chrome` and choose **Enabled by default**.
3. Restart Claude Code.

Skills can't do this for you: copying a skill folder doesn't run anything, and Claude Code doesn't let project files turn on browser access, so a repo can't connect Claude to your browser on its own. inbox-digest and bill-reminders don't need it.

#### Other agents

These follow the open [Agent Skills specification](https://agentskills.io/specification), so they work with any compatible agent. Copy the folders under `skills/` into the folder your agent loads skills from. The [client list](https://agentskills.io/clients) links to each agent's setup docs.

### Requirements

| Skill | Gmail access | Google Calendar access | Browser tool |
|---|---|---|---|
| inbox-cleanup | Read and modify | – | For bulk delete and unsubscribing |
| email-labeling | Optional | – | Required |
| bill-reminders | Read | Write | – |
| inbox-digest | Read | Optional | – |

Gmail and Calendar access come from MCP servers or API connectors. Gmail connectors can't change Gmail settings, so filters, label colors and bulk actions go through the browser tool, where you sign in to Gmail yourself.

In Claude Code, the browser tool is Claude in Chrome (needs Chrome or another Chromium browser and a Pro, Max, Team or Enterprise plan). The first time a skill needs the browser, Claude Code offers to install the extension and connects it in the same session; you just click **Add to Chrome**. You can also set it up yourself: install the [Claude in Chrome extension](https://chromewebstore.google.com/detail/claude/fcoeoabgfenejglbffodgkkbkcdhcgfn), then start Claude Code with `claude --chrome`. To skip the flag in future, run `/chrome` once and choose **Enabled by default**.

If you install the extension partway through a session and the browser still isn't available, restart with `claude --chrome --continue`. Your conversation carries over, so the skill picks up where it left off. Without a browser, email-labeling writes a filter file for you to import yourself.

### Validate

```bash
pip install skills-ref
for dir in skills/*/; do agentskills validate "$dir"; done
```

This also runs automatically on every push via GitHub Actions.

## License

[MIT](LICENSE)
