# Review Issue Log

Paper: "How Do AI Coding Agents Contribute to Software Development? An Empirical Study of Agentic Pull Requests"
Reviewer: (course reviewer, single-blind)
Severity: M = major, m = minor, e = editorial.

## M — methodology / construct validity

- M1 (Major) — Bug-inducing quality: SZZ (PyDriller) precision reported as 0.39, recall 0.67 [Threats, p.36]. No developer-validated ground truth on own dataset; bug-fix detection via keyword regex ("bug, fail, crash, fix, ...") can mis-tag. Findings on defect proneness rest on noisy proxy. Suggest manual validation on sample, or report sensitivity to keyword list.
- M2 (Major) — Selection bias in RQ3: only merged agentic/human PRs compared (§4.3 opening). Conclusions "defect proneness" and complexity apply to accepted code, not all contributions; rejected PRs may differ systematically. Add sensitivity analysis.
- M3 (Major) — LLM mediation in RQ2: gpt-4.1-mini summaries feed BERTopic (§3.3.1). Summarization quality is unvalidated; summarization is a generative step that can blur topic boundaries. Report prompt, validation inter-rater, or rerun on raw title+body (instead of summaries) to test robustness.
- M4 (Major) — GLMM reporting incomplete (§4.1): only EMMs and Tukey p-values; no random-effects variance (σ²_repo) despite formula, no model CIs, no goodness-of-fit (R²/AIC), no nesting of agent within repo despite telemetry, no sensitivity to quarter encoding. Limits trust in "no temporal effect" claim.
- M5 (Major) — Multiple testing: pairwise comparisons use Tukey adjustment only within GLMM factors, but across RQs (topic-level Empirical Bayes normalized ratios + quartile graphs) p-values reported without family-wise correction? Check Figure 8 + section 4.2.2 conclusions.
- M6 (Major) — "Lifecycle" operationalization: quarters defined as equal slices of agentic activity span per agent–repo pair (§3.2), and only repos with ≥2 agentic PRs retained (Table 2, n=309). RQ1/Q definitions inconsistent: Table 1 n=489 for RQ1 counts, Table 2 for quarterly decomposition. Could confound findings.
- M7 (Major) — `lifecycle` ≠ project maturity; agent adoption itself defines period boundaries. Alternative maturity definitions could change findings (authors acknowledge [Threats, p.36], but no sensitivity shown).

## M — statistical details

- M8 (Major) — Agent-maturity test (§4.1, Fig. 5): two-proportions z-test on aggregated quarterly merge rates assumes independent observations and ignores repository clustering and prior GLMM structure; should use logistic/mixed models. Reported p="0.00" (not meaningful) e.g. Codex 2nd vs 3rd.
- M9 (Minor/Major) — Cohen's κ inconsistency: §4.2 "84.2% Cohen's kappa" vs elsewhere κ=0.842 [Threats, p.37]. Are they mixing κ and raw agreement? Clarify.
- M10 (Minor) — Effect-size sign conventions: Table 7/8 use Cliff's δ with direction sometimes unclear (e.g. Cursor "δ=0.375" labeled "does not differ significantly" for changed LOC despite p=0.375 — not significant; fine; but Cursor vs others "matching vs non-matching" direction not explicitly stated).
- M11 (Minor) — Table 5: "Cursor / Copilot OR 0.833, z=-0.726, p=0.951" reported as "Cursor higher than Copilot" yet OR<1 and z-negative. Verify direction-of-effect statement.
- M12 (Minor) — Topical interpretation from 87% validation on 100 PR stratified sample is admissible; but merging 15 topics into 3 without reporting resulting inter-rater agreement needs explicit statement.

## m — reproducibility / evidence

- m1 — Replication package URL given (ref [73], github.com/mazloomzadeh/AI-Agent-Analysis) but no check for open data; claim available. Cannot verify since 2026-dated publication; verify access.
- m2 — Hyperparameters present for topic modeling (k range 10–60, k=36, UMass vs C_v, Gemini-embedding-001, POS ratio) but random seeds, LLM summarization prompt/task output, UMAP/Kmeans settings ("config omitted, see replication package") — require release.
- m3 — Data cut-off 2025-11-20 and "20 November 2025" in future relative to 2026 publication: OK, preprint dated 23 Jul 2026.
- m4 — LLM agent detection heuristics: Claude Code requires "Co-Authored-By: Claude" in body; Copilot/Cursor require branch prefix `head:copilot/` / `head:cursor/`. May miss some agent-authored PRs and mislabel integration/branch protection artifacts by human users with similar branch names.

## e — editorial / presentation

- e1 — Intro: "Finlay, Section 6" (line ~104, p.3) — typo "Finally".
- e2 — Section heading "Result" (singular) + "Section 4.1" then "4.2.1", "4.3.1" etc inconsistent.
- e3 — "agenic" PR (p.24, conclusion 1 example) — typo for "agentic"; "well-represented" etc.
- e4 — κ notation confusion (see M9).
- e5 — Results overreport: e.g. θ values in BERTopic formulas rendered as "?" (encoding/font) due to PDF extraction; tables fine.
- e6 — "Effort size" labels repeated inconsistently; "negligible" used very often, diluting contrast.
- e7 — Table 5 header "p.value" etc lack confidence intervals for odds ratios.
- e8 — Abstract: "agentic PRs show comparable or lower defect proneness than human PRs, with mostly non-significant differences" juxtaposed with RQ3 defects analysis: heterogeneity (Claude modifies more LOC / fewer changed LOC for Copilot etc.) — condensation loses nuance.
- e9 — Ref handling: ref [23] "Claude CodeDevin. 2025" — likely merged/confused; ref [3] venue formatting inconsistent ("IEEE Transactions on Software Engineering" not consistent).

## Venue evidence tasks (Part B-A)

- Paper metadata target: "Proc. ACM Meas. Anal. Comput. Syst. 37, 4, Article 111 (July 2026)" = ACM Proceedings on Measurement and Analysis of Computing Systems (POMACS, associated with SIGMETRICS). Real published issues may reject. Cross-check CORE journal rank (portal.core.edu.au/jnl-ranks/) and ACM acceptance ratio.
- Note: content is empirical SE (mining software repositories, PRs) — target venue mismatch likely; this is an arXiv preprint that may be re-targeting TOSEM/EMSE/IEEE TSE/MSR. Cover both: report actual listed venue, plus "if targeting traditional SE venue" alternatives.

## Prior data already validated (do not re-flag)

- Agent merge probabilities (Table 3): Claude 84.3, Codex 73.5, Cursor 63.9, Copilot 59.6, Devin 43.0.
- Quarter merge probabilities (Table 4): Q1 65.4, Q2 63.7, Q3 68.2, Q4 67.7; no significance.
- Topics: 24, max Cohen's κ pre-merge? 0.842 two-author.
- Bugs: Q4 significant but negligible effect size; agents vs human bug-inducing difference not significant other quarters.
