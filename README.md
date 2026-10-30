# From Broken Instrument to Redesigned Protocol

**Auditing an LLM-as-a-Judge Pipeline for RAG-Based Academic Mentorship**

Poster presented at the **RISE AI Latin America Summit 2026** (Education Track).

Juan Pablo Fuentes-Abarca, Gabriel Astudillo, Isabel Hilliger
Pontificia Universidad Católica de Chile

📄 [`poster.pdf`](./poster.pdf)

---

## What this is

We were building a RAG-based mentoring assistant for early-career women faculty in Chilean higher education. To compare configurations we used an LLM judge, and the first results didn't make sense: the judge gave a 91.67% faithfulness score to a baseline that had **no retrieved passages at all**, so grounding was impossible.

Instead of continuing the benchmark, we treated the evaluation pipeline itself as the object to study. This poster summarizes what the audit found and how we redesigned the protocol, using a Design Science Research framing and a setup a small team can afford (single annotator, commercial APIs, 196 generated responses).

## What we found

- **Hallucinated grounding.** The judge accepted fluent parametric knowledge as documentary evidence in the zero-retrieval control.
- **Prompt-metadata leakage.** Theoretical references in the rubric prompt turned into an unwritten scoring checklist: the judge penalized missing author names in 86.1% of GPT rationales (58.8% for the second judge, MiniMax M3).
- **Agreement is not validity.** Two judges from different model families agreed strongly (AC2 = 0.849), but a share of that agreement came from both following the same leaked instruction.
- **Ceiling effects and length bias.** Two rubric dimensions saturated at the top level, and scores tracked response length despite explicit instructions to ignore it.
- **The apparent RAG penalty.** RAG configurations scored about two points lower, but 83.7% of their responses were retrieval refusals. On the small subset of non-refused answers the gap shrinks substantially.

## What we changed

The redesigned protocol replaces prompt instructions with structural controls:

1. Atomic factual verification separated from qualitative scoring.
2. Behaviorally Anchored Rating Scales (BARS) written as observable positive behaviors, with theory citations removed from prompts.
3. Ex-ante applicability masks, so irrelevant dimensions are marked N/A before looking at outputs.
4. Full-sample reporting of abstentions, and **care routing**: when the system lacks institutional context, the response is routed to a human support channel instead of a bare refusal.

## Limitations

- One annotator, who was likely unblinded to condition, so the human-judge alignment is not independent validation.
- Small effective samples in the non-refused subset (as low as N = 1 in some cells); those results are indicative only.
- The protocol was refined after auditing the same 196 outputs, so it still needs out-of-sample validation.
- Chilean Spanish, one national context.

## Funding

Supported by the Instituto Milenio Fundamentos de los Datos (IMFD) and FONDECYT Grant No. 1241537 (ANID, Chile).

## Contact

juan.fuentes@uc.cl · [LinkedIn](https://www.linkedin.com/in/jotapefuentes/)
