# Method and Technical Exposition

Start with the problem's inputs, outputs, and assumptions. Keep a task definition
separate from the paper's particular implementation unless the section explicitly
defines that implementation. A benchmark's reference model need not be presented
as a new architectural paradigm.

Explain the design choices that matter to the claim and how information flows
through them. Motivation should describe the constraint or intended benefit, not
assert without evidence that this is the only viable design. Avoid inventing a
causal mechanism merely because an aggregate score improved.

Use equations when they specify a meaningful quantity, operation, or constraint.
Define symbols, coordinate frames, time horizons, tensor roles, and units where
needed. Do not turn a standard operation into several named modules to increase
apparent novelty, or force each component into the same paragraph template.

Distinguish:

- annotations available during training from inputs available at inference;
- auxiliary supervision from the independently evaluated prediction targets;
- generated explanations from an established causal account of model decisions;
- initialization or pretraining from task adaptation and test-time prompting;
- implementation choices from evaluation interventions.

Describe training and inference separately when their paths differ. State actual
frozen/trainable components, objectives, and output interfaces consistently with
the implementation records. A training description may be a paragraph, subsection,
or appendix reference depending on its role; neither its location nor paragraph
count is universal.

Keep enough detail in the main text to understand the claimed mechanism. Put
long configurations and implementation recipes in the supplement with a clear
pointer. Pseudocode and framework diagrams are useful when they clarify otherwise
ambiguous dependencies, not mandatory decorations.
