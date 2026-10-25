# Abstract and Introduction

The reader should understand what was missing, what the paper provides, how it
is used, and what the evidence establishes. These are reading outcomes, not a
fixed sentence sequence or paragraph count.

## Abstract

Explain the concrete research need, the contribution that addresses it, and the
result of using it. Preserve enough distinctive content to identify this paper;
do not reduce it to generic claims of a useful framework.

For benchmarks, explain what supervision, organization, or evaluation capability
the resource provides and how the experiments use it. Introduce a reference model
through the task it instantiates, not an abrupt inventory of architectures,
training variants, auxiliary signals, and diagnostics. For methods, explain the
central design at the level needed to understand its benefit. For analyses, make
the question and finding central rather than forcing a proposed model.

Keep verified headline numbers when they substantiate the main point. Select them
for meaning rather than a quota; preserve metric and comparison scope. The final
sentence may state a measured result or a supported implication. It need not end
with a leaderboard, competitor concession, or an additional diagnostic. Do not
use the final sentence to append a secondary cost already explicit in a complete
table. If a condition changes the interpretation of the abstract's claim, state
it directly at the relevant point.

Check the venue's actual abstract limit when compliance is in scope. A customary
length or example is not a venue requirement. Do not squeeze a disconnected topic
into a semicolon merely to retain every piece of work.

When rewriting for focus, preserving the paper's facts does not require preserving
every fact in the Abstract. Move a peripheral construction recipe or control study
out if it answers no question prepared by the main argument. Calling it "supporting"
does not fix the topic jump. Attribute reused data concisely and positively (for
example, "extends an existing image archive with...") rather than adding a denial
of work the paper never claims to have done.

When a resource supports several tasks, keep each result attached to the model or
adaptation that produced it. A colon after introducing one reference model should
not silently make that model the subject of results from another task.

## Introduction

Choose paragraph roles from the argument, not a template:

- Ground the need in a concrete task or setting.
- Explain the relevant gap without asserting that an entire field lacks resources.
- Show why filling the gap takes specific work and why that work matters to users.
- Introduce the contribution as a response to that need.
- Explain how its use is evaluated and what the results establish.

Combine or expand these roles as needed. Construction details belong here only
when they explain value or difficulty; procedural inventories belong later.
Do not force one paragraph per module or a coined term for every challenge.

For each transition, ask what unresolved question in the previous passage the next
passage answers. A data description can lead to its supported learning task, then
to a reference implementation and evaluation. A new control analysis with no
prepared question is a topic jump even if it shares the dataset.

Avoid circular necessity: training a reference is a way to investigate learning
from a resource, not a logical prerequisite for calling the resource a benchmark.
Distinguish a design motivation from proof that every alternative must fail.

Contribution statements should identify substantive work and its evidence, not
paper sections or training stages. A construction and validation process may be
a contribution when it is substantive; a dataset need not be relegated to an
extra bullet after a model. Choose the number of contributions from the actual
work, and distinguish an artifact contribution from a measured benefit.

## Continuity check

Read the Abstract and Introduction without the rest of the paper. Can a reader
explain the gap, contribution, use, and evidence without translating a list of
internal names? Then check the answers against the actual methods and results.
Do not trade accuracy for narrative smoothness, or narrative smoothness for an
exhaustive list of true but secondary facts.
