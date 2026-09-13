# mcp-ratchet — DO-330 Tool Qualification Study

A worked example of taking a real AI-adjacent tool through the DO-330 tool
qualification process: what role it plays in a DO-178C activity, whether it
needs to be qualified at all, at what Tool Qualification Level, what its Tool
Operational Requirements are, how you would verify them, and an honest verdict
on how far the qualification actually goes.

The tool under study is [**mcp-ratchet**](https://github.com/YashRao10/mcp-ratchet)
— a security scanner and runtime drift monitor for MCP (Model Context
Protocol) servers. This study looks specifically at its **deterministic
tool-surface drift-detection function** used as a configuration-integrity
control for a separately-qualified AI verification tool.

## Why this is worth doing

If a DO-178C program credits an LLM-backed assistant (exposed over MCP) as a
verification tool, that assistant needs DO-330 qualification. A documented
hazard for MCP tools is that a server's advertised tool definitions can change
after a human approved them. A drift monitor that fingerprints the qualified
tool's interface and detects any post-approval change is a natural
configuration-integrity control — but if its "no drift" output is credited,
the monitor itself comes into scope for qualification. This study works that
question end to end. There is very little public material on qualifying
anything in the AI toolchain under DO-330.

## Read order

| # | Doc ID | Title | Status |
|---|--------|-------|--------|
| 1 | MR-TQ-001 | Tool Qualification Context & TQL Determination | done |
| 2 | MR-TQ-002 | Tool Operational Requirements | done |
| 3 | MR-TQ-003 | Tool Qualification Plan | done |
| 4 | MR-TQ-004 | Tool Verification Cases & Results | done (Rev 2026-08-30) |
| 5 | MR-TQ-005 | Tool Accomplishment Summary & Verdict | done (Rev 2026-08-30) |

Editable sources live in `docs-source/*.html`; rendered PDFs in `docs/`.

**Status:** the five-document set is complete. Verdict (MR-TQ-005 §4): the
drift-detection function at mcp-ratchet commit `907c8a9` meets TOR-1..11 and is
a defensible **candidate for TQL-5 under Criteria 3**. The three source defects
it turned up were fixed on mcp-ratchet before verification (commits `78d5971`,
`a054e4a`, `907c8a9`). A **cold independent re-execution and adversarial review**
(2026-08-30, MR-TQ-004 §7, `VERIFICATION-LOG.md`) re-confirmed the environment,
suite, counts and commits, found every TOR genuinely test-backed, and returned
"holds with minor caveats": five points where the prose outran the cited test,
three closed with new assertions (suite now 195), three accepted as
source-backed. A named human QA sign-off on a real program is still required.

This study is also vendored into the tool's own repository at
[`mcp-ratchet/qualification/`](https://github.com/YashRao10/mcp-ratchet/tree/main/qualification)
so it stays next to the code it qualifies; this repo is the standalone,
citable copy.

## Related material

[`EASA-ISSUE-03-CROSSREF.md`](EASA-ISSUE-03-CROSSREF.md) — a working memo
(2026-09-12, not part of the five-document set) checking this study's premise
against EASA's Proposed Issue 03 AI Concept Paper (published 2026-06-03,
still in public comment). Kept deliberately separate from MR-TQ-001..005:
MR-TQ-005 states outright that it "introduces no new analysis," and this
memo is new analysis against a source none of the five documents cite. Short
version: Issue 03 anticipates reusing ED-215/DO-330 for AI-based tools used
by approved organisations, which is close to this study's exact premise —
but a hazard classification for the credited AI assistant, in EASA's own
risk-based framework, has not been argued here, so treat this as
"compatible in principle," not as an extension of the verdict.

## Scope discipline

This study does not reproduce the paywalled RTCA DO-330 text, and does not
assert specific per-TQL objective counts from its tables. TQL-determination
criteria are cited from named secondary sources. Where the standard's exact
content is needed and not independently confirmable, the study says so rather
than guessing — the same discipline used in the sibling `AAS-TQ-002` study.
