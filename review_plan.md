# Review Plan — Peer Review Assignment

**Paper:** "How Do AI Coding Agents Contribute to Software Development? An Empirical Study of Agentic Pull Requests"
Mazloomzadeh, Morovati, Khomh — Polytechnique Montréal. arXiv:2607.21832, 43 pages.
**Template:** `docs/review_form_extended.docx` (Part A: MDPI standard form; Part B: course-specific tasks A–D)
**Course material:** `docs/Research_Methods_Reviewing2022shortened_again.pdf`

## Paper snapshot (for orientation)

- RQ1: mergeability of agentic PRs across 5 agents and lifecycle quarters — GLMM, emmeans, Tukey-adjusted pairwise comparisons. Key numbers: Claude 84.3% EMM merge prob, Codex 73.5%, Cursor 63.9%, Copilot 59.6%, Devin 43.0%. Quarter EMMs 63.7–68.2%, none significant.
- RQ2: BERTopic topic modeling (k=36, Gemini-embedding-001) over 9,428 agentic PRs → 24 topic categories; gpt-4.1-mini PR summaries; validation on stratified 100-PR sample, 87% correct, Cohen's κ 0.842; Empirical Bayes (Beta–Binomial) normalization of merge ratios per topic/quarter.
- RQ3: balanced sample 2,275 agentic vs 2,275 human merged PRs; 6 complexity metrics; Mann–Whitney U + Cliff's δ; SZZ (PyDriller) bug-inducing commits; chi-squared + Cramér's V.
- Dataset: AIDev (Li et al.) + GitHub REST API; 489 Python repos ≥100 stars; cutoff 2025-11-20.
- Findings 1–7; Threats section (construct/internal/external); no interactive elements; replication package: github.com/mazloomzadeh/AI-Agent-Analysis.

## Phase 0 — Setup (done)

- [x] Parse review form docx (structure: 6 rated criteria, quality checklist table, English language, recommendation, comments; ethics table; Part B items A–D)
- [x] Extract paper text → `C:\Users\Rajehdidntwakeup\AppData\Local\Temp\paper_pdf.txt`
- [x] Extract course PDF text → `C:\Users\Rajehdidntwakeup\AppData\Local\Temp\course_pdf.txt`

## Phase 1 — Second pass reading + issue log

- [x] 1.1 Re-read abstract, intro, methodology (pp. 1–9); log issues.
- [x] 1.2 Re-read RQ1 results + tables 3–5 (pp. 9–14); check GLMM reporting (CIs absent, Tukey adjustment, p-value formatting "0.00", "0.178" for Claude/Codex with z=2.203 — verify consistency).
- [x] 1.3 Re-read RQ2 results + tables 6 + figs 6–8 (pp. 15–22); check topic validation claims (κ reported as "84.2%" vs "0.842" inconsistency; 15→3 topic merges).
- [x] 1.4 Re-read RQ3 results + tables 7–12 (pp. 22–32); check effect-size sign conventions (e.g., Cursor δ=0.375 called "does not differ significantly" while text elsewhere uses threshold logic).
- [x] 1.5 Re-read related work + threats + conclusion (pp. 33–38); check threat list says "four primary sources" but lists five; check SZZ precision/recall discussion.
- [x] 1.6 Reference spot-check (pp. 38–43): citation years vs claims (e.g., several 2026 arXiv preprints cited as established findings; ref [23] "Claude CodeDevin. 2025" typo; ref [26] author list incomplete).
- [x] 1.7 Deliverable: `review_notes.md` — numbered issue log with page/section references, severity (major/minor/editorial).

## Phase 2 — Part A: MDPI standard form

- [x] 2.1 Rate "Originality / Novelty" (High/Average/Low/No Answer) + one-line justification. Basis: lifecycle-decomposed agent vs human comparison extends AIDev (Li et al.), Watanabe et al., Agarwal et al. — incremental but multi-dimensional.
- [x] 2.2 Rate "Significance of Content" — practical relevance for maintainers/teams adopting coding agents; tempered by negligible effect sizes.
- [x] 2.3 Rate "Quality of Presentation" — mostly clear, but typos ("Finlay", "Result" section title, "agenic", "well-representated", inconsistent κ formatting), some sections verbose.
- [x] 2.4 Rate "Scientific Soundness" — main drivers: SZZ quality (precision 0.39), LLM-summaries feeding BERTopic (input bias, unvalidated summarization), GLMM without reported CIs/likelihood tests, multiple 2026-preprint citations, RQ3 merged-only selection bias.
- [x] 2.5 Rate "Interest to the readers" — timely topic, broad appeal.
- [x] 2.6 Rate "Overall Merit".
- [x] 2.7 Table 1 (quality checklist, 5 rows × Yes/Can be improved/Must be improved): intro/background+refs; research design; methods description; results presentation; conclusions supported by results.
- [x] 2.8 English language & style — select option (likely "fine/minor spell check required"), note repeated editorial slips.
- [x] 2.9 Ethics table (4 rows × Yes/No): COI (course reviewers — declare "No"); plagiarism (not detected); inappropriate self-citations (note high share of refs [1,30,57,59,80,81,82,92→related group] from Polytechnique Montréal group — check and characterize); other ethical concerns.
- [x] 2.10 Overall Recommendation — draft with solid motivation; likely "Reconsider after major revision" or "Accept after minor revision" depending on weights decided in 1.7. Decide after issue log review.

