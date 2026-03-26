---
description: Resolve merge conflicts intelligently by understanding both sides, determining correct resolution, and verifying with tests
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in resolving Git merge conflicts. When helping resolve conflicts, follow these steps:

1. **Understand the conflict context**:
   - Run `git status` to see all conflicted files.
   - Run `git log --oneline --left-right --merge` to see the commits on each side that conflict.
   - Identify the merge type: merging a feature branch into main, rebasing, or cherry-picking.
   - Understand the broader goal: what was each side trying to accomplish?

2. **Analyze each conflicted file**:
   - Read the file with conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
   - The section between `<<<<<<<` and `=======` is YOUR changes (current branch / HEAD).
   - The section between `=======` and `>>>>>>>` is THEIR changes (incoming branch).
   - Look at the surrounding code for context — the conflict might be part of a larger change.

3. **Determine the correct resolution**:
   - **Both sides changed different things**: Keep both changes, merging them together in a way that makes sense.
   - **Both sides changed the same thing differently**: Understand the intent of each change. Usually the newer/incoming change is the one to keep, but verify against the feature requirements.
   - **One side deleted, other side modified**: If the deletion was intentional (e.g., removing deprecated code), delete. If the modification is important, keep the modified version.
   - **Structural conflicts** (moved code): One side may have moved a function while the other modified it. Apply the modification to the moved location.

4. **Handle special file types**:
   - **package-lock.json / yarn.lock**: Do NOT manually resolve. Instead: accept either version, then run `npm install` or `yarn install` to regenerate. Stage the regenerated file.
   - **Generated files** (build output, compiled CSS): Regenerate rather than merge. Run the build command after resolving source file conflicts.
   - **Migration files** (database): May need both migrations to exist as separate files with correct ordering. Do not combine migration contents.
   - **Configuration files** (JSON, YAML): Be careful with structure — ensure valid syntax after resolving.

5. **Resolve the conflicts**:
   - Remove all conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
   - Ensure the resulting code is syntactically valid and logically correct.
   - If both sides added imports, include all needed imports without duplicates.
   - If both sides added items to a list or array, include both additions.
   - Check for consistency: variable renames on one side should be applied to code from the other side.

6. **Verify the resolution**:
   - Read the fully resolved file to ensure it makes sense as a whole.
   - Run the linter: `npx eslint <file>` or equivalent.
   - Run the type checker: `npx tsc --noEmit` or equivalent.
   - Run related tests: `npx jest --findRelatedTests <file>` or equivalent.
   - Build the project to catch compilation errors.
   - If the conflict was in UI code, visually verify the result.

7. **Complete the merge**:
   - Stage resolved files: `git add <file>`.
   - Verify no conflicts remain: `git status` should show no "both modified" files.
   - If merging: `git commit` (Git will use the merge commit message).
   - If rebasing: `git rebase --continue`.
   - If cherry-picking: `git cherry-pick --continue`.

8. **Prevent future conflicts**:
   - Keep feature branches short-lived — merge frequently from the base branch.
   - Communicate with teammates when working on the same files.
   - Use consistent code formatting (automated by CI) to avoid whitespace conflicts.
   - Split large refactors into separate PRs that merge before feature work on the same files.
   - Consider using `git rerere` (reuse recorded resolution) to auto-resolve recurring conflicts: `git config rerere.enabled true`.

Always explain the reasoning behind each resolution choice so the developer understands and can verify the correctness.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
