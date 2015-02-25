# Automated Releases

## Technologies

* [Git](http://gitlab.fsw.com/)
* [Jenkins](http://fswjenkins01.foodservicewarehouse.com:8080/)
* [Ansible](http://gitlab.fsw.com/architecture/fsw-ansible)
* [Gator](http://fswjenkins01:8080/view/utility/job/build_gator/) -> [git repo](http://gitlab.fsw.com/architecture/gator)
* [NuGet](http://proget.fsw.com/)
* [Chocolatey](http://proget.fsw.com/)

## Release Workflow Flow

A [visio diagram](http://sp.foodservicewarehouse.com/Development/EngineeringStandards/Release_Flow.vsdx) of the release flow can be found [here](http://sp.foodservicewarehouse.com/Development/EngineeringStandards/Release_Flow.vsdx)

![release workflow diagram](http://sp.foodservicewarehouse.com/Development/EngineeringStandards/Release_Flow.png)

## Branching Strategy

* master
    * All code entering this branch should be reviewed and merged using gitlab's merge request feature.  Any code merged into this branch should be considered production `ready`, but not necessarily production 'deployed'. This branch will be automatically built (and unit tests run) by the build server and deployed to the `dev` environment any time new code is committed.
* topic|feature|bugfix/*
    * A branch should be created per user story (bugfix, feature, etc) from master.  This branch should rarely be a shared branch (if ever) and should be considered independently deploy-able. This branch will be automatically built (and unit tests run) by the build server.  The built package produced by the build job for this branch can be deployed to the dev environment upon request, but it will not be done automatically.

