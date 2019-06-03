# Scripts

The following scripts may be used for various shared purposes in our projects to
simplify the process

## Semantic Versioning
An [Semantic Versioning][semver] [script](semver-bump) is provided that can be placed somewhere
in your `$PATH`. This script allows you to easily generate a release tag and
release notes for a project.

You will need to have a default `editor` setup in your [git
configuration][git-config] for this to work properly. Here are a few examples:

```
$ git config --global core.editor "atom --wait"

$ git config --global core.editor "subl -n -w"

$ git config --global core.editor "vim"

$ git config --global core.editor "emacs"
```

[semver]: https://semver.org/
[git-config]: https://www.git-scm.com/book/en/v2/Customizing-Git-Git-Configuration
