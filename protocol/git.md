Git Protocol
============

A guide for programming within version control.

Maintain a Repo
---------------

* Avoid including files in source control that are specific to your
  development machine or process by adding their formats to the .gitignore file.
Look at [GitHub's gitignore repo][git-ignore] for starting points depending on
the programming language.
* Delete local and remote feature branches after merging.
* Perform all new work in a feature branch.
* Rebase frequently to incorporate upstream changes.
* Use a [pull request] for code reviews.
* Never commit any sensitive information such as files with passwords, SSH keys,
  etc. to a repository.

[git-ignore]: https://github.com/github/gitignore
[pull request]: https://help.github.com/articles/using-pull-requests/

Write a Feature
---------------

For all new development work, create a local feature branch based off develop.
Please use a user-friendly feature name for your branch, such as
feature/add-gridview-display.

    git checkout master
    git pull
    git checkout -b <feature-name>

Rebase frequently to incorporate upstream changes.

    git fetch origin
    git rebase origin/master

Resolve conflicts. When feature is complete and tests pass, stage the changes.

    git add --all

When you've staged the changes, commit them.

    git status
    git commit --verbose

Write a [good commit message]. Example format:

    Present-tense summary under 50 characters

    * More information about commit (under 72 characters).
    * More information about commit (under 72 characters).


If you've created more than one commit, use a rebase to squash them into
cohesive commits with good messages. You can also do this after the pull request
is created, if you receive feedback that requires additional commits.

See the git documentation for [rebase] or this tutorial on [squashing commits
with rebase].

    git rebase -i origin/master

Push your branch to GitHub.

    git push origin <feature-name>

Submit a [GitHub pull request] after confirming the **entire test suite** passes
locally.

If you have already submitted a pull request and need to rebase to squash additional commits you will likely need to force push your squashed commit.

  `git push --force-with-lease origin <feature-name>`

*Please do not submit PRs on the last day of a Sprint. This does not give the
  team adequate time for the review process prior to creating a release.*

[good commit message]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
[GitHub pull request]: https://help.github.com/articles/using-pull-requests/
[rebase]: http://git-scm.com/docs/git-rebase
[squashing commits with rebase]:
http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html

Pull Requests
-----------

* Use the [Code Review](code_review.md) guidelines to avoid miscommunication.
* If two or more members of `@ucsdlib/developers` have signed off on a PR, the
  creator of the PR should request a merge.
* The feature branch should always be deleted following the merge of a PR.
