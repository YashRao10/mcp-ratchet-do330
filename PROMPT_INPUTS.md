# PROMPT_INPUTS — mcp-ratchet DO-330 Tool Qualification Study

Verbatim record of the user prompts that drove this project, per the standing
"every project keeps a raw prompt log" directive. Newest at the bottom.

---

## Session 2026-08-29 — project kickoff

> ok what else should we do and what is the new project that we work on

> what is it going to do because I dont know anything about DO-330

> go ahead and use mcp and you are going to start building this one

Interpretation confirmed in-thread: "use mcp" = use **mcp-ratchet** as the
tool being qualified (chosen from the three candidates offered — the
compliance-navigator agent, mcp-ratchet, or a small purpose-built tool).
The project is a worked DO-330 tool-qualification package for an AI-adjacent
tool, rendered in the house document template (HummingBird Technosys, Inc.).

---

## Session 2026-09-12 — EASA Issue 03 cross-reference

A peer Claude session (running on a newly set-up Mac) researched next-project
ideas and proposed: "Re-evaluate mcp-ratchet-do330 under EASA's new W-shape/
Trustworthiness Levels framework (Issue 03 AI Concept Paper, June 2026) —
nobody's mapped an existing DO-330 case study against it yet."

> yeah dig in

Verified the underlying claim independently (fetched and text-extracted the
actual 239-page Proposed Issue 03 PDF rather than trusting the secondhand
summary) before acting on it. Found the "Trustworthiness Levels" framing was
imprecise — no such separate scale exists, it's still AL/TQL via a new
risk-based allocation table — but found a genuinely load-bearing citation
(§3.3.6 preamble, p.85) that anticipates exactly mcp-ratchet-do330's premise:
reusing ED-215/DO-330 tool qualification for AI-based systems used by
approved organisations. Wrote up the full analysis in
`EASA-ISSUE-03-CROSSREF.md` (working memo, not yet folded into the numbered
doc set) with a recommendation for a short, honestly-scoped addition to
MR-TQ-005 rather than a new document or an overclaim of EASA endorsement.
