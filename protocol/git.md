Git Protocol
============

A guide for programming within version control.

Maintain a Repo
---------------

* Avoid including files in source control that are specific to your
  development machine or process by adding their formats to the .gitignore file.
* Delete local and remote feature branches after merging.
* Perform all new work in a feature branch.
* Rebase frequently to incorporate upstream changes.
* Use a [pull request] for code reviews.
* Never commit any sensitive information such as files with passwords, SSH keys,
  etc. to a repository.

[pull request]: https://help.github.com/articles/using-pull-requests/

Write a Feature
---------------

For all new development work, create a local feature branch based off develop.
Please use a user-friendly feature name for your branch, such as
feature/add-gridview-display.

    git checkout develop
    git pull
    git flow feature start <feature-name>

Rebase frequently to incorporate upstream changes.

    git fetch origin
    git rebase origin/develop

Resolve conflicts. When feature is complete and tests pass, stage the changes.

    git add --all

When you've staged the changes, commit them.

    git status
    git commit --verbose

Write a [good commit message]. Be sure to reference the JIRA ticket ID in your
commit message to trigger the JIRA workflow updates. Example format:

    Present-tense summary under 50 characters DHH-123

    * More information about commit (under 72 characters).
    * More information about commit (under 72 characters).

    https://<jira-url>/browse/<project>/<ticket>

If you've created more than one commit, use a rebase to squash them into
cohesive commits with good messages. You can also do this after the pull request
is created, if you receive feedback that requires additional commits.

See the git documentation for [rebase] or this tutorial on [squashing commits
with rebase].

    git rebase -i origin/develop

Share your branch.

    git flow feature publish <feature-name>

Submit a [GitHub pull request] after confirming the **entire test suite** passes
locally.

If you have already submitted a pull request and need to rebase to squash additional commits you will likely need to force push your squashed commit.

  `git push -f`

Currently, upon PR creation a JIRA trigger will automatically move the ticket
status to *Code Review Requested* and assign the ticket
to the project lead developer role to perform [Code Review](code_review.md)
However, it is actually the responsibility of the team to review the PR. JIRA is
not able to assign responsibility of a workflow state to a group. Be sure to
send a comment in the PR to the `@ucsdlib/developers` group asking for review.

*Please do not submit PRs on the last day of a Sprint. This does not give the
  team adequate time for the review process prior to creating a release.*

[good commit message]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
[GitHub pull request]: https://help.github.com/articles/using-pull-requests/
[rebase]: http://git-scm.com/docs/git-rebase
[squashing commits with rebase]:
http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html

Review Code
-----------

At least two team members other than the author reviews the pull request. They follow
[Code Review](code_review.md) guidelines to avoid
miscommunication. See [Code Review](code_review.md) for more information.

They make comments and ask questions directly on lines of code in the GitHub
web interface or in the JIRA ticket if non-developer feedback is needed.

When satisfied, the PR is merged by the last developer to sign off and the JIRA workflow will automatically mark
the ticket as Resolved.

Delete the feature branch following the PR merge.
