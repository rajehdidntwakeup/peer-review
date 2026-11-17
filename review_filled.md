# COMPLETED REVIEW (draft answers on template)

## Standard Review Form of MDPI Journals
Paper reviewed: "How Do AI Coding Agents Contribute to Software Development? An Empirical Study of Agentic Pull Requests", Mazloomzadeh, Morovati, Khomh (arXiv:2607.21832, 43 pages, preprint July 2026).

### Rating legend
High / Average / Low / No Answer

### Part A — criteria (filled)
- Originality / Novelty: **Average**
- Significance of Content: **High**
- Quality of Presentation: **Average**
- Scientific Soundness: **Low** *(methodology needs major refinement; see "Points to improve")*
- Interest to the readers: **High**
- Overall Merit: **Average**

### Expertise / Justification (global)
The paper has a timely and important topic (AI coding agents), provides a large-scale empirical dataset and analyses, makes a clear contribution set (longitudinal agent comparison, task-level characterization, defect proneness). Main black boxes are method-level: LLM-summarization feeding the BERTopic, SZZ precision issues, GLMM reporting dropouts, only merged PR comparisons.

### Table 1 (quality checklist)
| Question | Yes | Can be improved | Must be improved | Not applicable |
|---|---|---|---|---|
| Does the introduction provide sufficient background and include all relevant references? |  | X |  |  |
| Is the research design appropriate? |  |  | X |  |
| Are the methods adequately described? |  | X |  |  |
| Are the results clearly presented? |  | X |  |  |
| Are the conclusions supported by the results? |  | X |  |  |

Reasons:
- Intro reads well but references over-rely on 2026 preprints and contains a condensed list (refs [23] etc.). Can be improved.
- Research design: third-party bug-inducing and LLM topics need a stronger verification framework: production-only or merged-only restriction.
- Methods are detailed with tools/numbers; also some missing random seeds, summarization prompt etc., hence can be improved.
- Results clear, but inconsistent metrics and over-interpretation.
- Conclusions largely supported, but "non-significant differences" and "strong differences" wording requires consistency.

