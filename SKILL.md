---
name: pull-request-branch-independence
description: Keep ordinary pull request branches independent from other unmerged pull requests by branching from the current base, checking ancestry and diff scope, and rebuilding accidental stacks. Use when creating or recreating pull requests unless stacked pull requests are explicitly requested.
---

# Pull Request Branch Independence

Use this skill when creating or recreating a pull request in a single-user AI-agent repository workflow.

Keep ordinary pull requests independent from other unmerged pull requests.
Use a stacked pull request only when the user explicitly requests one.

## Create from the current base

Resolve the pull request base branch from the user's instruction, repository guidance, or surrounding workflow.

Before creating a work branch, obtain the latest head of that base branch.
Create the work branch directly from that head.

Do not use the head, branch, or commit of another unmerged pull request as the starting point, merge source, or cherry-pick source for the new pull request.

When the new work requires changes from an earlier pull request, wait until that pull request is reflected in the base branch, then create the new work branch from the updated base.

When creating multiple pull requests in parallel, create each one independently from its applicable base branch.
Do not use a stated merge order in pull request descriptions as a substitute for independent commit history.

## Verify independence before creating the pull request

Before creating or updating the pull request, use available Git or GitHub history comparison to confirm:

1. the new head descends from the intended base branch history;
2. the head of another unmerged pull request targeting the same base is not an ancestor of the new head;
3. when another pull request's head appears in the ancestry, those commits are already reachable from the base branch; otherwise treat the branch as stacked;
4. the diff against the base does not contain changes that belong only to another unmerged pull request.

When an accidental stack or unrelated inherited diff is present, do not create or update the pull request from that branch.
Recreate the work branch from the latest base and move only the changes belonging to the current pull request.

## Verify independence after creation

After creating the pull request, verify its base, head, and commit range.

The pull request is independent only when merging its head into the base would not also make another unmerged pull request's head reachable from the base.

When the created pull request is accidentally stacked, recreate it from the latest base with only its own changes.
