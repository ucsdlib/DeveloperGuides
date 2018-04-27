# Create New Project

A guide for creating a new GitHub project repository

## Project README.md
Each project should have a `README.md` file. See [Project README's][readme]


## Copy GitHub template files
Copy the files in the `.github` folder in the `DeveloperGuides` repository to `.github` in your new project.

Update each file as needed for the new project.

## Merge Options
Navigate to `Settings` and scroll to `Merge button`

Ensure only `Allow rebase merging` is selected

## Collaborators & teams
Navigate to `Settings` in the repository and click `Collaborators & teams`

At the minimum, you should grant the `Developers` and `Operations` groups `Write` access.

## Jenkins Plans
To ensure Jenkins staging/test plans can automatically build tags, please ensure
the plan has the following configuration:

1. Find the desired plan and click `Configure`
1. Navigate to `Source Code Management`
1. Ensure the git repository URL is setup correctly
1. Click `Advanced` toggle (just below git URL)
1. Set `Refspec` to `+refs/tags/*:refs/remotes/origin/tags/*`
1. Navigate to `Branches to build` subsection
1. Set value of `Branch Specifier` to `*/tags/*

## Capistrano
If the project uses, or will be using, Capistrano with `deploybot`, you need to setup the
environment config files to support dynamically receiving a reference (branch,
commit hash, tag) from deploybot.

For example, `<app>/config/deploy/qa.rb`:

`set :branch, (ENV['BRANCH'] || fetch(:branch, 'master'))`

You can then deploy a tag using `deploybot` as follows(in this case, our tag is
`1.4.1`:

`deploybot deploy damspas/1.4.1 to qa`

## Protected Branches
Navigate to `Settings` in the repository and click `Branches`

Following the [GitHub Flow model][gh-flow], you should select the following in the Branches configuration for the repository:

Default Branch: `master`

Protected Branch - `master`:
  * Project this branch
  * Require pull request reviews before merging
  * Require status checks to pass before merging
  * Require branches to be up to date before merging

[readme]:../best-practices/project_readme.md
[gh-flow]:https://guides.github.com/introduction/flow/