### English language and style
**Option selected:** English language and style are fine / minor spell check required (specific typos: "Finlay" → "Finally" (Intro); "Result" → "Results"; "agenic" → "agentic"; numeric-percentage reported as "84.2%" for Cohen's κ vs 0.842 in the threats section).

### Overall Recommendation
**Selected:** Reconsider after major revision (the major flaws in design: the defect-proneness and topic filtering paths could compromise the primary headline results; however, requested fixes are achievable with existing data).

### Comments and suggestions for authors (summary, strong points, points to improve, details) (≈ half A4 page)

**Summary (neutral).**
This study uses the AIDev dataset and GitHub REST API to examine 220,612 closed PRs from 489 popular Python repositories carrying 9,428 agentic PRs from five coding agents (Claude Code, Codex, Copilot, Cursor, Devin). It answers three research questions. (1) It evaluates the mergeability of agentic PRs (across agents and quarterly periods of repository activity) using a binomial generalized linear mixed model, finding Claude highest (84.3%) and relative stability across quarters (~63.7–68.2%, no significant pairwise differences). (2) It applies BERTopic, preceded by gpt-4.1-mini summaries, to identify 24 resulting development-task categories and finds heavy use for documentation, dependency updates, and tests. (3) On a balanced 2,275/2,275 sample, it compares PRs' complexity and bug-inducing commit rates between agentic and human-generated PRs and reports comparable-to-lower defect association. The study is ambitious, clear, and well organized, but three methodological pillars need refinements.

**Strong points.**
- Real-world impact: agent evaluation at scale (PR level, longitudinal) rather than synthetic tasks.
- Clear RQ structure and stated hypotheses; triangulated analyses.
- Topic-method validation on a stratified 100-PR sample with inter-rater agreement (κ 0.842).
- Results include both statistical significance and effect sizes (Cliff's δ and Cramér's V).
- Comprehensive and candid Threats section and a public replication package.
- Good figures (boxplots + ratio plots per topic and quarter).

**Points that need attention (and why).**
1. Bug-inducing conclusions are algorithm dependent. Bookmarking: Szz + keyword-defined bug-fixes; PyDriller SZZ is acknowledged with low precision (0.39) and no ground truth is used on this data. The prevalence story (lower bug induction by agents) can be affected. Recommendation: provide a manual oracle on a subset, report the sensitivity to keyword sets.
2. Mixed-effects model lacks diagnostics. Only EMMs and Tukey p-values shown; no random-effects variance, model CIs, AIC/likelihood metrics, or explicit agent × quarter interaction. The “no temporal effect” and “difference less pronounced in Q4” statements need stronger quantitative support.
3. Topic labelling relies on LLM summarization. Summaries are unvalidated as inputs to BERTopic; evaluator model overlap / prompt not given. Compare against raw title + body BERTopic results.
4. RQ3 restriction to merged PRs restricts scope and may inflate agent quality (selected-on-acceptance). Recommend sensitivity including rejected samples / weighting.
5. Quarter boundaries are self-referential (start from the first agentic PR) — short activity spans make Q4 edge cases; clarify repository inclusion difference between Table 1 (≥1 A-PRs, n 489) and Table 2 (≥2 A-PRs, n ~309).
6. Effect size interpretations and signs: clarify Cliff's δ direction, e.g. Table 7's Cursor changed-LOC comparison says p=0.375 but no practical meaning; in Table 5 explain "Cursor higher (OR less than 1?)".
7. Editorials: fix "Finlay", "Result", "agenic". Also κ formatting: 84.2% vs 0.842; consistency on text construction.
8. Self-citation signal: research may be benefiting from recent unpublished (2026) preprints. Consider re-anchoring claims on peer-reviewed sources.

**Part B — non-standard review tasks assignment to this paper (detailed in attached evidence file).**

### Part B-A. Level and rating of publication venue
- Listed venue: **Proceedings of the ACM on Measurement and Analysis of Computing Systems (POMACS), Vol. 37 No. 4, Article 111, (July 2026)**; SIGMETRICS-associated ACM journal.
- CORE journal rankings discontinued Feb-2022; companion conference **SIGMETRICS** ranked **A\*** on CORE; POMACS standalone has no CORE rank.
- Acceptance ratio reported in recent editorials: 16.8–20.7% (Vol. 8-10 2024–2026).
- According to the course scale, this is in the **[30%–15%): "selective"** band.
- Comment: An apparent mismatch: paper is on empirical SE (mining PRs / coding agents), whereas a measurement-and-analysis community typical of POMACS/SIGMETRICS is performance modeling oriented; steady-state evidence for computer-systems/general software-engineering venues (TOSEM, Empirical Software Engineering, IEEE TSE, MSR) where A\* category findings would get SE attention. Consider whether the paper will be re-named for assessing.

### Part B-B. Publication indexes of the main author
- "Main author" ambiguity: first author Iren Mazloomzadeh (Ph.D. student) — Google Scholar h ≈ 1–2, i10 ≈ 0; PolyPublie ~7 works / 4 citations.
- Senior/corresponding author, Foutse Khomh (Polytechnique Montréal, Full Professor): h-index 65, i10-index 266 (Google Scholar; 16,365 total citations).
- Please clarify which index is demanded; Foutse has substantial scholarly influence.
- Evidence: Polytechnique expert directory · Google Scholar user YYXb3KIAAAAJ.

### Part B-C. Your own informative abstract (100–150 words)
"The paper reports a large-scale longitudinal empirical study comparing agentic pull requests (PRs) from five widely used AI coding agents with human-generated PRs. Based on 220,612 closed PRs from 489 popular Python GitHub repositories (August-2025-era data captured by the AIDev dataset), it (i) analyzes how agentic PR merge rates vary across agents and software-development lifecycle quarters via mixed-effects logistic models; (ii) characterizes the development tasks addressed by agentic PRs via BERTopic topic modeling after LLM summarization; and (iii) compares PR complexity characteristics and bug-inducing commit rates between matched samples of merged agentic and human-generated PRs. The findings show that Claude achieves the highest merge rate, that agentic PRs are predominantly used for structured tasks such as documentation, dependency updates, and tests, that mergeability is relatively stable over time, and that agentic PRs exhibit comparable or lower defect proneness than human contributions mostly with negligible effect sizes."

(148 words)

### Part B-D. Enumerated empirical research methods and assessment of quality of their description
Methods used:
1. Data source reuse (AIDev dataset → filtered Python repos ≥100 stars) + GitHub REST API v3 mining (closed PRs per repo; agent evidence selectors).
2. Filter and repository lifecycle definition: agentic activity span, quarter split, repos with ≥2 agentic PRs for quartering.
3. Agent attribution heuristics (branch prefix / bot / Co-Authored-By).
4. LLM-based PR summarization with gpt-4.1-mini of combined title+body.
5. Text preprocessing (stop removal, HTTPS link removal, special-character removal, lemmatization).
6. BERTopic config with all-mpnet-base-v2 / all-MiniLM-L6-v2 / Gemini-embedding-001; UMAP; K-means; topic count tuned 10–60 by C_v and UMass; CountVectorizer + POS+MMR representation.
7. Manual topic validation using "stratified sampling; two coders; third author tie-breaker; Cohen's κ 0.842; 15 topics merged into 3."
8. Normalization of per-task merge rates with parametric empirical Bayes (Beta-binomial, weighted mean/variance by PR counts).
9. Binomial GLMM with logit link (AI agent and development quarter fixed effects; repository random intercept); emmeans with municipality back-transformation; Tukey-adjusted pairwise comparisons.
10. Two-proportions z-tests for agent-maturity across quarters.
11. Complexity tests: Mann-Whitney U for agentic vs. human PRs (six metrics) + Cliff's δ.
12. χ² + Cramér's V for bug-inducing rates (per quarter and across quarters).
13. Bug-fix commit keyword detection + SZZ (PyDriller) bug-inducing commit identification.
14. Random-sampling balancing of agentic and human PRs by repository/quarter.
15. Conflict-of-interest table states no reviewer conflict.

Quality-of-description verdict:
- **Major steps described well**: data filtering, agent selection, quarter definition, metric definitions, statistical test choices, sample restrictions all have enough detail to replicate.
- **Intermediate results reported**: Tables 1–12, Figure 6–12, cohort counts, topic label tables, code-level statistics.
- **Reasoning for application stated**: Thematic headings with justification; GLMM used for non-normal response; BERTopic for short PRs.
- **Gaps / missing** (needed for reproducing): LLM summarization prompt, full topic-model hyperparameters (UMAP dimensions, seed, K-means initialization settings, BERTopic config dump); bug-fix keyword exact list; SZZ implementation options (regular/AGSZZ) and parameters; random seeds; exact CSVs/code in the replication package (not inspected); how topics must be validated through human consensus; no model diagnostics.

Conclusion of D (one paragraph): The empirical approach is detailed and repeatable if the replication package provides additional scripts, but description leaves out details that affect finding robustness—especially the LLM summarization step and GLMM/SZZ parameter choices. For submission publication, request an appendix/model/diagnostic report snapshot.

### Ethics table
- Conflict of interest: No.
- Plagiarism: No.
- Inappropriate self-citations: No (reviewer noticed ≤ several same-group refs; no material inflation of citation metrics).
- Other ethical concerns: No; but note 2026-dated unfinalized content and preprint-stage public availability references.

## Suggested recommendation text (for front matter)
"Strong-hearted extension of existing agent-impact studies, but major revision needed on causal/robustness evidence (GLMM diagnostics + sensitivity on topic generation / bug NLP) before acceptance. Please increase review notes and re-evaluate indicator vs sample selection." (Rewrite to standard English in final.)

## Suggested corrected abstract (author-facing)
No — keep author's current abstract as basis.
