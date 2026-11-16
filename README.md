# claude-slack-assistant

Tomer's assistant for Claude in Slack. Tag `@Claude` in Slack, pick this repository, and Claude loads `CLAUDE.md` and the skills in `.claude/skills/`.

## What it can do

| Skill | Ask it | What happens |
|---|---|---|
| `email-writing` | "@Claude reply to Edona's last email about the registered agent" | Reads the Gmail thread, pulls call context from Spinach, checks the calendar if there's scheduling, and drafts the reply in Tomer's voice. A Gmail draft is created only when asked. Nothing is ever sent without an explicit "send it". |
| `call-context` | "@Claude what did we agree with Cross River on minimums?" | Searches Spinach calls and answers with meeting links. |

## Requirements

These connectors must be connected in claude.ai → Settings → Connectors, for the account that uses Claude in Slack:

- Gmail
- Spinach AI
- Google Calendar
- Slack

## Layout

```
CLAUDE.md                          # who Tomer is, routing, hard rules, Slack formatting
.claude/skills/
  email-writing/SKILL.md           # reply workflow + voice rules
  email-writing/examples.md        # real replies by situation
  call-context/SKILL.md            # how to search Spinach and cite calls
```

## Adding a capability

1. Create `.claude/skills/<skill-name>/SKILL.md` with frontmatter:
   ```
   ---
   name: <skill-name>
   description: Use when <the requests that should trigger it>
   ---
   ```
2. Add a row to the skills table in `CLAUDE.md`.
3. Test it from Slack with a real request, then commit.

## Updating the voice

Tomer's style changes. When drafts start feeling off, ask: "@Claude go over my last 30 sent replies and update the email-writing skill". Add any good new reply to `examples.md`.
