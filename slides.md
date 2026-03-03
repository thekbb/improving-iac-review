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

Transition: "That was the moment I realized the system was setting reviewers up to fail."
-->

---

# Why Terraform PRs Feel Bad

- Infra keeps getting bigger and more complex
- Reviewers must predict impact and risk
- Lots of "LGTM I guess"

<!--
"Bigger systems mean bigger diffs, and bigger diffs make confidence go down fast."
Context is everything.

Most reviews rely on things in other repos, modules, or external systems.

Transition: "So we need to talk about what the code can and cannot tell us."
-->

---

# HCL Is Good at Intent, Bad at Impact

- Declares what infra should be
- Logic and modules can hide meaning
- The diff is hard to parse mentally

<!--
Contrast intent vs impact.

Line: "HCL is great at saying what we want, not great at showing what will happen."

Line: "Who would take the bet that they can describe what will happen at AWS while looking at TF
that is an instance of an external module, which includes another external module and has a count?"

Transition: "That is why the plan is not optional. But we hide it."
-->

---

# The Plan Is Usually Missing

- Buried in CI logs, several clicks away,  in uncolored plain text
- Only works on a laptop (which is a whole other problem)
- Or cannot run locally, or see in CI...  So you YOLO

<!--
Line: "The plan is always somewhere. Make it visible at the right time."

Line: "Reviewing Terraform without the plan is driving without headlights at night."

Transition: "And even with a plan, reviewers are still juggling multiple realities."
-->

---

# Three Realities at Once

- HCL diff is intent
- Terraform state is last known assumptions
- Live infra is actual reality

<!--
Introduce the mental load.

Line: "Reviewers are juggling intent, state, and reality at the same time."

"This is a ton to think on."

"They also have their own work"

Line: "This is how you delete all the data in OpenSearch."

Transition: "When the projection is missing, signal collapses."
-->

---

# Why Signal Is So Low

- Terraform plan connects intent to impact
- It _always_ exists but is all too often not visible in PRs
- Hidden blast radius drives guesswork
- So we need key info, like the plan, _**in**_ the PR

<!--
Line: "The plan is the projection. We just hide it from the people making the decision."

Line: "The tooling is improvable. We can fix it."

Transition: "And no, the answer is not 'train reviewers harder.'"
-->

---

# Peer Review Remains the Gold Standard

- Best place for learning and shared context
- Best place to prevent badness
- Still true when AI generates the HCL (If not more so)

<!--
- AI speeds creation, not accountability.
- Machine generated HCL makes intent thinner.
- Machines can catch patterns, humans bring context.

Line: "Even if AI writes the HCL, humans still own the consequences. That is why review matters more."

Transition: "So the fix is system-level, not person-level."
-->

---

# Fix the Tooling/System, Not the People

- Better inputs, better reviews
- Automation beats memory
- Pattern: surface impact at the decision point

<!--
Line: "We do not need superhero reviewers. We need better instruments."

Line: "I'm going to show some example tooling that helps me. The pattern is surfacing impact at the decision point."

Transition: "Here are two concrete review aids."
-->

---
class: compact
---

# Review Aids

Two examples of a bigger pattern

## [Terraform Plan Commenter](https://github.com/marketplace/actions/terraform-plan-commenter)

- Run plan in CI
- Post a clear summary in the PR

## [AWS IAM `*` expander](https://github.com/marketplace/actions/expand-aws-iam-wildcards)

- Expand `*` in an inline comment
- Links to AWS documentation

<!--
Walk the audience through what "good" looks like.
* Summary first
* Updates the same content on subsequent runs
* link to real plan in action log if > comment size
* expands the `*`
* link to aws

Line: "These are two examples. The real pattern is: put impact in context for reviewers."

Transition: "Let me show you one PR where both happen."
-->

---

# Live PR Example

- Wildcard expansion turns `*` into meaningful info
- Terraform plan shows up in the PR

A real and totally not contrived example:

[`thekbb/shit-bruce-says#17`](https://github.com/thekbb/shit-bruce-says/pull/17)

<!--
Line: "This PR shows both the plan comment and the IAM wildcard expansion in one place."

Line: "I don't have to hunt and find - or skip the research"

Line: "The goal is not this PR. The goal is impact in every review."

Transition: "When signal improves, review behavior changes."
-->

---

# What Changes When Signal Improves

- Faster reviews
- Fewer risky approvals
- More confident merges
- Fewer pages (hopefully)

<!--
Line: "Faster reviews, fewer surprises, and a lot less 'wait, what did we just approve?'"

Transition: "So the close is simple."
-->

---

# Close

- Reviewers are us
- We deserve better signals at decision time
- Questions?

<!--
Line: "Reviewers are us. We need better signals to make the hard calls. AI can draft the change.
We still sign for the blast radius."

Line: "Raise your hand if your boss would accept you blaming Claude?"
-->
