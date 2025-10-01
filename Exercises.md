
## Practice Exercises

Level up your Git skills with hands‑on practice. Use a scratch / throwaway repository (NOT an important production repo). For any destructive operations, be sure you understand the implications first. You can repeat these exercises until they feel natural.

### Getting Ready (One‑Time Setup)
```
mkdir git-practice && cd git-practice
git init
echo "Hello" > readme.txt
git add readme.txt && git commit -m "Initial commit"
```

---
### 1. Staging and Amending
Goal: Understand staging granularity and amending commits.
Tasks:
1. Append two new lines to `readme.md`.
2. Stage ONLY the first added line using `git add -p` (interactive patch mode).
3. Commit with message "Partial change".
4. Stage the remaining line and amend the previous commit (no new commit object wanted in history).
5. Show that the commit hash changed (compare old vs new via `git reflog`).
Key Commands: `git add -p`, `git commit --amend`, `git show`, `git reflog`.

### 2. Ignoring Files
Goal: Practice using `.gitignore`.
Tasks:
1. Create files: `notes.log`, `temp.tmp`, `build/output.bin`.
2. Add patterns to `.gitignore` to ignore `.log`, `.tmp`, and `build/` directory.
3. Verify ignored vs untracked with `git status --ignored`.
4. Commit `.gitignore`.
Key Commands: `echo`, editing `.gitignore`, `git status --ignored`.

### 3. Branching & Merging (Fast‑Forward vs Merge Commit)
Goal: See the difference between fast-forward and non fast-forward merges.
Tasks:
1. Create branch `feature/alpha`; add a file `alpha.txt`; commit.
2. Switch back to `main`; make NO changes; merge `feature/alpha` (fast-forward expected).
3. Create branch `feature/beta` from `main` and add `beta.txt`; commit.
4. While on `main`, add `main-only.txt`; commit.
5. Merge `feature/beta` (should produce a merge commit now).
Key Commands: `git branch`, `git checkout -b`, `git merge --no-ff`, `git log --graph --oneline --decorate`.

### 4. Resolving Merge Conflicts
Goal: Gain confidence resolving conflicts.
Tasks:
1. Create branch `conflict-test`.
2. Edit the SAME first line of `readme.txt` differently on both `main` and `conflict-test` (commit each side).
3. Merge `conflict-test` into `main` and resolve the conflict favoring a manually combined line.
4. Verify resolution with `git diff --cached` before committing.
Key Commands: `git merge`, `git status`, `git diff`, conflict markers.

### 5. Interactive Rebase (Cleaning History)
Goal: Squash and reorder commits.
Tasks:
1. On a new branch `cleanup-demo`, make 3 small commits editing `readme.txt`.
2. Run `git rebase -i HEAD~3` and:
   - Reorder the second commit to be last.
   - Squash the last two into the first.
3. Force update (if published) with `git push --force-with-lease` (ONLY on a throwaway branch!).
Key Commands: `git rebase -i`, `git log --oneline`, `git push --force-with-lease`.

### 6. Stash Workflows
Goal: Temporarily shelving work.
Tasks:
1. Create uncommitted edits in two files.
2. Stash them with a message.
3. Make another edit and create a second stash.
4. List stashes; apply the first without dropping; then pop the second.
5. Drop all remaining stashes.
Key Commands: `git stash push -m`, `git stash list`, `git stash apply`, `git stash pop`, `git stash drop`, `git stash clear`.

### 7. Bisect to Find a Bug
Goal: Use binary search to locate a bad commit.
Setup:
1. Create a script `calc.sh` that echoes a number; commit several times changing the number; in one commit introduce a wrong value.
Bisect:
1. Mark a known good earlier commit: `git bisect start` → `git bisect good <hash>`.
2. Mark current head (with bug) as bad: `git bisect bad`.
3. At each step run the script (decide good/bad) until Git identifies the offending commit.
4. End with `git bisect reset`.
Key Commands: `git bisect start`, `git bisect good`, `git bisect bad`, `git bisect reset`.

### 8. Tagging & Releases
Goal: Create semantic version tags.
Tasks:
1. Add a notable change; commit.
2. Create an annotated tag `v1.0.0`.
3. Add another change; tag lightweight `v1.0.1`.
4. Show differences between tags.
Key Commands: `git tag -a v1.0.0 -m "Release 1.0.0"`, `git show v1.0.0`, `git diff v1.0.0 v1.0.1`.

### 9. Cherry-Picking
Goal: Move a specific fix onto another branch.
Tasks:
1. On `feature/exp`, commit a fix in `fix.txt`.
2. Switch to `main`; cherry-pick the fix commit hash.
3. Resolve any conflicts; confirm the file content.
Key Commands: `git cherry-pick <hash>`, `git log -p`.

### 10. Recovery Scenarios
Goal: Practice retrieving lost work.
Scenarios:
1. Create a commit, record its hash, then reset hard to the previous commit. Recover the lost commit via `git reflog` and `git cherry-pick` or branch off the reflog hash.
2. Accidental deletion of a file before committing: restore from index with `git checkout -- <file>` (or `git restore` variant if enabled).
3. After an interactive rebase gone wrong, abort with `git rebase --abort`.
Key Commands: `git reflog`, `git reset --hard`, `git checkout`, `git restore`, `git rebase --abort`.

### 11. Advanced Log & Search
Goal: Master locating history details.
Tasks:
1. Search commits whose messages contain a word.
2. Show only merges.
3. Show commits touching a specific file in a date range.
4. Generate a short one-line graph.
Key Commands: `git log --grep=`, `git log --merges`, `git log --since= --until= -- <file>`, `git log --oneline --graph --decorate`.

### 12. Rewriting Author Info (Local Only)
Goal: Adjust incorrect author on the last commit.
Tasks:
1. Amend latest commit with corrected `--author` (or adjust global config & amend).
2. Verify environment config via `git config --list`.
Key Commands: `git commit --amend --author=`, `git config`.

### 13. Submodules (Optional Advanced)
Goal: Embed another repository.
Tasks:
1. Add a small public repo as a submodule in `vendor/lib`.
2. Commit submodule addition.
3. Update the submodule to a newer commit and record the change.
Key Commands: `git submodule add`, `git submodule update --init --recursive`, `git diff --submodule`.

---
### Suggested Daily Quick Drill (5–10 min)
1. Make a change, stage part of it, amend.
2. Create & switch to a branch, edit, rebase onto main.
3. Stash, switch branches, pop.
4. Log graph review.

### Tips
* Keep `git log --oneline --graph --decorate --all` handy to visualize.
* Use `alias` in your shell or Git config to speed frequent commands.
* Practice in small repeated cycles to build muscle memory.

