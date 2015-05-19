# Nuget Specifications & Workflow

This document will outline all of the terms, requirements and workflows in order
to work with the FSW nuget feeds. Each pillar will have their own nuget feed.
Furthermore, a default nuget feed will exist for any and all shared libraries
and components.  With the start of SOA, libraries will be shared less and less
in favor for independently published services.

## Definitions:

### Release Package / Package
Package that has been built from the master branch and is ready for production.  Apart from the Fsw4.0 solution, release packages cannot be created from a commit that does not already have a Pre-Release package.  Release packages can only depend on other release packages (third-party pre-release approvable).

### Pre-Release Package
Package that has been built from master or a release branch depending on the structure of the repository.  These packages will later be recreated from the exact same build as release packages.  Pre-release packages can only reference release packages.

### Snapshot Package
A nuget pre-release package that is tagged with the branch name or other specifier that is meant to be used for testing purposes only. Snapshot packages will not become pre-release or release packages.  Snapshot packages should be cleaned out when then branch is merged into master.

## Nuget Feeds
### Default
Contains packages that are meant to be shared between pillars.  This includes the overarching FSW 4.0 solution packages.  Pre-release packages can be here, but no snapshots.

### Team Feeds
* Release Packages
  * Contains production-ready packages from the pillar.
* Pre-Release Packages
  * Packages meant for internal testing and promotion for projects that belong to the pillar.
* Snapshot Packages
  * Can be created from projects that do not belong to the pillar.
  * Used only for testing purposes.
  * Snapshot packages should never be referenced by any non-snapshot.
  * Snapshot packages can be referenced by branches that are not being compiled into packages.
  * Snapshot packages and their consuming applications should be used and tested by developers only to reduce redundant testing of the same features by QA.

## Team Feed Package Workflow
1. Do work on topic branch.
* Create snapshot packages from topic branch if necessary.
  * Go to Jenkins build job for snapshot packages for your project.
  * Give Jenkins job parameter appropriate name for the snapshot.  “Pre” is not a valid snapshot name as it is used for pre-release packages.
  * Build job.
  * Nuget snapshot package will be uploaded to the team feed.
* Test applications that rely on snapshot package on a topic branch.
  * Using Package Manager Console in Visual Studio, update the package to the snapshot package.  Assuming project name is **ProjectAlpha** & Package name is **MyPackage**, and snapshot name is **MyBranch**:
  * `Update-Package -Version 1.0.0.0-MyBranch -ProjectName ProjectAlpha MyPackage`
  * The version number of a snapshot package can increase, but keep the snapshot name the same to indicate progression in testing.
  * If changes need to be made to the snapshot package, return to step 1.
* When the branch has passed dev & unit tests, the branch can be merged into master.
* Once the branch is merged, a pre-release nuget package will be created by the automatic build server.
* Test applications that rely on the pre-release package on the topic branch from step 3
  * Any applications currently using a snapshot package in a branch should be updated to the pre-release package.
  * Feature testing by QA should now be started on the dependent applications.
  * If changes to the pre-release package are necessary, there are a couple of possible workflows.
    1. If necessary changes are minor, create a fix branch from the pre-release commit, fix the code, and re-merge into master to generate a new pre-release package.
    * If changes are larger, abandon the pre-release package and continue work on a new branch and snapshot series.  The pre-release package will not be promoted to release and the version will never be referenced by an application.
* Once the pre-release package has been approved by QA feature testing, the package can be promoted to a release package.
  * Go to Jenkins build job for package promotion of your repository.
  * Build job.
  * Nuget release package will be uploaded to the team feed.
* Update all dependent applications to the release package, merge topic branches into master and perform regression testing for the application as a whole.
* Any future changes to the package will be considered new branches as either features or bug fixes.  The life-cycle of this release has ended at this point.

## Shared (Default) Package Workflow
1. Do work on topic branch.
* Create snapshot packages from topic branch if necessary.
  * Go to Jenkins build job for snapshot packages for the shared project for your team’s nuget feed.
  * Example build job: `package_SharedProjectAlpha_TeamA_Snapshot`
  * Give Jenkins job parameter appropriate name for the snapshot.  "Pre" is not a valid snapshot name as it is used for pre-release packages.
  * Build job.
  * Nuget snapshot package will be uploaded to the team feed.
* Test applications that rely on snapshot package in a topic branch.
  * Using Package Manager Console in Visual Studio, update the package to the snapshot package.  Assuming project name is **ProjectAlpha** & Package name is **MyPackage**, and snapshot name is **MyBranch**:
  * `Update-Package -Version 1.0.0.0-MyBranch -ProjectName ProjectAlpha MyPackage`
  * The version number of a snapshot package can increase, but keep the snapshot name the same to indicate progression in testing.
  * If changes need to be made to the snapshot package, return to step 1.
* When the branch in the shared library has passed dev & unit tests, the branch can be merged into __master__ (or __develop__, in the FSW 4.0 solution.)
* When a release branch is cut from the shared library, a pre-release package will be created.
* Test applications that rely on the pre-release package on the topic branch from step 3.
  * Any applications currently using a snapshot package in a branch should be updated to the pre-release package.
  * Updating this type of package will require uninstalling the package and re-installing from the Default nuget feed.
  * Feature testing by QA should now be performed on the dependent applications.
  * If changes to the pre-release package are necessary, changes should be made on the release branch as per the Release Manager's instructions.  If the changes made by the topic branch do not make the release because they had to be reverted, then work should continue on a new topic branch and return step 1.
* Once the release branch has been merged into master, release packages will be created to replace the pre-release packages.
* Update all dependent applications to the release package, merge topic branches into master and perform regression testing for the application as a whole.
* Any future changes to the package will be considered new branches as either features or bug fixes.  The life-cycle of this release has ended at this point.
