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

## Protected Branches
Navigate to `Settings` in the repository and click `Branches`

Following the Git Flow model, you should select the following in the Branches configuration for the repository:

Default Branch: `develop`

Protected Branch - `develop`:
  * Project this branch
  * Require pull request reviews before merging
  * Require status checks to pass before merging
  * Require branches to be up to date before merging

Protected Branch - `master`:
  * Project this branch

[readme]:../best-practices/project_readme.md
