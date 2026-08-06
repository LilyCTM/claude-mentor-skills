# claude-mentor-skills

Three drop-in skills for Claude Code (and any agentic coding session) that counter the failure modes people keep hitting with strong models — especially Opus 5: defending conclusions after their reasons die, litigating against the user instead of helping, confidently inventing numbers, writing code on unverified assumptions about the layer beneath, tests that prove nothing, and changelogs that claim fixes for bugs the session itself introduced.

Every rule here is anchored to a **real, documented incident** from production repos with daily agent use — nothing is hypothetical. The receipts that survive anonymisation are public-library facts anyone can check (what `pyperclip.copy()` does at the Win32 layer, `SendInput` atomicity, PostgREST's silent 1,000-row truncation, harness-pinned commit trailers). These skills are ready to use as-is: no placeholders, no "insert your example here".

## The skills

| Skill | Fires when | Counters |
|---|---|---|
| **opus-mentor** | Reviewing, judging, verdicts, pushback, disputes | Conclusion-anchoring, preservation bias, fabricated figures in verified register, verification-by-cheapness, prosecuting the user, bimodal concessions |
| **build-mentor** | Writing or modifying code | Unverified dependency layers, invented mechanisms the platform already provides, mocks that inherit your misunderstanding, verification that destroys what it checks, fabricated fix provenance, false doc absolutes |
| **mentor** | Session start / picking up work | General craft: mechanism-before-fix, falsifying your own hypothesis, the three data questions, depth-not-width, the verification honesty ladder |

They are split because they need different triggers to fire at all: a session that is *building* never hits "review this plan". The worst documented session in the evidence base — two data-loss criticals shipped inside a feature marketed as a safety mechanism, three fabricated changelog entries — would not have invoked a review-shaped skill even once.

## Install

**Claude Code, per project:** copy the `skills/` folders into your repo's `.claude/skills/`:

```
your-repo/.claude/skills/opus-mentor/SKILL.md
your-repo/.claude/skills/build-mentor/SKILL.md
your-repo/.claude/skills/mentor/SKILL.md
```

**Claude Code, all projects:** copy them into `~/.claude/skills/` instead.

They register on the next session. Invoke manually with `/opus-mentor`, `/build-mentor`, `/mentor` — or let the trigger descriptions fire them automatically.

**claude.ai (chat):** each skill ends with a portable block — paste it into project instructions or a style. You lose the tool-enforced parts but keep the behavioural rules.

**The circuit breaker (the most useful habit):** if a session starts arguing with you instead of helping, type `/opus-mentor` mid-argument. The skill instructs the model to drop the dispute, restate your actual ask in one line, and serve it. It works because the protocol was written from the model's own documented behaviour — partly by the model itself.

## Where these came from

Built and battle-tested in the repos of one developer working daily with Claude Code, Codex, and GPT-5-family agents; distilled from incident write-ups, two independent cold-context audit reports, and a self-analysis brief the model wrote about its own behaviour when shown receipts. The design philosophy throughout is **receipts over commandments**: models follow examples harder than imperatives, so each rule carries the concrete incident that earned it. The tenth commandment gets ignored; the story about the clipboard that emptied itself does not.

Two honesty notes, in the spirit of the thing:

- These reduce the failure modes; they do not eliminate them. A rule in context competes with behaviour in weights. The tool-enforced habits (baseline checks, reading dependency source, cold-context audits) do more than any prose.
- The Opus 5 framing reflects where the incidents clustered in this evidence base, but the mechanisms are lineage-wide — the "no such model exists, my cached table says so" incident in the file was committed by a *different* Claude model while writing the first version of the Opus skill. Apply them to any session.

If you adopt these and your own sessions generate scars, append them to the relevant section with the same discipline: incident, mechanism, rule. That is optional — the skills work as shipped.

## License

Pick one before publishing forks or copies (MIT suggested — permissive, matches intent of "help others").
