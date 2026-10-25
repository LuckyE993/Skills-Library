# Whole-Manuscript Consistency

Use this pass when requested or when a central change affects multiple sections.
For local edits, inspect only the relevant connections. Do not make a complete
manuscript audit a prerequisite for fixing a sentence.

## Follow the argument across artifacts

Read the current manuscript, its included tables and captions, and the relevant
supplement. Reuse existing evidence summaries. Inspect underlying records where
needed to resolve a claim, not by default rerunning models or rebuilding datasets.

Trace the title, Abstract, Introduction, contributions, methods, experiments, and
Conclusion. Do they identify the same main work? Does each principal claim have
support in a result, construction record, formal argument, or verified citation?
Do not force every contribution into a performance table. Check that auxiliary
supervision and supporting analyses have not become untested central claims.

## Check meanings, not just strings

- Task names, annotation fields, losses, predicted outputs, and scored quantities
  must remain distinct. A shared backbone does not make their capabilities identical.
- A common noun such as "language" may correctly name an architecture while being
  too vague for a specific evaluated task. Replace by meaning, not global search.
- Symbols, coordinate frames, horizons, metric directions, aggregation sets, units,
  and delta references must agree where they describe the same quantity.
- Source annotations, prompt-visible identifiers, normalized evaluation labels,
  and output examples can use different representations. Explain the mapping
  instead of falsely calling them identical.
- Check both a representation's definition and its use. A caption calling raw,
  view-coded identifiers "view-neutral" is wrong even if later normalization is
  correct. A raw identifier in a quoted prompt raises a separate provenance question;
  do not rewrite the quote or assume which prompt version produced it.
- Training-only signals must not appear as test-time inputs elsewhere. Output
  capabilities must not be confused with evidence that those outputs are faithful.

Preserve original citation titles, actual prompts, and genuine model outputs.
Search can find candidates, but broad replacement cannot decide their meaning.

## Check displays and supporting text

Compare each affected table or figure with its caption, first discussion, later
interpretations, and supplementary breakdown. Inspect numbers and sample counts,
panel labels, row names, highlights, legends, units, and stated control meanings.
Figure numbering and placement may change; update references by label.

Find obsolete versions, contradictory duplicate values, internal stage labels,
pending claims, and unexplained aliases. Preserve accepted results and unrelated
artifacts. If source evidence conflicts, report it instead of silently choosing the
version that best supports the narrative. Do not turn a pending entry into a zero
or confuse an inapplicable metric with an unrun experiment.

## Validate and finish

When revising a LaTeX manuscript, compile using its existing build workflow when
available. Check undefined citations/references and overfull warnings. Render the
affected pages to inspect clipping, overlap, color overflow, text in boxes, and
figure placement near its discussion; a clean log is not visual validation.

For page compliance, identify the main-text/reference/supplement boundary using the
actual venue and project rules, not the PDF's total page count alone. Do not shrink
fonts, alter margins, or add filler to satisfy a page target. Preserve figures and
tables unless their removal is authorized or the requested correction requires it.
If the constraints cannot be satisfied by scoped edits, explain the concrete conflict.

Report material issues with locations, evidence, and a recommended correction.
Separate what was fixed, what remains uncertain, and what was not checked. Do not
claim compilation, visual inspection, citation verification, or submission readiness
without doing the corresponding work. Once the requested checks pass, stop rather
than inventing further rounds of stylistic revision.
