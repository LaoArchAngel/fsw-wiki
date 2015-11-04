# Deploying database changes

This document goes over the steps of making FswDB changes and deploying them
to production.

## Overview

1. Create FswDB branch.
* Apply changes to FswDB branch.
* Generate script for dev/stage/production
* Get QA approval (testing in stage).
* Apply changes to fswdev3.fsw database
* Deploy changes to production.

## Procedure

### FswDb project branches

There are two types of changes that may require a branch of FswDB:

1. Schema changes (Only allowed to add columns - no renames or drops)
* Stored Procedure/Function modifications


### Branching and testing steps:

1. Pull latest version of master from the [FswDB repository](http://gitlab.fsw.com/tfs/FswDB).
2. Create branch from master
3. Apply changes to branch
4. Compare branch with FswStg3.FswStg database
5. Generate script that will update FswStg3.FswStg database with ONLY YOUR changes
 * To generate a script containing only your changes, open the StgCompare.scmp file in Visual Studio:  

  ![fswdb1](http://gitlab.fsw.com/tfs/library/uploads/b1fdd3f41610fcc900c822382c406b4b/fswdb1.PNG)  

 * The comparison should be from the FswDB project to the FswStg3.FswStg database:  

  ![fswdb2](http://gitlab.fsw.com/tfs/library/uploads/eed1784e14bbd17744ad1a5d4d87f522/fswdb2.PNG)     

 * Click the compare button
 * Identify and select ONLY YOUR changes from the list:  

  ![fswdb3](http://gitlab.fsw.com/tfs/library/uploads/11ba9e1e2044375f9aaf5e52c7ab896b/fswdb3.PNG)  

 * With only your changes selected, click the "Generate Script" button:  

  ![fswdb4](http://gitlab.fsw.com/tfs/library/uploads/7f56a2ed12b5d779c366f8537a0170ad/fswdb4.PNG)  

 * The generated script will open inside of a window in Visual Studio with some default settings:  

  ![fswdb5](http://gitlab.fsw.com/tfs/library/uploads/fa70783090d29aded8d4b53f7d9c44b2/fswdb5.PNG)  

 * Everything up to the USE statement may be safely removed:  

  ![fswdb6](http://gitlab.fsw.com/tfs/library/uploads/1dde359d05cb7f6e35d08e5d02a8a9ea/fswdb6.PNG)  

 * The USE statement(s) should then be changed to use the "Fsw" database:  

  ![fswdb7](http://gitlab.fsw.com/tfs/library/uploads/e43708018698bf1d9b61188d55f85581/fswdb7.PNG)  

 * Save the file locally

6. In your branch, delete any existing scripts in the _ReleaseScripts folder
7. Commit newly created script to _ReleaseScripts folder in branch
8. Push branch to origin
9. Submit merge request of branch into master via GitLab
 * QA pulls branch
 * QA runs script against one of the test databases (FswMoon, FswMars, FswVenus, FswSaturn, FswMercury)
 * QA runs script against FswStg3.FswStg database and performs any regression testing, if necessary
 * QA approves branch
 * Branch is merged
10. Run your script against the FswDev3.Fsw database
 * The comparison can be run against FswDev3.Fsw to confirm there is no drift between FswDB master and that database
 * If there are differences between the FswDev3.Fsw database and the master branch, and email should be sent to the Dev department to find out who owns those changes
11. [Update the schema of the local "unit test" database](http://gitlab.fsw.com/tfs/library/wikis/Testing/TestDatabase#updating-the-schema).  This is mostly important if the database changes affected table schemas (contrasted with stored procs and other DB objects).
12. Script may then be added to the [Change Log: SQL asana project](https://app.asana.com/0/30603980759983/list) and run in production by DBA



#### See Also

* [FswDB project in GitLab](http://gitlab.fsw.com/tfs/FswDB)
* [Regenerating Entity Framework Data Tiers](http://gitlab.fsw.com/tfs/library/wikis/data/datatiers/entityFramework/regen)
