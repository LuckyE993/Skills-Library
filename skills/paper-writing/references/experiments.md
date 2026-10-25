# Experiments, Tables, and Result Captions

Organize experiments around the questions that support the paper, not the order
in which jobs ran. Distinguish capability comparison, component attribution, and
supporting diagnostics; use the ordering that matches the paper's contribution.

## Read the comparison before interpreting it

Identify what rows share and what changes: data, supervision, initialization,
output format, model, budget, checkpoint selection, or test-time inputs. A result
may show the complete approach is useful without isolating any one changed factor.
Do not attribute a gain to a rationale, head, or annotation category unless the
corresponding controlled comparison supports that attribution.

Keep method names recognizable. State material comparison differences clearly in
the setup, caption, footnote, or accompanying prose, with supplementary details
as appropriate. A fact essential to interpreting the headline cannot be hidden
only in the supplement. Do not append implementation history to every baseline row.

## Explain metrics and results

Define unfamiliar metrics before drawing conclusions: quantity, aggregation
population, unit, direction, and reference for any delta. Check denominators,
eligibility rules, averaging, precision, and the distinction between percentage
points and relative percentage change. A response diagnostic need not be an
accuracy metric or have a "higher is better" direction.

Let the scientific question determine the primary and secondary metrics. Report
a supported main finding without automatically adding another method's advantage
on a secondary measure. Preserve the table and any qualification needed to avoid
implying overall dominance. "Lowest final error" and "best planner" are different
claims. Neither blanket caveat removal nor caveat stacking improves honesty.

If the user asks to remove a secondary-metric concession and the retained claim is
already metric-specific, remove that digression rather than merely moving it to
the next sentence. This does not permit hiding a changed input budget or other
material condition. Attach the necessary condition to the comparison concisely;
do not append every unknown about every configuration.

### Let tables carry secondary tradeoffs

- When a table clearly reports a secondary metric with its unit, direction or
  interpretation, comparison scope, and necessary conditions, let the table carry
  that comparison. Use the surrounding prose for the primary finding and why it
  matters.
- Do not turn a table-visible tradeoff into a final “but/however/although” clause
  after a positive result. A neutral pointer such as “Table X also reports memory
  and latency” is sufficient when navigation helps.
- Keep a secondary result in prose when it changes fairness, applicability, or the
  meaning of the central claim, or when a reviewer explicitly asks about it. State
  the measured fact and its impact directly once; do not omit it to improve tone.
- Example: replace “The method is more accurate, but uses more memory” with
  “The method improves accuracy under the evaluated setting (Table X).” If the
  memory requirement limits the claimed deployment setting, state that boundary
  in the setup or limitations discussion.

Separate measured observations from plausible explanations and causal conclusions.
A paragraph may simply state what the comparison shows; it need not manufacture
a cause for every gain or repeat what the experiment does not prove. If uncertainty
changes the claim, state it directly once where it matters.

After replacing an overbroad claim with a supported one, do not automatically add
sentences negating each deleted claim. For example, a scoped statement about reduced
bytes at measured accuracy need not then disclaim losslessness, universal compute
efficiency, and superiority to all methods. Explain the removed overclaims to the
author separately if useful. Keep qualifications required by the retained claim.

Before retaining a caveat in replacement prose, ask which surviving claim it
qualifies. If it only refutes the discarded claim, put that explanation in the
author-facing note instead. For example, once a result is explicitly attributed
to a combined configuration rather than a particular loss, the result sentence
need not repeat why the removed loss-specific attribution was unsupported. Keep
the changed factors clear in the comparison setup where they matter.

Additional seeds, intervals, ablations, or generalization tests depend on the claim,
venue, and authorized experiment contract. Do not require or forbid them globally.
A writing task can flag missing evidence or narrow a claim; it does not authorize
running new experiments. Reuse completed, applicable evidence.

## Tables and captions as one unit

Read values from the accepted source artifact when a numeric update is requested.
Do not introduce display overrides or change results to fit the prose. If two
sources disagree, identify the conflict before treating either as authoritative.

Check cells, headers, caption, and interpretation together: metric names, units,
sample counts, row groups, reference conditions, delta signs, best-value marking,
and color meanings must agree. Use concise labels with definitions where needed;
do not replace them with long internal run descriptions.

For unfinished work, preserve the project's explicit distinction between pending
and inapplicable values. Placeholders support no result claim. Submission readiness
requires resolving pending entries, not disguising them as missing-at-random data.

Captions should explain how to read the display and the necessary comparison, with
the main observation when useful. They need not repeat the entire result paragraph
or list every possible caveat. Cross-reference by stable LaTeX labels rather than
assuming a figure number remains unchanged after reordering.
