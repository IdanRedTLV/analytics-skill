# Analytics Skill for Claude Code

A Claude Code skill that helps you instrument product analytics correctly — applying consistent naming conventions, discovering events systematically, and producing a structured tracking plan ready for implementation.

---

## What it does

The skill works through 6 steps in order:

1. **Gather context** — understands the feature, flow, or screen from screenshots, PRDs, plain descriptions, or codebases, and identifies your analytics platform
2. **Apply naming conventions** — enforces Title Case, Verb+Noun event names, consistent property names, and correct property type labelling
3. **Discover events** — systematically identifies events across 7 categories: screens, core actions, secondary actions, dialogs, errors, flow start/end, and settings
4. **Output a tracking plan** — produces a markdown table with Event Name, Trigger, Business Question, Implementation, and Status columns
5. **Validate** — silently checks all conventions before presenting output and fixes any violations
6. **Offer next steps** — offers JSON/CSV export, code snippets, codebase coverage review, or iteration

---

## Installation

Clone or download this repository, then run:

```bash
mkdir -p ~/.claude/skills/analytics
cp .claude/skills/analytics/SKILL.md ~/.claude/skills/analytics/SKILL.md
```

---

## Usage

Type `/analytics` in any Claude Code session, optionally followed by the feature or screen name:

```
/analytics
/analytics checkout flow
/analytics onboarding screen
```

Accepted inputs: screenshots, PRDs, plain descriptions, or a codebase. The skill adapts its approach based on what you provide.

---

## Output

The skill produces a markdown table with one row per event:

| Event Name | Trigger | Business Question | Implementation | Status |
|---|---|---|---|---|
| Title Case, Verb + Noun | When exactly this fires | The business question it answers | Frontend / Backend / Frontend + Backend | New Event / Existing Event |

A one-line screen summary follows the table. Full structured JSON export is available on request, as well as CSV, Notion table, and platform-specific schemas (Mixpanel, Amplitude, Segment, PostHog).

---

## Naming conventions

The skill enforces 10 conventions on every output:

1. **Title Case** — all event and property names use Title Case with spaces
2. **Verb + Noun** — event names follow an action structure: `Send Message`, `View Profile`, `Add to Cart`
3. **User perspective** — events describe what the user does, not what the system records (`Send Message`, not `Message Sent`)
4. **Balanced granularity** — use properties for context, not separate events; different business purposes get separate events
5. **Consistent property names** — the same concept uses the same property name across all events
6. **Act On pattern** — dialogs and modals use a single event with an `Action` property (Confirm / Cancel / Close)
7. **Action Property grouping** — similar grouped actions use one event with an `Action` or type property
8. **Duration tracking** — time-in-flow flows use View + Leave event pairs with a `Duration(s)` or `Duration(m)` property
9. **Property type labelling** — every property is clearly labelled as Event, User, or Super
10. **Position as percentage** — UI interaction events include screen position as 0-100 percentage values; system events omit the field entirely

---

## License

MIT
