# Benchmark and Dataset Exposition

Distinguish source material from the new contribution. Existing recordings,
annotations, synchronization, or object associations remain upstream work unless
this paper actually introduces them. Explain what is newly annotated, transformed,
linked, validated, or made evaluable.

## Connect construction to use

Identify the tasks and what each needs as input, supervision, and evaluation
target. Explain how those records correspond to the same sample, object, event,
or time when that correspondence matters. Then describe the construction that
makes the task possible and the checks that support the resulting data quality.

For example, object references may make an object-related answer's evidence
explicit. That does not imply every question refers to an object, or that answers
without identifiers are impossible to verify. Distinguish an annotation field
from what a model must produce and what the evaluator actually scores.

Tie a difficulty to its handling: ambiguous cross-view identity to the actual
association or checking procedure, temporal target alignment to the actual
motion-record conversion. Do not invent new synchronization or alignment
algorithms when the source dataset supplies those links.

Model-assisted labels, rule-computed targets, and human checks are different
sources of evidence. Describe their actual roles and available validation. Do not
call generated labels human-verified or ground truth without supporting records.
Name a generating model when necessary to understand the construction; put exact
prompts, versions, and extended examples in accessible supplementary details.

## Demonstrate utility without changing the subject

Link each important data product to its use: evaluation, task adaptation, reference
training, or analysis. A competitive reference can demonstrate usability without
becoming the paper's main novelty. Separate success on different tasks unless the
experiments directly establish a relationship between them.

Keep auxiliary labels, trained outputs, and evaluation controls distinct. A control
can be central to a benchmark when controlled evaluation is its actual contribution;
otherwise it supports interpretation after the main capability comparisons.

## Scope the gap

Check whether a statement concerns a particular source resource, task, setting, or
combination of capabilities. Replacing "no datasets provide" with "datasets do not
provide" does not fix an unsupported field-wide claim. A resource can contribute
a useful combination without claiming that none of its ingredients existed.

Explain splits, sample eligibility, leakage prevention, target conventions, and
annotation checks sufficiently to interpret results. Keep major validity conditions
in view; route longer templates and construction details to the supplement.
