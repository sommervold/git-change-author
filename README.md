# git-change-author

This is a script that changes the author and committer of several commits in a git repository.
This is very dangerous and could mess up your repository. manually check everything before pushing changes.

## Usage

Feed commit hashes through stdin. Each line must have this format:

`COMMIT_HASH|AUTHOR_NAME|AUTHOR_EMAIL`

This will update commit `COMMIT_HASH` to have author `AUTHOR_NAME <AUTHOR_EMAIL`. Commit date and author date is set to the author date.
If a merge conflict occurs, you have to resolve it and commit the changes. Make sure the resolution and merge commit is identical to the original merge commit. You will be prompted on how if one occurs.

An example execution can be:

```
# commits.txt
40c115a80c8edcd48a8bc4f1614a06967009b7e9|Person 1|email1@example.com
b0c4374593324cb02cffcb428b2b2b4b18e563cf|Person 2|email2@example.com
57cb9bbc36c975e9a58a0cc17dbe4acebd629180|Person 1|email1@example.com
3fc62637c6443a5c4af9d22e9c42b1d8fb52d68d|Person 1|email1@example.com

```

`cat commits.txt | git-change-author`

Note that `commits.txt` has to end in a single newline.

If you just want to set the committer and author to be the same, you can generate a commit list with `git log --format="%H|%an|&ae"`
