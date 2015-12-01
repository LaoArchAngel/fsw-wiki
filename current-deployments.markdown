# Current Deployment Procedures and Other Important Information You Didn't Ask For
## Fsw4.0 Repository
### **Websites**

* **Fsw.com**
 * Stage deploys to **FswEcStgOldWeb1** and **FswEcStgOldWeb2**
 * Production deploys to **FswWeb10/11/12** and **FswWeb14/15/16** depending on cluster in service
 * [Fsw.com Build, Package, and Deploy - SNAPSHOT](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution_snapshots/)
 * [Fsw.com Build and Package - RELEASE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution/)
       * [Fsw.com Promotions - DEPLOY TO STAGE & PRODUCTION](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/package_fsw-com_choco_only/)


* **FswAdmin.com**
 * Stage deploys to **STG-FswAdmin1**
 * Production deploys to **FswAdmin1** and **FswAdmin2**
 * [Fsw.com Build, Package, and Deploy - SNAPSHOT](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution_snapshots/)
 * [FswAdmin.com Build and Package - RELEASE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution/)
       * [FswAdmin.com Promotions - DEPLOY TO STAGE & PRODUCTION](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/package_fswadmin-com_choco_only/)


#### **Other websites:**
* **IppBuy.com**
* **FswOrderup.com**
* **PartnerPortal**
* **Reporting**

 * Stage deploys to **STG-FswWeb1**
 * Production deploys to **FswWeb1** and **FswWeb2**
 * [Build and Deploy sites - DEPLOY TO STAGE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_deploy_fsw40/)
      * These sites currently deployed to production via Powershell Scripts on FswMulti1

### **Windows Services**

* **AsyncUpdateWindowsService**
* **SalesForceWindowsService**
* **IncomingTransmissionService**
* **SolrWindowsService**
* **WinnowingWindowsService**
* **AsyncQueueConsumer**
* **CartConsumerService**
* **TransmissionConsumerService**

 * Stage deploys to **STG-FswSvc1**
 * Production deploys to **FswSvc2/3/4** (The number of instances will depend on the app)
 * [Build and Deploy Windows Services - DEPLOY TO STAGE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_deploy_fsw40/)
      * These windows services currently deployed to production via Powershell Scripts on FswMulti1

### **Console Applications and Other**

* **OcrImport**
* **NightlyDbUpdates**
* **ScheduledTransmissionProcessor**
* **KountIncoming**

 * Stage deploys to **STG-FswSvc1**
 * Production deploys to **FswMulti1**
 * [Build and Deploy Console Apps - STAGE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_deploy_fsw40/)
 * [Build and Publish Console Apps To FswMulti1 - PRODUCTION](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_fsw40_prod/)
        * These applications currently deployed to production via Powershell Scripts on FswMulti1