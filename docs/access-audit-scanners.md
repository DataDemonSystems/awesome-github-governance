# GitHub Access Audit Scanners

Access audit scanners are valuable because they make hidden GitHub access visible quickly.

They are usually best when the immediate goal is to answer: who has access to what?

## What Scanners Are Good At

Good scanner use cases:

- one-off access snapshots
- local reporting
- security review preparation
- scheduled CI reports
- identifying admins, outside collaborators, and direct access
- producing JSON, Markdown, or HTML artifacts

Scanners are often the fastest way to move from "we have no idea" to "we have findings."

## What Scanners Do Not Solve Alone

A scanner report is not the same as a governance workflow.

Someone still has to decide:

- which findings matter
- who owns each repository
- which direct grants should be removed
- which access should move into teams
- which exceptions are justified
- who approves the changes
- how the changes are applied
- how evidence is retained

The scanner can create the list. The organization still needs an operating model.

## gh-iga Style Reports vs Repod

| Question | Access audit scanner | Repod |
| --- | --- | --- |
| What is the main job? | Produce an access report quickly. | Turn access findings into a review and cleanup workflow. |
| Best fit | Security engineer or platform engineer running a scan. | Team-based review, delegated access cleanup, and audit evidence. |
| Output | Static report artifacts. | Reports, maps, workbook workflows, diffs, and account-scoped history. |
| Cleanup | Usually manual or external. | Built around moving findings into reviewed changes. |
| Long-term use | Scheduled reports can show recurring risk. | Ongoing governance loop for access operations. |

## Recommended Pattern

Use a scanner when:

- you need a fast local snapshot
- a report artifact is enough
- the next step will be handled manually
- the team wants a low-friction first look

Use Repod when:

- the report needs an owner
- cleanup needs review
- direct grants need to become team access
- managers need to participate
- audit evidence should come from the workflow

## References

- gh-iga: https://github.com/abhishek20c/gh-iga/tree/main
- gh-iga article: https://dev.to/abhishek_chowdhury_466115/who-actually-has-admin-access-to-your-github-repos-most-teams-have-no-idea-31kj
- Repod vs gh-iga: https://repod.dev/web/compare/repod-vs-gh-iga
- Repod GitHub access audit tool: https://repod.dev/web/solutions/github-permission-audit-tool
- Repod free GitHub access audit: https://repod.dev/web/tools/free-github-access-audit

