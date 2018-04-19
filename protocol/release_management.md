## Summary

Overview of the release management process for all software applications.

In general, we are following the [GitHub Flow][gh-flow] pattern for managing our
branching and release strategy.

*Note:* At the moment, we are in a transition between Jenkins and CircleCI. As a
result, there will be some noted differences throughout this document that will ultimately be modified as things resolve between Jenkins and CircleCI. The current thinking is that we will transition all applications to Jenkins, eventually. For specifics on CircleCI and the newer
"chatops" workflow, please see the [Environment Variables
repository][env-variables]

## Release and QC
1. Development Manager will assign a developer as Release Manager for the
   application.
2. Development Manager will create a GitHub issue for the release and assign to
   the Release Manager.
3. Release Manager will navigate to master branch and create a tag off the
   commit we want to release from. The example below assumes creating the tag
off the most current commit (_HEAD_). This can be done in [GitHub(preferred)][release], or on the command
line as follows:
```
git tag -a 1.2.3
git push --follow-tags
```

4. In either case, using the GitHub UI or the command line, please enter a
   summary of changes for the release. These will be accessible to interested
stakeholders at a URL such as:
https://github.com/ucsdlib/dmr/releases/tag/v2.0.5
5. For projects where there is an application version file, update to match the
   release version and commit the file to the release branch.
6. CircleCI, DeployBot, and/or Jenkins will need to be setup to deploy the tag, run test suite and
   static analysis tooling. If successful, application will be
deployed to the test environment. If not, Release Manager is responsible for
fixing reported errors.
7. Release Manager will assign the Deploy issue to the Product Owner for
   review, highlighting areas that need to be tested.
8. If problems are detected:
  - A developer will make needed code changes on a new branch off master.
  - Commit and push changes to the new branch.
  - Write additional tests, if necessary, to cover the problem space detected
  - Run application test suite and Code Climate to verify all tests and
     analysis tools pass.
  - Create a Pull Request to get your changes merged back into master
  - Move the release tag to the new commit (_HEAD_) and update the release notes
    accordingly.
11. When Product Owner signs off on release, they will assign to Release
    Manager.

## Production
1. Release Manager assigns Deploy issue to Operations for Production release.
2. When application is released to Production Operations assigns Deploy issue
   back to Product Owner for final review.
3. Product Owner can close Deploy issue is release is acceptable, or assign
   back to Release Manager with noted bugs. In this case either:
  * A hotfix branch will be created to address a significant bug. This will then
    follow the same PR cycle as any other ticket but be addressed immediately.
  * A new GitHub issue will be created to address the bug in a future Sprint.

[release]:https://help.github.com/articles/creating-releases/
[env-variables]:https://github.com/ucsdlib/env-variables/
[gh-flow]:https://guides.github.com/introduction/flow/
