---
name: pull-request-branch-independence
description: Keep ordinary pull requests independent so merging one does not also make another unmerged pull request's current head reachable from the same base. Use when creating or recreating pull requests unless stacked pull requests are explicitly requested.
---

# Pull Request Branch Independence

Use this skill when creating or recreating a pull request in a single-user AI-agent repository workflow.

Keep ordinary pull requests independent from other unmerged pull requests.
Use a stacked pull request only when the user explicitly requests one.

A pull request is independent when merging its head into its base would not also make the current head of another unmerged pull request targeting that base reachable from the base.

## Create from the current base

Resolve the pull request base branch from the user's instruction, repository guidance, or surrounding workflow.

Before creating a work branch, obtain the latest head of that base branch.
Create the work branch directly from that head rather than from another unmerged pull request's head.

When the new work requires an earlier pull request's result, wait until that result is reflected in the base branch, then create the new work branch from the updated base.

When creating multiple pull requests in parallel, create each one independently from its applicable base branch.

## Verify independence before creation

Before creating or updating the pull request, use available Git or GitHub history comparison to confirm that the current head of no other unmerged pull request targeting the same base is an ancestor of the new head.

When another unmerged pull request's current head is an ancestor of the new head, treat the branch as stacked.
Unless stacked pull requests were explicitly requested, recreate the work branch from the latest base without that ancestry before creating or updating the pull request.

## Verify independence after creation

After creating the pull request, verify its base, head, and commit ancestry again.

Confirm that merging this pull request's head into the base would not also make another unmerged pull request's current head reachable from the base.

When the created pull request is accidentally stacked, recreate it from the latest base without the other pull request's head in its ancestry.

This skill owns pull request branch-history independence.
Pull request scope, review criteria, implementation work, and provider-specific pull request creation mechanics remain with their surrounding workflows.
