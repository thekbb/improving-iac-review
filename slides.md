---
title: "Improving IaC Reviews: Better Signal, Less Noise in Pull Requests"
duration: 20min
class: title-slide
---

<style>
.title-slide {
  text-align: center;
}
/* Increase text size for all slides */
html, body {
  font-size: 130%;
}
.slidev-layout {
  font-size: 1.2em;
}
.slidev-layout.compact {
  font-size: 0.9em;
}
/* Ensure model slide text isn't dimmed */
.slidev-layout.model p {
  opacity: 1;
}
/* Increase gap between title and body for specific slides */
.slidev-layout.gap h1 + p {
  margin-top: 1.1em;
}
/* Small vertical spacing utility */
.gap-sm {
  height: 0.35em;
}
/* Subtext styling for Three Realities slide */
.slidev-layout.model .reality-sub {
  font-size: 0.85em;
  color: #9aa3ab;
  margin-left: 0.6em;
  margin-top: -0.8em;
}
/* Styled quote for emphasis */
.slidev-page .slidev-layout .quote {
  margin: 0.9em 0 1.1em 0;
  padding: 0.9em 1.2em;
  border-left: 6px solid #6ad3ff;
  background: rgba(255, 255, 255, 0.06);
  border-radius: 10px;
  font-style: italic;
  font-weight: 600;
  font-size: 1.2em;
  text-align: left;
  color: #e8eef2;
  text-shadow: 0 1px 6px rgba(0, 0, 0, 0.35);
}
.slidev-page .slidev-layout .quote-text {
  line-height: 1.6;
  margin-bottom: 0.5em;
}
.slidev-page .slidev-layout .quote-cite {
  font-style: normal;
  font-size: 0.9em;
  opacity: 0.85;
  padding-left: 0.6em;
}
blockquote p {
  margin: 0.2em 0;
}
blockquote strong {
  font-style: normal;
  font-weight: 600;
}
blockquote cite {
  display: block;
  margin-top: 0.4em;
  font-size: 0.85em;
  opacity: 0.85;
}
/* Presenter notes only */
.grid-section.note .prose {
  font-size: 80% !important;
}
</style>

# Improving IaC Reviews

## Better Signal, Less Noise in Pull Requests

<!--
Quick story about a PR I approved that fixed an OpenSearch cluster by deleting and recreating it,
losing a few tens of millions of records.

I tried hard. I messed up.

Transition: "I think of that often, and reviewing Terraform still scares me."
-->

---

# Terraform Reviews Require Predicting the Future

<div class="quote">
<div class="quote-text">"It's tough to make predictions, especially about the future."</div>
<div class="quote-cite">— Yogi Berra</div>
</div>

<!--
Systems grow.
Diffs grow.
Confidence drops.

Terraform reviews are about impact, not syntax.

Transition: "So let's name the mental model."
-->

---
class: model gap
---

# Three Realities at Once

Intent
<div class="reality-sub">(HCL diff)</div>

<div class="gap-sm"></div>

State
<div class="reality-sub">(terraform.tfstate)</div>

<div class="gap-sm"></div>

Reality
<div class="reality-sub">(AWS)</div>

<!--
Three realities.
One reviewer.
This is the job.

“HCL tells us what we want.”
“State tells us what Terraform thinks exists.”
“Reality is what AWS is actually doing.”

Transition: "HCL gives us intent, but intent is not impact."
-->

---
class: gap
---

# HCL Shows Intent

But intent ≠ impact

<!--
HCL says what we want.
It does not show what will happen.

Transition: "We need a projection."
-->

---
class: gap
---

# Terraform Plan = Projection

Projection connects intent to expected impact.

<!--
The plan is the projection.
It connects intent to impact.

Transition: "Now notice where we hide it."
-->

---
class: gap
---

# We Hide the Projection

The plan exists, but it is not in the PR.

<!--
Buried in CI logs.
Or stuck on a laptop.
So reviews become guesswork.

Transition: "Fix the system, not the humans."
-->

---
class: gap
---

# Fix the System, Not the People

- Better inputs, better reviews
- Surface impact at decision time

<!--
We do not need superhero reviewers.
We need better instruments.

Transition: "Here are two examples of the pattern."
-->

---
class: compact
---

# Review Aids

Pattern: surface impact at decision time

## [Terraform Plan Commenter](https://github.com/marketplace/actions/terraform-plan-commenter)

- Summary in the PR
- Full plan linked

## [AWS IAM `*` expander](https://github.com/marketplace/actions/expand-aws-iam-wildcards)

- Expand `*` inline
- Link to AWS docs

<!--
Two examples.
Same pattern.
Impact in context.

Transition: "Let me show you one PR where both happen."
-->

---
class: gap
---

# Live PR Example

- Wildcard expansion turns `*` into meaningful info
- Terraform plan shows up in the PR

A completly real and totally not contrived example:

[`thekbb/shit-bruce-says#17`](https://github.com/thekbb/shit-bruce-says/pull/17)

<!--
No hunting in CI logs.
Impact is visible at decision time.

Transition: "When signal improves, review behavior changes."
-->

---
class: gap
---

# What Changes When Signal Improves

- Less "LGTM I guess"
- Faster reviews
- More confident merges

<!--
Fewer surprises.
Fewer risky approvals.

Transition: "So the close is simple."
-->

---
class: gap
---

# Close

I approved a Terraform change.
It deleted millions of records.

Terraform did exactly what the code said.
I do not want better reviewers.
I want better instruments.

Questions?

<!--
Bring it back to the story.
The system sets us up to fail.
Fix the system.
-->
