# GitHub Governance Tooling Comparison

GitHub governance can be approached through several tool categories. None of them is universally correct. The right choice depends on whether the organization needs discovery, human review, policy enforcement, configuration as code, or repeatable audit evidence.

This document compares common approaches:

- Terraform with the GitHub provider
- safe-settings
- github-org-manager
- access audit scanners such as gh-iga
- Repod as a reviewable GitHub governance workflow

## Summary

| Approach | Best for | Weak spot |
| --- | --- | --- |
| Terraform GitHub provider | Encoding known desired state in infrastructure-as-code workflows | Less natural for messy discovery, ownership decisions, and non-technical review |
| safe-settings | Enforcing repository settings and policy from configuration | Not primarily an access-review or ownership-discovery workflow |
| github-org-manager | YAML-based GitHub org member, team, and repo permission management | Requires the organization to be ready to express the model as config |
| gh-iga and scanners | Fast access reports and local evidence artifacts | Reports do not automatically become operated cleanup workflows |
| Repod | Reviewing live access drift, planning changes, delegating cleanup, and generating governance evidence | Not a replacement for policy-as-code or IaC when the desired state is already mature |

## The Main Distinction

Most GitHub governance tools sit on one side of this line:

- **Known desired state:** the team already knows how the organization should look and wants software to enforce it.
- **Unknown or disputed desired state:** the team first needs to understand the current state, review ownership, identify exceptions, and agree what should change.

Terraform, safe-settings, and github-org-manager are strongest when the desired state is known or can be encoded in configuration.

Repod is strongest when the organization needs to turn live GitHub state into a reviewed operating model before enforcement.

## Terraform GitHub Provider

Terraform is useful when GitHub resources are part of a broader infrastructure platform and changes should flow through existing plan/apply review workflows.

Typical fit:

- repositories are created from templates or platform modules
- teams and memberships are managed from code
- repository settings are part of an infrastructure lifecycle
- change review already happens in pull requests
- the desired state is clear

Common tension:

- a Terraform plan is good at showing changes to declared resources
- it is less good at explaining why a direct GitHub grant exists, which team owns an orphaned repository, or whether a broad-access team is still justified

Use Terraform when GitHub governance is ready to become infrastructure-as-code. Use a discovery and review workflow before Terraform when the model is still unclear.

## safe-settings

safe-settings is designed around policy and settings enforcement through a GitHub App, configuration, validators, dry-run behavior, and scheduled or event-driven sync.

Typical fit:

- repository settings need consistent enforcement
- branch protection, rules, labels, or settings should drift back to policy
- the organization wants validators around GitHub settings changes
- the team can operate a GitHub App/service model

Common tension:

- safe-settings is a strong policy-as-code tool
- it is not primarily a human workflow for deciding repository ownership, cleaning direct grants, or running access reviews with engineering managers

Use safe-settings when settings policy is the problem. Use access governance tooling when access drift and ownership are the problem.

## github-org-manager

github-org-manager is a configuration-first approach for managing GitHub organization state through YAML.

Typical fit:

- members, teams, and repository permissions should be represented in files
- the team wants a versioned source of truth for org structure
- maintainers are comfortable reviewing YAML changes
- individual permissions and unmanaged access should be reduced

Common tension:

- configuration works best after the team knows the target model
- many organizations need a review phase before they can safely encode the model

Use github-org-manager when the organization is ready for GitHub org-as-code. Use a review layer first when the current state is messy.

## Access Audit Scanners

Access audit scanners are valuable because they make hidden access visible quickly.

Typical fit:

- the team needs a fast report
- local execution is preferred
- a security engineer wants a snapshot for review
- scheduled CI reports are enough

Common tension:

- a report is not the same as an operating model
- someone still has to assign owners, decide changes, review exceptions, and apply cleanup

Use scanners when the immediate need is visibility. Use a workflow layer when findings must become reviewed changes.

## Where Repod Fits

Repod is positioned between raw discovery and enforcement.

It helps when:

- nobody has a clear organization-wide access picture
- direct grants and broad teams need review
- access changes need to be planned before they are applied
- managers or operators need to participate without GitHub org admin
- evidence needs to be produced for access review, SOC 2, ISO 27001, or internal governance
- spreadsheet-shaped planning is useful before changes become automation

Repod can complement other tools:

- use Repod to understand and clean the model before encoding it in Terraform or YAML
- use Repod to generate review evidence alongside policy-as-code
- use Repod to identify access drift that a settings enforcement tool does not cover

## Recommended Decision Path

1. If the target state is unknown, start with discovery and review.
2. If access exceptions are the main problem, fix the team permission model first.
3. If repository settings drift is the main problem, evaluate safe-settings.
4. If organization state is stable and should be versioned, evaluate Terraform or github-org-manager.
5. If auditors need evidence, make the review workflow produce evidence naturally.

## References

- Terraform GitHub provider: https://registry.terraform.io/providers/integrations/github/latest/docs
- Terraform GitHub provider repository: https://github.com/integrations/terraform-provider-github
- github/safe-settings: https://github.com/github/safe-settings
- OpenRailAssociation/github-org-manager: https://github.com/OpenRailAssociation/github-org-manager
- gh-iga: https://github.com/abhishek20c/gh-iga/tree/main
- GitHub teams documentation: https://docs.github.com/en/organizations/organizing-members-into-teams/about-teams
- GitHub repository roles: https://docs.github.com/en/organizations/managing-user-access-to-your-organizations-repositories/managing-repository-roles/repository-roles-for-an-organization
- Repod comparison pages: https://repod.dev/web/docs

