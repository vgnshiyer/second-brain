Created on 2024-06-29_09-59-02

## 📔 Notes

### Gerrit

- A git server like github that manages code though `changes`.
- Changes are associated with Ids.
- Add the changeId to the footer of the commit for the commit to be picked up along with an existing change.
- A `change` is gerrit is like a `pull request` in github.
- In gerrit we push with either `refs/for/*` of `refs/heads/*`.
    - refs/for/* --> this is used when you want to push a change for review. eg. `refs/for/master` will create a change in master branch for review.
    - refs/heads/* --> this is used when you want to push to a branch directly bypassing the review.

**Note:** `git push refs/heads/master` is not similar to `git push --force`. The latter only pushes the change to the remote branch if it can be fast-forwarded. Whereas command like `git push origin refs/heads/master --force` aims to re-write history.

#### Important workflows

1. Create a new change: `git push origin HEAD:refs/for/master`

--> creates a new change for review in the master branch

2. Update a patchset: If you need to update a change after receiving feedback, you can create a patchset with ammend.
```bash
git commit --amend
git push origin HEAD:refs/for/master
```

Alt.
```bash
# fetching a change to create a patchset
git fetch origin refs/changes/45/12345/1 
# refs/changes/ --> namespace for changes in Gerrit
# 45 --> last 2 digits of change num, gerit manages changes in folders 
# 12345 --> change number
# 1 --> patchset number

git checkout FETCH_HEAD
# fetching stores the patch in Fetch head. Checking out brings it in local.

# you make your changes

git commit --amend -m "Updated patchset"

# create new patchset
git push HEAD:refs/for/master
```

- patchset is a version of the change
- only the latest patchset if applied to the target branch.

3. Creating dependent changes: Push the series of commits in sequence. Each commit will be a separate change for review that will depend on the previous one.
```bash
git push origin HEAD:refs/for/master
```

4. Cherrypicking: Pick a change from a different branch to the target branch for review.
```bash
git checkout target-branch
git cherry-pick <commit-id>
git push origin HEAD:refs/for/target-branch
```

5. Rebasing a change: If change is out of date, you may need to rebase it on TOT.
```bash
git fetch origin
git rebase origin/master
git push origin HEAD:refs/for/master
```
**Tipani:** To check if your commit is at the top-of-tree or not, try and see if the output of the `git fetch` command is empty or not. If not, `rebase`.

6. Submit a change: After the review, the change can be submitted to be merged by gerrit.

7. Revert a change: 
```bash
# revert by the commit-id
git revert <commit-id>
git push origin HEAD:refs/for/master
```

#### Terms in gerrit
1. projects --> repositories or set of repositories
2. branches --> similar to branches in git (eg. developer branches)
3. codelines --> versions of the code (dev, preprod, prod)

#### Review scoring
```bash
+2 --> lgtm, approved
+1 --> lgtm, some1 else must approve
0 --> no score
-1 --> prefer not submit
-2 --> shall not submit
```

Useful link:
- https://gerrit-review.googlesource.com/Documentation/intro-gerrit-walkthrough.html
- https://gerrit-review.googlesource.com/Documentation/intro-gerrit-walkthrough-github.html
- https://gerrit-review.googlesource.com/Documentation/intro-user.html

Big difference I noticed in gerrit: It asks you to submit a review in each branch, for each commit. Whereas in github, you cam directly push to a branch.

## 🔗 Links

- [[Road to principal engineer]]
