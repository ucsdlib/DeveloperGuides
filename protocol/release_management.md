## Summary

Overview of the release management process for all software applications.

*Note:* At the moment, we are in a transition between Jenkins and CircleCI. As a
result, there will be some noted differences throughout this document that will ultimately be modified as things resolve between Jenkins and CircleCI. The current thinking is that we will transition all applications to Jenkins, eventually. For specifics on CircleCI and the newer
"chatops" workflow, please see the [Environment Variables
repository][env-variables]

## Release and QC
1. Development Manager will assign a developer as Release Manager for the
   application.
2. Development Manager will create a GitHub issue for the release and assign to
   the Release Manager.
3. Release Manager will navigate to develop branch
```
git checkout develop
```
4. Release Manager will create a release branch using the proper version for the
   branch name.
```
git flow release start 1.2.3
# or
git checkout -b release/1.2.3
```
5. For projects where there is an application version file, update to match the
   release version and commit the file to the release branch.
6. Publish the local release branch to Github
```
git flow release publish 1.2.3
# or
git push origin release/1.2.3
```
7. _Deprecated(do not use in new apps)_ Move the staging tag to point to the release branch and push tag to Github
```
git tag -a -f staging -m "release 1.2.3"
git push -f --tags
```
8. CircleCI or Jenkins will detect the `release/1.2.3` branch and will run test suite and
   static analysis tooling. If successful, application will be
deployed to the test environment. If not, Release Manager is responsible for
fixing reported errors.
9. Release Manager will assign the Deploy issue to the Product Owner for
   review, highlighting areas that need to be tested.
10. If problems are detected:
  - The Development Team will make needed code changes on the release branch
  - Commit and push changes to the remote branch
  - Write additional tests, if necessary, to cover the problem space detected
  - Run application test suite and Code Climate to verify all tests and
     analysis tools pass.
11. When Product Owner signs off on release, they will assign to Release
    Manager.

## Production
1. When Product Owner has assigned the Deploy issue back to the Release
   Manager, the release branch must be finished prior to deployment.
```
git fetch master
git flow release finish 1.2.3
git push
git push --tags
```
**or**
```
# update develop branch if changes were made in release branch
git checkout develop
git rebase release/1.2.3
git push origin develop

# update master branch
git checkout master
git rebase release/1.2.3
git push origin master
git push origin master --tags #if needed

# delete release branch
git branch -d release/1.2.3
git push origin -d release/1.2.3
```
2. Release Manager should [create a release][release] off `master` and document changes.
3. Release Manager assigns Deploy issue to Operations for Production release.
4. When application is released to Production Operations assigns Deploy issue
   back to Product Owner for final review.
5. Product Owner can close Deploy issue is release is acceptable, or assign
   back to Release Manager with noted bugs. In this case either:
  * A hotfix will be created to address a significant bug
  * A new GitHub issue will be created to address the bug in a future Sprint.

[release]:https://help.github.com/articles/creating-releases/
[env-variables]:https://github.com/ucsdlib/env-variables/
