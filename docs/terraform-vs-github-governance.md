# Terraform For GitHub Governance

Terraform can be a strong way to manage parts of GitHub, especially when GitHub resources are treated like infrastructure and changes should pass through plan, review, and apply.

The key question is whether the organization already knows the desired state.

## What Terraform Is Good At

Terraform is best when GitHub configuration is part of a declared, versioned infrastructure model.

Good Terraform use cases:

- creating repositories from standard modules
- managing teams and memberships from code
- assigning known team-to-repository permissions
- managing repository settings that should be reviewed through pull requests
- keeping GitHub changes aligned with broader platform infrastructure
- using plan/apply workflows for reviewable changes

In this model, GitHub is another infrastructure surface.

## Where Terraform Gets Awkward

Terraform is less natural when the hard problem is not applying a known state, but discovering what the state should be.

Examples:

- nobody knows which team owns an old repository
- a direct grant exists but nobody knows why
- contractors have mixed access through teams and direct repository permissions
- GitHub Actions workflows have deployment reach that is not reflected in the access model
- engineering managers need to review access without editing Terraform
- compliance teams need evidence of human review, not only an apply log

Terraform can encode decisions. It does not automatically make those decisions easier.

## The Discovery Gap

Many organizations try to move GitHub into Terraform before they understand the current access model.

That usually creates friction:

- existing manual exceptions have to be imported or overwritten
- stale access becomes harder to reason about
- non-platform stakeholders struggle to review code-based permission changes
- the Terraform repository becomes the bottleneck for every access question

This is not a Terraform problem. It is a sequencing problem.

The safer sequence is:

1. Inventory current repositories, teams, members, and permissions.
2. Identify direct grants, broad teams, orphaned repositories, and stale access.
3. Decide ownership and target permissions.
4. Review the proposed changes with the relevant owners.
5. Apply or encode the stable model.

Terraform is a better fit after step 4 than before step 1.

## Terraform vs Repod

| Question | Terraform GitHub provider | Repod |
| --- | --- | --- |
| What is the main job? | Encode and apply declared GitHub resources. | Review live GitHub access and plan safe changes. |
| Who is the primary user? | Platform engineers comfortable with IaC. | Platform teams, engineering managers, GitHub admins, operators, and consultants. |
| What is the review surface? | Pull requests and Terraform plans. | Org maps, access reports, spreadsheets, diffs, and governance reports. |
| What happens when ownership is unclear? | The model must be decided before it can be encoded. | The workflow helps expose and resolve unclear ownership. |
| Does it replace Terraform? | No. | No. Repod can produce the reviewed model that later becomes Terraform. |

## Recommended Pattern

Use Terraform when:

- the target model is already stable
- changes should be code-reviewed by platform engineers
- GitHub is part of a broader infrastructure platform
- the team is comfortable with import, drift, state, and provider behavior

Use Repod before or alongside Terraform when:

- direct grants need cleanup
- teams need to review repository ownership
- access findings need to become a human decision
- managers need a review surface outside code
- audit evidence matters

## Practical Example

A platform team wants all production repositories managed through Terraform.

Before encoding that state, it should answer:

- Which repositories are production?
- Which teams own them?
- Which teams should have read, triage, push, maintain, or admin?
- Which direct grants should be removed?
- Which access is temporary?
- Which repositories should be archived?
- Which Actions workflows can publish packages or deploy?

Once those decisions are reviewed, Terraform can be a good place to encode stable policy.

## References

- Terraform GitHub provider: https://registry.terraform.io/providers/integrations/github/latest/docs
- Terraform GitHub provider repository: https://github.com/integrations/terraform-provider-github
- GitHub repository roles: https://docs.github.com/en/organizations/managing-user-access-to-your-organizations-repositories/managing-repository-roles/repository-roles-for-an-organization
- GitHub teams documentation: https://docs.github.com/en/organizations/organizing-members-into-teams/about-teams
- Repod export, review, apply workflow: https://repod.dev/web/docs/export-review-apply-repo-team-access
- Repod GitHub governance guide: https://repod.dev/web/docs/github-org-permissions-governance