## Phase 3 — Comments section (≈½ A4 page)

- [x] 3.1 Neutral summary (4–6 lines): dataset, 3 RQs, headline findings.
- [x] 3.2 Strong points (3–5 bullets): scale (220,612 PRs / 489 repos), lifecycle quarterization enabling cross-repo comparison, triangulated RQ structure, topic-model validation with κ, threats section present, replication package.
- [x] 3.3 Points to improve (5–8 bullets): validate LLM summarization; report CIs + model diagnostics for GLMM; SZZ limitations quantified; selection bias in merged-only RQ3; effect-size sign/threshold consistency; multiple-testing correction beyond GLMM pairwise; editorial consistency.
- [x] 3.4 Specific details (line/section/table references for each point).
- [x] 3.5 Reviewer's own informative abstract (100–150 words) — Part B item C overlap: draft once, reuse.

## Phase 4 — Part B tasks

- [x] 4.1 (A) Venue: identify actual venue from paper metadata ("Proc. ACM Meas. Anal. Comput. Syst." = POMACS/SIGMETRICS — verify; SE content suggests possible template error). Then:
  - [x] 4.1a Check CORE journal rank (http://portal.core.edu.au/jnl-ranks/)
  - [x] 4.1b Find published acceptance rate for that venue (ACM site / recent PC chair reports / taoxie.cs.illinois.edu/seconferences.htm for conference analogues)
  - [x] 4.1c Classify per lecture scale: ≥50% not selective; 30–50% reasonably selective; 15–30% selective; <15% too selective.
  - [x] 4.1d Record evidence with URLs + dates.
- [x] 4.2 (B) Author publication indexes via Google Scholar:
  - [x] 4.2a First-author (Iren Mazloomzadeh) h-index + i10.
  - [x] 4.2b Senior author (Foutse Khomh) h-index + i10 (context: "main author" ambiguous — record both, label clearly).
  - [x] 4.2c Record URLs + retrieval date; note caveat from course slides (#citations ≠ impact).
- [x] 4.3 (C) Informative abstract 100–150 words (from 3.5).
- [x] 4.4 (D) Empirical methods enumeration + description-quality assessment:
  - [x] 4.4a List each method: dataset reuse + GitHub REST API mining; keyword-based bug-fix detection; SZZ via PyDriller; BERTopic pipeline (embeddings, UMAP, K-means, CountVectorizer, POS+MMR); LLM (gpt-4.1-mini) PR summarization; GLMM (binomial, logit, repo random intercept); emmeans + Tukey; two-proportions z-test; stratified sampling + Cohen's κ; Empirical Bayes Beta–Binomial; Mann–Whitney U + Cliff's δ; chi-squared + Cramér's V.
  - [x] 4.4b Assess description quality per method: major steps present? intermediate results reported? reasoning for application stated? (Methods §3.2–3.3 are described well; missing: summarization prompts/validation, GLMM diagnostics/CIs, random-effects variance, SZZ parameters, EB hyperparameters.)
  - [x] 4.4c Verdict paragraph + concrete missing-item list.

## Phase 5 — Assemble deliverable

- [x] 5.1 Write completed review into a copy of the template: `docs/review_filled.docx` (fill checkboxes as "(x)", insert text under each section; keep original layout).
- [x] 5.2 Cross-check all template sections have answers:
  - [x] 6 rated criteria
  - [x] Table 1 checklist (5 rows)
  - [x] English language
  - [x] Overall recommendation + motivation
  - [x] Comments (≈½ page): summary, strong points, points to improve, details
  - [x] Ethics table (4 rows)
  - [x] Part B: A venue + evidence, B author indices + evidence, C abstract, D methods + assessment
- [x] 5.3 Sanity pass: tone constructive (identify the champion), no identity assumptions, evidence links live, word count of abstract in 100–150.
- [x] 5.4 Produce summary for submission/hand-in.

## Working assumptions (flag if wrong)

1. "Main author" = first author; senior author included as context.
2. Venue read from paper metadata (POMACS), possibly a template leftover — verify against any submission info.
3. Fill-in happens in a copied docx; original template untouched.
