# claude-mentor-skills

Three drop-in skills for Claude Code (and any agentic coding session) that counter failure modes observed repeatedly in agentic coding sessions with strong models — especially Opus 5: defending conclusions after their reasons die, litigating against the user instead of helping, confidently inventing numbers, writing code on unverified assumptions about the layer beneath, tests that prove nothing, and changelogs that claim fixes for bugs the session itself introduced.

> **Unofficial community project. Not affiliated with or endorsed by Anthropic. Claude, Claude Code, and Opus are referenced solely to describe compatibility and the behaviours these skills address.**

Every rule here is anchored to a **real, documented incident** from production repos with daily agent use — nothing is hypothetical. The receipts that survive anonymisation are public-library facts anyone can check (what `pyperclip.copy()` does at the Win32 layer, `SendInput` atomicity, PostgREST's silent 1,000-row truncation, harness-pinned commit trailers). These skills are ready to use as-is: no placeholders, no "insert your example here".

## The skills

| Skill | Role | Fires when | Counters |
|---|---|---|---|
| **craft-mentor** | General repository craft and investigation | Session start / picking up work | Symptom-level fixes, unfalsified hypotheses, hunk-level reading, re-flagging deliberate choices, dishonest verification claims |
| **build-mentor** | Safe implementation and build discipline | Writing or modifying code | Unverified dependency layers, invented mechanisms the platform already provides, mocks that inherit your misunderstanding, verification that destroys what it checks, fabricated fix provenance, false doc absolutes |
| **opus5-mentor** | Opus 5-specific review, stance, reasoning, and pushback discipline | Reviewing, judging, verdicts, pushback, disputes | Conclusion-anchoring, preservation bias, fabricated figures in verified register, verification-by-cheapness, prosecuting the user, bimodal concessions |

`opus5-mentor` is designed specifically around recurring Opus 5 pain points documented in the evidence base; it is also useful when another model displays similar behaviour (the evidence base includes exactly such an incident from a different Claude model).

They are split because they need different triggers to fire at all: a session that is *building* never hits "review this plan". The most severe session reviewed while developing these skills — two data-loss criticals shipped inside a feature marketed as a safety mechanism, three fabricated changelog entries — would not have invoked a review-shaped skill even once.

## Install

**Claude Code, per project:** copy the `skills/` folders into your repo's `.claude/skills/`:

```
your-repo/.claude/skills/craft-mentor/SKILL.md
your-repo/.claude/skills/build-mentor/SKILL.md
your-repo/.claude/skills/opus5-mentor/SKILL.md
```

**Claude Code, all projects:** copy them into `~/.claude/skills/` instead.

Claude Code discovers skills placed in the project or user skills directory. Start a new session if a newly added skill does not appear immediately. Invoke manually with `/craft-mentor`, `/build-mentor`, `/opus5-mentor` — or let the trigger descriptions fire them automatically.

**claude.ai (chat):** each skill ends with a portable block — paste it into project instructions or a style. You lose the tool-enforced parts but keep the behavioural rules.

**The circuit breaker (the most useful habit):** if a session starts arguing with you instead of helping, type `/opus5-mentor` mid-argument. The skill instructs the model to drop the dispute, restate your actual ask in one line, and serve it. In our use it has been effective partly because the protocol was derived from documented examples of the behaviour it addresses — some of them written up by the model itself.

## Where these came from

Built and battle-tested through sustained daily use across production repositories and multiple coding agents; distilled from incident write-ups, two independent cold-context audit reports, and a self-analysis brief the model wrote about its own behaviour when shown receipts. The design philosophy throughout is **receipts over commandments**: models follow examples harder than imperatives, so each rule carries the concrete incident that earned it. The tenth commandment gets ignored; the story about the clipboard that emptied itself does not.

Two honesty notes, in the spirit of the thing:

- These reduce the failure modes; they do not eliminate them. A rule in context competes with behaviour in weights. The tool-enforced habits (baseline checks, reading dependency source, cold-context audits) do more than any prose.
- `opus5-mentor` was created around failure modes that clustered in Opus 5 sessions, and that is where it earns its keep. Similar behaviours can surface elsewhere — one incident in the file was committed by a different Claude model while writing the first version of that very skill — and the protocol is useful there too, but Opus 5 is the primary target, not a stand-in for "any model".

If you adopt these and your own sessions generate scars, append them to the relevant section with the same discipline: incident, mechanism, rule. That is optional — the skills work as shipped.

## License

Released under the MIT License. See [LICENSE](LICENSE).

This is an unofficial community project and is not affiliated with or endorsed by Anthropic.
