Summary
-------

Overview of the release management process for all software applications.

*Note:* At the moment, we are in a transition between Bamboo and CircleCI. As a
result, there will be some noted differences throughout this document that will ultimately be removed once
Bamboo is removed from the architecture. For specifics on CircleCI and the newer
"chatops" workflow, please see the [Environment Variables
repository](https://github.com/ucsdlib/env-variables/)

## Release and QC
1. Development Manager will assign a developer as Release Manager for the
   application.
2. Development Manager will create a JIRA ticket for the release and assign to
   the Release Manager.
3. Release Manager will navigate to develop branch
```
git checkout develop
```
4. Release Manager will create a release branch using the proper version for the
   branch name.
```
git flow release start 1.2.3
```
5. For projects where there is an application version file, update to match the
   release version and commit the file to the release branch.
6. Publish the local release branch to Github
```
git flow release publish 1.2.3
```
7. Move the staging tag to point to the release branch and push tag to Github
```
git tag -a -f staging -m "release 1.2.3"
git push -f --tags
```
8. Bamboo(or Circle) CI will detect the release/1.2.3 branch and will run test suite and
   static analysis tooling via Code Climate. If successful, application will be
deployed to the test environment. If not, Release Manager is responsible for
fixing reported errors.
9. Release Manager will assign the Deploy ticket to the Product Owner for
   review.
10. If problems are detected:
  1. The Development Team will make needed code changes on the release branch
  2. Commit and push changes to the remote branch
  3. Write additional tests, if necessary, to cover the problem space detected
  4. Run application test suite and Code Climate to verify all tests and
     analysis tools pass.
11. When Product Owner signs off on release, they will assign to Release
    Manager.

## Production
1. When Product Owner has assigned the Deploy ticket back to the Release
   Manager, the release branch must be finished prior to deployment.
```
git fetch master
git flow release finish 1.2.3
git push
git push --tags
```
2. Release Manager assigns to Operations for Production release.
3. When application is released to Production Operations assigns Deploy ticket
   back to Product Owner for final review.
4. Product Owner can close Deploy ticket is release is acceptable, or assign
   back to Release Manager with noted bugs. In this case either:
  * A hotfix will be created to address a significant bug
  * A new JIRA ticket will be created to address the bug in a future Sprint.
