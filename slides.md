---
title: "Improving IaC Reviews: Better Signal, Less Noise in Pull Requests"
duration: 20min
---

# Improving IaC Reviews

## Better Signal, Less Noise in Pull Requests

<!--
Open with a quick story about a Pull Request I approved that fixed an OpenSearch cluster by deleting and recreating it,
losing a few tens of millions of records.
-->

---

# Why Terraform PRs Feel Bad

- Infra keeps getting bigger and more complex
- Reviewers must predict impact and risk
- Lots of "LGTM I guess"

<!--
Set the emotional context. Keep it light.
Line: "Bigger systems mean bigger diffs, and bigger diffs make confidence go down fast."
-->

---

# HCL Is Good at Intent, Bad at Impact

- Declares what infra should be
- Logic and modules hide meaning
- The diff is hard to parse

<!--
Contrast intent vs impact. Line: "HCL is great at saying what we want, not great at showing what will happen."
-->

---

# The Plan Is Usually Missing

- Buried in CI logs, several clicks away in plain text
- Only works on a laptop (which is a whole other problem)
- Or cannot run locally, so you YOLO

<!--
Three disappearances. Line: "The plan is always somewhere. Make it visible at the right time."
-->

---

# Three Realities at Once

- HCL diff is intent
- Terraform state is last known assumptions
- Live infra is actual reality

<!--
Introduce the mental load. Line: "Reviewers are juggling intent, state, and reality at the same time."
-->

---

# Why Signal Is So Low

- Terraform plan connects intent to impact
- It _always_ exists but is all too often not visible in PRs
- Hidden blast radius drives guesswork

<!--
Key insight. Line: "The plan is the projection. We just hide it from the people making the decision."
-->

---

# Peer Review Still Wins

- Best place for learning and shared context
- Best place to prevent badness
- Still true when AI generates the HCL

<!--
Keep this slide short and grounded. Hit these beats:
- AI speeds creation, not accountability.
- Machine generated HCL makes intent thinner.
- Machines can catch patterns, humans bring context.
Line: "Even if AI writes the HCL, humans still own the consequences. That is why review matters more."
-->

---

# Fix the System, Not the People

- Better inputs, better reviews
- Automation beats memory
- Pattern: surface impact at the decision point

<!--
Make it feel practical. Line: "We do not need superhero reviewers. We need better instruments."
Line: "Tools are just examples. The pattern is surfacing impact at the decision point."
-->

---

# Review Aids

Two examples of a bigger pattern

# [Terraform Plan Commenter][plan-commenter]

- Run plan in CI
- Post a clear summary in the PR

# [AWS IAM `*` expander][iam-expander]

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
-->

[plan-commenter]:
  https://github.com/marketplace/actions/terraform-plan-commenter
[iam-expander]: https://github.com/marketplace/actions/expand-aws-iam-wildcards

---

# Live PR Example

- Wildcard expansion turns `*` into meaningful info
- Terraform plan shows up in the PR

[`thekbb/shit-bruce-says#17`][pr-17]

<!--
Use this for the demo instead of screenshots.
Line: "This PR shows both the plan comment and the IAM wildcard expansion in one place."
Line: "The goal is not this PR. The goal is impact in every review."
-->

[pr-17]: https://github.com/thekbb/shit-bruce-says/pull/17

---

# What Changes When Signal Improves

- Faster reviews
- Fewer risky approvals
- More confident merges

<!--
Outcomes. Line: "Faster reviews, fewer surprises, and a lot less 'wait, what did we just approve?'"
-->

---

# Close

- Reviewers are us
- We deserve better signals at decision time

<!--
Close with the thesis. Line: "Reviewers are us. We need better signals to make the hard calls. AI can draft the change.
We still sign for the blast radius."
-->

---
