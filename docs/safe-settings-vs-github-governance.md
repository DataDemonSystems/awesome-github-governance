# safe-settings For GitHub Policy-As-Code

safe-settings is a policy-as-code approach for enforcing GitHub settings from configuration. It is strongest when the problem is repository and organization settings drift.

GitHub access governance is related, but it is not the same problem.

## What safe-settings Is Good At

safe-settings is useful when an organization wants settings to be controlled from an admin repository and applied through a GitHub App/service model.

Good safe-settings use cases:

- enforcing repository settings
- maintaining branch protection and rules
- applying organization or repository configuration from files
- validating settings changes
- running dry-run or scheduled sync behavior
- reacting to GitHub events

This is a strong model when the target settings are known and the team wants enforcement.

## What safe-settings Is Not Primarily For

safe-settings is not primarily a human access-review workflow.

It does not, by itself, answer every governance question:

- Which team owns this repository?
- Why does this user have direct access?
- Which repositories have broad read or write access?
- Which access should be removed after offboarding?
- Which exceptions should become teams?
- Which findings are ready to be shown to an auditor?

Those questions require discovery, ownership decisions, review, and evidence.

## Policy Enforcement vs Governance Review

Policy enforcement assumes the policy exists.

Governance review often starts before the policy is clear.

Example:

- safe-settings can enforce a branch protection policy once the repository should have that policy
- governance review asks whether the repository is production, who owns it, who can change workflows, who can administer it, and whether current access is justified

Both layers are useful. They solve different parts of the problem.

## safe-settings vs Repod

| Question | safe-settings | Repod |
| --- | --- | --- |
| What is the main job? | Enforce GitHub settings from configuration. | Review and operate GitHub repo-team access. |
| Best fit | Repository settings, policy validation, scheduled sync. | Permission drift, direct grants, ownership review, audit evidence. |
| Operating model | GitHub App/service plus admin repository. | SaaS review workflow with reports, exports, diffs, and delegated admin. |
| Human review | Strong for code/config review of settings. | Strong for access review by operators, managers, and platform teams. |
| Complementary use | Enforce stable repository policy. | Discover and clean access model before or alongside enforcement. |

## Recommended Pattern

Use safe-settings when:

- repository settings are the main source of drift
- the team has a stable policy model
- policy changes should be made through config
- event-driven or scheduled enforcement is wanted

Use Repod when:

- direct grants and team permissions need review
- access ownership is unclear
- repository access cleanup needs human approval
- managers need to participate without GitHub org admin
- audit evidence needs to explain access decisions

## References

- github/safe-settings: https://github.com/github/safe-settings
- GitHub protected branches: https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches
- GitHub CODEOWNERS: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners
- GitHub Actions secure use: https://docs.github.com/en/actions/reference/security/secure-use
- Repod vs safe-settings: https://repod.dev/web/compare/repod-vs-safe-settings
- Repod blanket write access risk guide: https://repod.dev/web/docs/blanket-github-write-access-risk

