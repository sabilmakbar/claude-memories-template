---
name: feedback_example
description: Example working-preference rule — replace with your first real rule
metadata:
  type: feedback
---

State the rule itself first, in one or two plain sentences. For example: always add new
dependencies through the project's package manifest, never with ad-hoc install commands.

**Why:** the generalized reason the rule exists — what goes wrong without it. Keep it
project-agnostic: no repo names, no incident stories.

**How to apply:** when the rule fires and what's exempt. Link related rules with
[[feedback_other_rule]] wikilinks targeting their `name:` field.
