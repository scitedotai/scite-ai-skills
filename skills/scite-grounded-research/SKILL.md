---
name: scite-grounded-research
description: "Answer any research or literature question by grounding in the Scite MCP instead of the model's memory or raw web browsing — optimizing for both token cost and citation integrity. Use whenever a request involves finding, verifying, or synthesizing scientific literature: 'what does the evidence say about X', 'find papers on Y', 'verify this citation/DOI', 'has this paper been retracted', 'is this claim supported or contested', 'check these references before I submit', or any claim that needs a real, resolvable source. Also trigger when a user pastes a claim, a DOI, or a bibliography and wants it checked. Do NOT answer scientific-literature questions from parametric memory when this skill applies — ground first."
---

# Scite Grounded Research

Ground literature answers in the Scite MCP so citations come from the sources, not the model. This both cuts token cost (one structured ~15k-token call replaces 200k+ tokens of raw web HTML across several fetches, and lets a cheaper model tier do the work) and protects citation integrity (real DOIs, real supporting/contrasting classification, retraction flags).

**Core principle:** accuracy comes from the sources, not the model. A smaller model on grounded evidence beats a larger model working from memory.

## When to use

- A question about what the scientific literature says on a topic
- Verifying a claim, citation, or DOI before it reaches a manuscript or student essay
- Checking whether a foundational paper was retracted, corrected, or contradicted
- Synthesizing contested literature where supporting vs. contrasting matters

## When NOT to use

- Non-scholarly questions, opinion, or general knowledge with no citation burden
- The user explicitly wants the model's own reasoning without sources

---

## Workflow

### Step 1 — Ground before answering
Never draft a cited literature answer from memory. Call `Scite:search_literature` first. Use domain-specific technical terms (the index spans all fields, so broad phrases return noise). Keep `limit` small (10–20) to stay token-efficient — the whole point is fewer tokens, not more.

### Step 2 — Read the citation signal, not just the hit list
For each relevant paper, look at the `tally`: `supporting`, `contrasting`, `mentioning`. A high contrasting count is a flag that the finding is contested — report it. Check `retraction_notices` and the `has_retraction` / `has_concern` / `has_correction` filters for integrity issues. This is the step that catches what an ungrounded model misses.

### Step 3 — Verify any user-supplied citation exactly
If the user pastes a DOI or reference, fetch it by `dois:` with no `term` to confirm it's real and get true metadata. A DOI that returns nothing is a likely fabrication — say so plainly.

### Step 4 — Answer from the retrieved evidence only
Cite author, year, journal, and DOI from the returned records — never a DOI reconstructed from memory. When the literature is split, present both sides using the supporting/contrasting classification rather than smoothing it into false consensus.

### Step 5 — State the honest limit
Grounding sharply reduces fabrication; it does not eliminate the need for human verification. When coverage is open-access-only or a claim rests on a single record, say so.

---

## Token-efficiency habits baked in

- **One structured call over many raw fetches.** Prefer a single well-targeted `search_literature` call to repeated broad ones.
- **Small `limit`, use `offset` to paginate** only if needed.
- **Fetch metadata without a `term`** (pass `dois`/`titles` alone) when you only need to verify — cheaper than a full-text search.
- **Let the tier drop.** Because the evidence is pre-digested, a smaller model can do the summarizing — don't reach for the largest model by default.

## What good output looks like

A short, sourced answer that: states what the evidence says, names supporting AND contrasting work when the finding is contested, flags any retraction/correction, gives real resolvable DOIs, and notes where human verification is still needed. Never a confident single-source claim when the tally shows disagreement.
