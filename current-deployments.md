# Current Deployment Procedures and Other Important Information You Didn't Ask For
## Fsw4.0 Repository
### **Websites**

* **Fsw.com(old)**
 * Stage deploys to **FswEcStgOldWeb1** and **FswEcStgOldWeb2**
 * Production deploys to **FswWeb10/11/12** and **FswWeb14/15/16** depending on cluster in service
 * [Fsw.com Build, Package, and Deploy - SNAPSHOT](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution_snapshots/)
 * [Fsw.com Build and Package - RELEASE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution/)
       * [Fsw.com Promotions - DEPLOY TO STAGE & PRODUCTION](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/package_fsw-com_choco_only/)

* **Fsw.com(archer)**
 * [Code] (http://gitlab.fsw.com/the-a-team/fsw.com)
 * Stage deploys to **FswEcArcherStg1** OR **2** depending on cluster group.
 * Prod deploys to **FswEcArcher1/2** OR **FswEcArcher3/4** depending on cluster group.
 * [build_ecomm_archer](http://fswjenkins01:8080/job/build_ecomm_archer/) builds a deployable package version of whatever branch is specified.
 * [deploy_ecomm_archer](http://fswjenkins01:8080/job/deploy_ecomm_archer/) deploys the given version to the specified environment AND cluster.
     * Use [stage status](http://www.stg-fsw.com:9000/status) and [prod status](http://www.fsw.com:9000/status) to determine the current In Service cluster.
     * **NOTE**: Should the deployment hang for an reason, stop the job. You will need to log onto the server/s that the job was attempting to deploy to and kill 7Zip and Chocolatey. For some reason they hang and don't send a response back to Jenkins. Re-running the last job should work after that.
 * [deploy_ecomm_loadbalancer](http://fswjenkins01:8080/job/deploy_ecomm_loadbalancer/) Will put into service whichever cluster/environment is specified.

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
 * [Build, Publish, and Deploy Console Apps To FswMulti1 - PRODUCTION](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_fsw40_prod/)
        * This job will currently only automatically deploy STP, OcrImport, and NightlyDbUpdates ---- ITS still need test as of 1/28/2016
        * IncomingTransmissionProcessor may still be deployed using the release scripts on FswMulti1
* **FswEcommProductManagementApi**
 * Stage deploys to **FswEcPmStg**
 * Production deploys to **FswEcPm1**
 * [build_ecomm_proudct_management_api](http://fswjenkins01:8080/job/build_ecomm_product_management_api/) Will build a deployable package version of the Api.
 * [deploy_ecomm_product_management_api]() Takes the pervious package version and deploys to specified environment.
     * On deployment, it will try to automatically set a schedule for both Hydration and Popularity. Use a GET on the following to see that they are set, or not.
         * https://ecomm-product-mgmt-api.stg-fsw.com:8457/api/ProductManagement/interval/Hydrator
         * https://ecomm-product-mgmt-api.stg-fsw.com:8457/api/ProductManagement/interval/Popularity
     * Should they not be set, they can be set by adding the following.
         * ?intervalInMinutes=60&runDate=2016-02-22T14:31&overrideInterval=true
     * **NOTE**: After Hydration has started, it is a good idea to watch the logs and ensure it completes at least once. There can be issues with 'out of memory' exceptions.