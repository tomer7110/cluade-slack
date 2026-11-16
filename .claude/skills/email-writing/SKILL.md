---
name: email-writing
description: Use when Tomer asks to reply to, answer, draft, write or rewrite an email (English or Hebrew), or forwards an email thread into Slack and wants a response - anything that will be sent under Tomer Amsallem's name.
---

# Email writing in Tomer's voice

Built from Tomer's real sent mail (Velo threads with investors, banks, lawyers, accelerators, vendors, candidates, plus Hebrew threads). Real examples by situation are in `examples.md`. Read it when the situation isn't obvious.

## Workflow for a reply

1. **Find the thread.** Use the link, subject, sender or keywords Tomer gave → `mcp__Gmail__search_threads` → `mcp__Gmail__get_thread` (full thread, not the search preview). Reply to the **latest** message and read everything above it. If several threads match, list them in one line each and ask which one.
2. **Get call context** when the sender is someone Tomer has met or the thread mentions a call. Follow the `call-context` skill (search Spinach by the person's name and the company). Use what was actually said or agreed: promised docs, follow-up dates, numbers.
3. **Check the calendar** when the reply proposes or accepts a time. Use `mcp__Google_Calendar__list_events` or `suggest_time` and offer 2 concrete windows. Never write "let me know what works" without windows.
4. **Decide the basics:**
   - *Language*: same as the incoming email.
   - *Length*: match the moment. Confirmations are one line. Most replies are 20–60 words. Over 120 words needs a reason.
   - *We vs I*: "we" by default (Tomer + Adi / Velo). "I" only for things Tomer did himself.
   - *Sign-off*: see the table below.
5. **Draft** following the voice rules below.
6. **Deliver in Slack**, in this order:
   - `Suggested subject: …` on one plain line, only for a new thread (omit for replies).
   - A code block containing only the email, greeting through sign-off.
   - `Context used: …` on one line (e.g. "Spinach call 14 Sep: Ethan said he'd send a startup package"), then any open question.

   Then offer: "Want me to put it in Gmail as a draft?" If he says yes, call `mcp__Gmail__create_draft` with `replyToMessageId` = the latest message id, `to`/`cc` copied from the thread (reply-all if others were CC'd, especially Adi), plain-text `body`, `includeSignature: false` (the body already ends with the sign-off). If the thread is a Velo thread that Tomer answers from tomer@sendwithvelo.com, mention that the draft is in the Gmail account and he may want to switch the From address.
   **Never call `mcp__Gmail__reply` or `send_message` without an explicit "send it".**

## Voice rules

**Shape**
- Greeting on its own line, then a blank line.
- One idea per line. Most "paragraphs" are a single sentence with blank lines between them.
- Order: greeting → (thanks / context, one line) → the answer or ask, said plainly → logistics (times, attachments) → short thanks → sign-off.
- No bullet lists, headers, bold, or em-dashes in the email. Numbered `1)` `2)` is fine only when answering a list of requested details.

**Greetings**: `Hi [First name],` (default) · `Hey [First name],` (warm/peers) · `Hi Charlie & Larry,` (two people) · `Dear [Name],` (formal/legal/bank ops) · Hebrew: `היי [שם],`

**Sign-offs (replies)**

| Situation | Ending |
|---|---|
| Normal back-and-forth, scheduling, quick answers | `Regards,` / `Tomer` |
| Closing a loop, thank-you, decline, first reply to an intro | `Best Regards,` / `Tomer` |
| Message from both founders (feedback thanks, updates) | `Tomer & Adi` |
| One-line confirmation | no sign-off, or just the line: `Sounds great, see you then` |
| Hebrew | `תודה` / `תודה רבה` / `בברכה,` / `תומר` |

Often a `Thank you very much.` or `Thanks again,` line sits right before the sign-off. Don't add the full signature block. Gmail appends it.

**Phrases he actually uses**
- Asks: "We would love to…" (his main phrase for asking anything) · "Could you please send a meeting invite?" · "Please let us know what works best for you."
- Thanks: "Thanks again for the call the other week." · "Thank you for the update, and for taking the time to review the deck." · "We really appreciate it."
- Intro replies: "Nice to e-meet you." + "[Introducer], thanks for the intro." (moving the introducer to BCC isn't his habit, so don't add it)
- Follow-ups: "As promised, …" · "As we discussed, I am attaching…" · "When we met in August, you asked us to remind you on September 15th… So here is our reminder,"
- Scheduling: offers windows with the day and time, 24h clock or "9 am", timezone when cross-border ("17:00 Israel time", "morning/noon EST").
- Being late or rescheduling: honest and short. "Something unexpected came up on our end…" / "I'll be five minutes late. I'm running late from another meeting."
- Declining or getting declined: gracious. "Completely understandable. We appreciate your clarity and quick response." / "We would love to keep you posted as we grow."
- Hebrew: "שלומי מצויין, מה שלומך?" · "אשמח ל…" · "נשמח להמשיך איתכם" · 🙏 or :) once, near thanks · "סליחה על הדיליי😅"

**Keep his imperfections, within limits**
- Ending a line with a comma before the blank line ("Yeah that works,", "Looking forward to hearing from you,") is his. Keep 1–2 of these per email.
- Loose, natural grammar and `&` instead of "and" are fine.
- Don't copy his typos ("lisenses", "atatched", "u"). A draft should read like Tomer on a careful day, not like a mistake.
- Never polish into consultant English: no semicolons, no "I hope this email finds you well", "please don't hesitate to reach out", "circle back", "touch base", "leverage", "synergies", "per my last email".

**Explaining Velo** (only when the recipient doesn't know it): one sentence + one concrete example. "We are a platform that connects different payment apps across borders. For example, Venmo/Zelle in the US to PayBox/Bit in Israel."

## Before you hand over the draft

- Does every fact (date, time, price, promise, name spelling) come from the thread, Spinach or the calendar? If not, use a `[placeholder]` and flag it.
- Is it the right length for the moment? Cut any sentence that doesn't move the thread forward.
- Does it answer every question the sender asked, in order?
- Are the right people on it (Adi CC'd if she was on the thread)?
- Is there no subject line inside the code block?

## Common mistakes

| Mistake | Fix |
|---|---|
| Replying from the search snippet | Always `get_thread` and read the latest message |
| "Let me know when works for you" | Two concrete windows from the calendar |
| Long, warm, polished paragraph | 3–6 short lines, one idea each |
| Full signature block pasted in | `Regards,` + `Tomer` only |
| Inventing what was agreed on a call | Check Spinach, quote the meeting in "Context used" |
| English reply to a Hebrew email | Mirror the language |
