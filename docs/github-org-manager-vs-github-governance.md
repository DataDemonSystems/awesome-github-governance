# github-org-manager And YAML-Based GitHub Organization Management

github-org-manager is a configuration-first approach for managing GitHub organization members, teams, and repository permissions.

It is a good fit when the organization wants GitHub org state expressed in YAML and reviewed as code.

## What github-org-manager Is Good At

Good github-org-manager use cases:

- managing members and teams from YAML
- representing repository permissions in configuration
- reducing individual permissions by moving access into teams
- applying a consistent organization model
- reviewing changes in version control
- running dry-run style checks before applying changes

This is a strong model when the organization has enough discipline to treat GitHub org structure as managed configuration.

## The Hard Part: Knowing The Model

YAML works well when the target state is clear.

It is harder when:

- current access is messy
- repository ownership is unclear
- team hierarchy does not match how the company now works
- legacy direct grants exist everywhere
- teams have broad access for historical reasons
- non-platform stakeholders need to decide access changes

In those cases, the first task is not writing YAML. The first task is discovering and agreeing the model.

## github-org-manager vs Repod

| Question | github-org-manager | Repod |
| --- | --- | --- |
| What is the main job? | Manage GitHub org state from YAML. | Review live access state and turn findings into safe changes. |
| Best fit | Organizations ready for GitHub org-as-code. | Organizations still resolving drift, ownership, and exceptions. |
| Review surface | Pull requests and YAML diffs. | Org maps, reports, spreadsheets, access diffs, and workflow screens. |
| Direct grants | Discouraged or managed as config. | Surfaced as findings that need review or cleanup. |
| Delegation | Mostly through repository/config review workflows. | Designed to let operators participate without broad GitHub org admin. |

## Recommended Pattern

Use github-org-manager when:

- the target organization model is agreed
- platform engineers should own GitHub org configuration
- YAML review is acceptable for the people making access decisions
- the organization wants config as the durable source of truth

Use Repod before or alongside github-org-manager when:

- the current model needs discovery
- managers need a non-code review surface
- direct grants need review
- repository ownership needs cleanup
- audit evidence needs to be produced from access reviews

## Migration Pattern

A practical sequence:

1. Use discovery to inventory members, teams, repositories, and access.
2. Identify direct grants, broad-access teams, stale teams, and orphaned repositories.
3. Decide repository ownership and intended team access.
4. Review proposed changes with system owners.
5. Apply cleanup.
6. Encode stable long-term structure in YAML if the organization wants org-as-code.

This avoids writing configuration around a broken access model.

## References

- OpenRailAssociation/github-org-manager: https://github.com/OpenRailAssociation/github-org-manager
- Repod vs github-org-manager: https://repod.dev/web/compare/repod-vs-github-org-manager
- Repod GitHub Team permissions vs direct access guide: https://repod.dev/web/docs/github-team-access-vs-direct-repository-access
- Repod delegated access guide: https://repod.dev/web/docs/delegate-github-repo-team-access-without-org-admin
- GitHub teams documentation: https://docs.github.com/en/organizations/organizing-members-into-teams/about-teams

