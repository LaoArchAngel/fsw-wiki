# Deploying database changes

This document goes over the steps of making FswDB changes and deploying them
to production.

## Overview

1. Create FswDB branch.
* Apply changes to FswDB branch.
* Apply changes to Dev
* Generate script
* Get QA approval (testing in stage).
* Deploy changes to production.

## Procedure

### FswDb project branches

There are two types of changes that may require a branch of FswDB:

1. Schema changes (Only allowed to add columns - no renames or drops)
* Stored Procedure/Function modifications


### Branching and testing steps:

1. Pull latest version of master from the FswDB repository.
* Create branch from master
* Apply changes to branch
* Push your changes from FswDB project on the branch to fswdev3.fsw database
* Compare branch with FswStg database
* Generate script that will update FswStg database with ONLY YOUR changes
 * If other items appear in comparison, ignore them when generating the script
* Commit script to branch under either Post-Release or Pre-Release folder
* Submit merge request of branch into master via GitLab
 * QA pulls branch
 * QA runs script against test database
 * QA approves branch
 * Branch is merged
* Script may then be added to the [Change Log: SQL asana project](https://app.asana.com/0/30603980759983/list) and run in production


#### See Also

* [FswDB project in GitLab](http://gitlab.fsw.com/tfs/FswDB)
* [Clean Local Git Repository][2]
* [Database Change Overview](../../database/changeOverview)
* [Data Tier Regeneration Branches][1]
* [Linq2Sql Data Tier Regeneration][3]


[1]: ../../../git/branching/dataTierRegen
[2]: ../../../git/cleanRepo
[3]: ../linq2sql/regen
