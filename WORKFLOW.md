# Git Team Sync Workflow

## 1. What did the rejected push error message tell you, and why did it happen?

The rejected push said that the remote contained work that I did not have locally and that the update was rejected because it was not a fast-forward. This happened because another clone had pushed changes to the same feature branch after my local branch had diverged. Git rejected my push rather than overwriting the remote commits.

The first rejection happened when Clone B tried to push its rounding change before fetching Clone A's VIP bonus commit. The second rejection happened when Clone A tried to push its new loyalty-point change before fetching the merge that Clone B had pushed.

## 2. What's the actual difference between how you resolved Task 3 (merge) vs Task 4 (rebase)?

In Task 3, I used a merge. I fetched the remote changes and merged them into Clone B's feature branch. Git created a merge conflict in `orders.js`, and I resolved it by keeping both behaviors: the VIP 1.5x bonus for orders over $100 and rounding the loyalty points with `Math.round()`. The merge produced a merge commit.

In Task 4, I used a rebase instead of a merge. I fetched the remote changes and rebased my local commit on top of the updated `feature/loyalty-points` branch. This caused another conflict in `orders.js`. I resolved it by preserving the remote rounding behavior while incorporating my new `+ 1` loyalty-point bonus. After resolving the conflict, I continued the rebase and pushed normally without using force.

The main difference is that merge combines two histories with a merge commit, while rebase replays my local commit on top of the updated remote history.

## 3. What one habit would have avoided both rejected pushes in this lab?

A useful habit would be to fetch the remote branch before starting work or before pushing to a shared branch. Running `git fetch origin` and checking whether the remote branch has moved would have shown that another clone had pushed changes. Keeping my local branch synchronized with the shared remote would have prevented both rejected pushes.

## 4. Which approach - merge or rebase - would you default to on a shared team branch, and why?

I would default to merge when working directly on a shared team branch because it preserves the actual branch history and does not rewrite commits that other developers may already have. Rebase is useful for organizing local work before sharing it, but I would be more cautious about rebasing commits that are already being used by teammates.
