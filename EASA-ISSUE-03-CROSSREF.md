# Cross-reference: mcp-ratchet-do330 against EASA AI Concept Paper, Proposed Issue 03

Working memo, not yet a formal doc in the read-order set. Drafted 2026-09-12
to evaluate whether this study's DO-330 tool-qualification package holds up
against EASA's newer AI-specific certification framework (Proposed Issue 03,
published 2026-06-03, open for a 10-week public comment period).

**Source used:** the actual Proposed Issue 03 PDF (239 pages), fetched and
text-extracted directly — not a secondary summary. Citations below are to
that document.

## Correcting the starting claim

The prompt for this work described EASA's framework as introducing "Trustworthiness
Levels" as a new classification scheme alongside the W-shape process. That is
imprecise. The document does not define a separate "Trustworthiness Level"
scale. What it actually does:

- Keeps the existing **AL/TQL (Assurance Level / Tool Qualification Level)**
  scale (AL2/TQL2 through AL6), the same scale DO-178C/DO-330 already use.
- Adds a new **AI trustworthiness analysis** building block (safety/risk,
  security, ethics-based assessments) that gates the rest of the process, and
  a **hazard-classification-to-AL/TQL allocation table** (Table 6, keyed off
  a separate risk-level table, Table 5) as the *mechanism* for arriving at
  the TQL for an "AI constituent."
- Wraps all of this in the **W-shape process**: a dual-V structure where the
  first V handles the AI/ML model's own data-driven lifecycle (data
  management → model training → model verification) and the second V is the
  classical implementation/verification V-cycle, joined where the trained
  model is implemented into deployable software/hardware.

So: same TQL scale, new *risk-based route* to a TQL number, plus a new
gating trustworthiness-analysis phase — not a parallel level system.

**Also worth flagging for anyone writing about this publicly:** this
document's own use of "MCP" means *multicore processor* (fitting: it's an
avionics hardware/software assurance paper), not Model Context Protocol.
Pure acronym collision with mcp-ratchet's domain — do not conflate the two
in anything citing this paper.

## The load-bearing finding

Table 6 (p.42, §RA-05, Anticipated MOC) allocates AL/TQL by hazard
classification for an "AI constituent":

| Hazard class | AL/TQL (acceptable risk) | AL/TQL (moderate risk / net safety benefit) |
|---|---|---|
| H1 | n/a | n/a |
| H2 | AL2/TQL2 | AL3/TQL3 |
| H3 | AL3/TQL3 | AL4/TQL4 |
| H4 | AL5/TQL5 | AL5/TQL5 |
| H5 | AL6 | AL6 |

Separately, and more directly relevant, §3.3.6's preamble (p.85, Anticipated
MOC SU-IMP-04) states:

> "In the case of AI-based systems used by approved organisations, software
> development assurance guidance might not be available. In such a case,
> existing 'tool qualification' industry standards (such as ED-215/DO-330)
> can be used, the applicable objectives being modulated through the
> determined TQL."

This is close to a direct hit on this study's premise. "AI-based systems
used by approved organisations" is exactly the mcp-ratchet-do330 scenario:
an LLM-backed verification assistant, used by a DO-178C program (an approved
organisation), where classical software development assurance guidance
doesn't apply cleanly to an LLM. EASA's own anticipated guidance says: use
DO-330/ED-215 for this, with the TQL determined via the new risk-based
process (Table 5/6) rather than assumed.

## What this means for the existing case study

MR-TQ-001 already determines TQL-5/Criteria-3 for mcp-ratchet's
drift-detection function via classical DO-330/DO-178C reasoning (the
function supports a credited LLM verification tool; drift in the LLM's
advertised tool surface after approval is the hazard being controlled). That
reasoning is **not contradicted** by EASA Issue 03 — it's the kind of
scenario EASA anticipates needing exactly this kind of standard reuse.

What EASA's framework adds, and what this study doesn't yet have, is an
explicit **hazard classification (H1-H5) for the AI constituent** — i.e.,
for the LLM-backed verification assistant itself, not for mcp-ratchet's
drift-detector directly. The drift-detector is deterministic, not itself an
"AI constituent" under this framework; it's the configuration-integrity
control *supporting* the AI constituent, same relationship DO-330 already
models (a tool supporting a qualified item). Table 6's AL/TQL would attach
to the LLM assistant based on the hazard of it being wrong; that TQL would
then flow down to mcp-ratchet the same way TOR-1..11 already derive their
rigor from TQL-5 in the existing study.

**Concretely, a hazard classification for the LLM assistant would need to be
argued** (something MR-TQ-001 currently derives from DO-178C-side reasoning,
not an EASA-style hazard/risk table) before this cross-reference could claim
more than "compatible in principle." That argument isn't in scope for this
memo — it would require a specific program context (what failure conditions
follow from the assistant being wrong), which the existing study deliberately
avoids inventing (see its own "Scope discipline" section).

## Recommendation

Worth a short, honestly-scoped addition to the existing 5-doc set — likely
a new short section in MR-TQ-005 (Accomplishment Summary) rather than a full
new document, titled something like "Cross-reference: compatibility with
emerging EASA AI certification guidance (Issue 03, June 2026)." It should:

1. State the finding above (Issue 03 anticipates exactly this reuse pattern).
2. Explicitly flag what's *not* established: no hazard classification (H1-H5)
   has been argued for the LLM assistant in this study, so "TQL-5" here is
   asserted via DO-330 mechanics, not yet cross-derived via EASA's own Table
   5/6 risk route. State this as an open item, not a gap being papered over.
3. Not claim EASA endorsement of mcp-ratchet specifically — Issue 03 is a
   proposed, comment-period document as of this writing (2026-09), not yet
   adopted guidance.

This keeps the same "measure the measurement honestly" discipline the rest
of this study (and the sibling spec-conformance-evals project) already uses,
rather than overclaiming a regulatory tailwind that isn't fully there yet.

**Not done in this pass:** actually writing that MR-TQ-005 addition, or
re-rendering the PDFs. Flagging the finding + draft language for Yash to
decide whether/how to fold in.
