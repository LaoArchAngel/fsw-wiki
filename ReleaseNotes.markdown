### Revisions
| Date | Editor | Changes |
| -------- | -------- | -------- |
|2015-02-06|Clyde Latham|added release for 2015_02_05|
|2015-02-09|Clyde Latham|added release for 2015_02_10|
|2015-02-11|Clyde Latham|added release for 2015_02_12|

# Stage Deployment History
___

>> # __2015_02_12__

### __The following projects have been published to stage and are ready for release testing:__
- FSWAdmin
- FSW.com
- ASyncQueueConsumer

#### __Notes__
- origin/hotfix/27908-EclipsePayments merged into release branch and republished

### __The following scripts have been run against FswStg:__

#### __Pre Release:__
- 27548 – Danny Su – Add MS Division and Clean up old MS.sql
- Danny Su – Update the Non-Taxable Adjustment Code.sql
- 2015_02_12_FswStg_Update1.publish

#### __Post Release__
- Just run the two scripts for the stored procedure and function or run schema compare to add them.
Have JVD setup a job to have stored procedure run every day and email Patricia Sparrow

### __The following work items are slated for release:__
#### __Killer Owls Team:__
* Bug 27908:Eclipse: Orders with entity id 0 on orders.payment blow up on the order review page

http://fswtfs3:8080/tfs/DefaultCollection/FswGit/_workitems#_a=edit&id=27908

http://gitlab.fsw.com/tfs/fswgit/merge_requests/108

#### __Ecomm Team:__
* Bug 27882:Admin : Pollywog - Adjusts Item Sell Price on completion, even if caught with unmatched items

http://fswtfs3:8080/tfs/DefaultCollection/FswGit/_workitems#_a=edit&id=27882

http://gitlab.fsw.com/tfs/fswgit/merge_requests/99

* Product Backlog Item 27846:**Ops/Accounting - Avalara - Expiring tax codes need fixed

http://fswtfs3:8080/tfs/DefaultCollection/FswGit/_workitems#_a=edit&id=27846

http://gitlab.fsw.com/tfs/fswgit/merge_requests/112

* Product Backlog Item 27762:Customer Service - Remove code to populate fulfillment partner names if internal FSW employees

http://fswtfs3:8080/tfs/DefaultCollection/FswGit/_workitems#_a=edit&id=27762

http://gitlab.fsw.com/tfs/fswgit/merge_requests/110

* Bug 27867:Accellos/Admin : PO's in Accellos Not Updating PO in Admin

http://fswtfs3:8080/tfs/DefaultCollection/FswGit/_workitems#_a=edit&id=27867

http://gitlab.fsw.com/tfs/fswgit/merge_requests/105

* Product Backlog Item 27333:Fulfillment - Automated Metrics

http://fswtfs3:8080/tfs/DefaultCollection/FswGit/_workitems#_a=edit&id=27333

http://gitlab.fsw.com/tfs/fswgit/merge_requests/77

* Product Backlog Item 27548:M&A - Switch MarketSource parent business division to M&A not Licensing

http://fswtfs3:8080/tfs/DefaultCollection/FswGit/_workitems#_a=edit&id=27548

http://gitlab.fsw.com/tfs/fswgit/merge_requests/69

#### __Fsw.com Team:__
* Product Backlog Item 27904:Changes to Top Brands

http://fswtfs3:8080/tfs/DefaultCollection/FswGit/_workitems#_a=edit&id=27904

http://gitlab.fsw.com/tfs/fswgit/merge_requests/100

#### __IppBuy.com Team:__
* N/A

___
