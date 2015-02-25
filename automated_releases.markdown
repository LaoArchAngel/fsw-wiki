# Automated Releases

## Technologies

* [Git](http://gitlab.fsw.com/)
* [Jenkins](http://fswjenkins01.foodservicewarehouse.com:8080/)
* [Ansible](http://gitlab.fsw.com/architecture/fsw-ansible)
* [Gator](http://fswjenkins01:8080/view/utility/job/build_gator/) -> [git repo](http://gitlab.fsw.com/architecture/gator)
* [NuGet](http://proget.fsw.com/)
* [Chocolatey](http://proget.fsw.com/)

## Branching Strategy

* master
    * All code entering this branch should be reviewed and merged using gitlab's merge request feature.  Any code merged into this branch should be considered production `ready`, but not necessarily production 'deployed'. This branch will be automatically built (and unit tests run) by the build server and deployed to the `dev` environment any time new code is committed.
* topic|feature|bugfix/* (ex: feature/detect-user-agent)
    * A branch should be created per user story (bugfix, feature, etc) from master.  This branch should rarely be a shared branch (if ever) and should be considered independently deploy-able. This branch will be automatically built (and unit tests run) by the build server.  The built package produced by the build job for this branch can be deployed to the dev environment upon request, but it will not be done automatically.

## Release Workflow Flow

A [visio diagram](http://sp.foodservicewarehouse.com/Development/EngineeringStandards/Release_Flow.vsdx) of the release flow can be found [here](http://sp.foodservicewarehouse.com/Development/EngineeringStandards/Release_Flow.vsdx)

![release workflow diagram](http://sp.foodservicewarehouse.com/Development/EngineeringStandards/Release_Flow.png)

## Jenkins Build Jobs

A Jenkins build job should be expected to always produce one package.  The package could be a Nuget package (in the case of .net assemblies) a Chocolatey package (in the case of a windows application); a module (in the case of javascript or node.js); a yum package (in the case of a centos application).  A build job should, at minimum, include the following steps:
    1. build
    2. unit test
    3. package

There should be 2 types of builds: 
* snapshot builds 
    * builds run against topic|feature|bugfix branches
* release builds
    * builds run against the master branch

#### Build Promotions

Builds can be *promoted* for deployment specific environments. Snapshot builds cannot only be promoted for deployment to dev/qa environments (or the earliest suitable integration testing environment).  Snapshot builds cannot be promoted for deployment to Production. Release builds can be promoted to any environment and are expected to follow the flow dev/qa --> stage --> prod.  A release build should never skip an environment.

In Jenkins, we accomplish build promotions using the [Promoted Builds Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Promoted+Builds+Plugin). The Promoted Builds plugin allows you to distinguish good builds from bad builds by introducing the notion of 'promotion'.Put simply, a promoted build is a successful build that passed additional criteria (such as more comprehensive tests that are set up as downstream jobs.) The typical situation in which you use promotion is where you have multiple 'test' jobs hooked up as downstream jobs of a 'build' job. You'll then configure the build job so that the build gets promoted when all the test jobs passed successfully. This allows you to keep the build job run fast (so that developers get faster feedback when a build fails), and you can still distinguish builds that are good from builds that compiled but had runtime problems.

Another variation of this usage is to manually promote builds (based on instinct or something else that runs outside Jenkins.) Promoted builds will get a star in the build history view, and it can be then picked up by other teams, deployed to the staging area, etc., as those builds have passed additional quality criteria. In more complicated scenarios, one can set up multiple levels of promotions. This fits nicely in an environment where there are multiple stages of testings (for example, QA testing, acceptance testing, staging, and production.)

### Jenkins Release Flow Pipeline

Where a particular build is in its release path can be tracked and viewed using the [Delivery Pipeline Plugin] (https://wiki.jenkins-ci.org/display/JENKINS/Delivery+Pipeline+Plugin).
![Example Delivery Pipeline](https://wiki.jenkins-ci.org/download/attachments/69764097/screenshot2.png?version=1&modificationDate=1400172472000)

### TODO: The rest of this document