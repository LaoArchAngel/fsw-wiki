# Current Deployment Procedures and Other Important Information You Didn't Ask For
## Fsw4.0 Repository
### **Websites**

* **Fsw.com(old)**
 * Stage deploys to **FswEcStgOldWeb1** and **FswEcStgOldWeb2**
 * Production deploys to **FswWeb10/11/12** and **FswWeb14/15/16** depending on cluster in service
 * [Fsw.com Build, Package, and Deploy - SNAPSHOT](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution_snapshots/)
 * [Fsw.com Build and Package - RELEASE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution/)
       * [Fsw.com Promotions - DEPLOY TO STAGE & PRODUCTION](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/package_fsw-com_choco_only/)

* **[Fsw.com(archer)](http://gitlab.fsw.com/the-a-team/fsw.com)**
 * Stage deploys to **FswEcArcherStg1** OR **2** depending on cluster group.
 * Prod deploys to **FswEcArcher1/2** OR **FswEcArcher3/4** depending on cluster group.
 * [build_ecomm_archer](http://fswjenkins01:8080/job/build_ecomm_archer/) builds a deployable package version of whatever branch is specified.
 * [deploy_ecomm_archer](http://fswjenkins01:8080/job/deploy_ecomm_archer/) deploys the given version to the specified environment AND cluster.
     * Use [stage status](http://www.stg-fsw.com:9000/status) and [prod status](http://www.fsw.com:9000/status) to determine the current In Service cluster.
     * **NOTE**: Should the deployment hang for an reason, stop the job. You will need to log onto the server/s that the job was attempting to deploy to and kill 7Zip and Chocolatey. For some reason they hang and don't send a response back to Jenkins. Re-running the last job should work after that.
 * [deploy_ecomm_loadbalancer](http://fswjenkins01:8080/job/deploy_ecomm_loadbalancer/) Will put into service whichever cluster/environment is specified.  Note that the first run of this deploy often fails--re-run immediately and it should work.

* **FswAdmin.com**
 * Stage deploys to **STG-FswAdmin1**
 * Production deploys to **FswAdmin1** and **FswAdmin2**
 * [Fsw.com Build, Package, and Deploy - SNAPSHOT](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution_snapshots/)
 * [FswAdmin.com Build and Package - RELEASE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution/)
       * [FswAdmin.com Promotions - DEPLOY TO STAGE & PRODUCTION](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/package_fswadmin-com_choco_only/)


 * Stage deploys to **STG-FswWeb1**
 * Production deploys to **FswWeb1** and **FswWeb2**
 * [Build and Deploy sites - DEPLOY TO STAGE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_deploy_fsw40/)
      * These sites currently deployed to production via Powershell Scripts on FswMulti1

### **Windows Services**

* **SalesForceWindowsService**
* **IncomingTransmissionService**
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
  * Load the _FSW4.0_ solution.
  * Navigate to the _KountEns_ project. (/ThirdParty-ToRemove/Kount/KountEns)
  * Right-click on _KountEns_.
    * Click the _Publish..._ option.
  * Click the _Preview_ tab on the left.
  * Ensure _KountIncoming_ is selected in the drop-down.
  * Click the _Publish_ button.
  * **NOTE:** I do not actually know if these are the most up-to-date instructions.  The person who does left weeks ago.
* **Distribution Services**

 * Stage deploys to **STG-FswSvc1**
 * Production deploys to **FswMulti1**
 * [Build and Deploy Console Apps - STAGE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_deploy_fsw40/)
 * [Build, Publish, and Deploy Console Apps To FswMulti1 - PRODUCTION](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_fsw40_prod/)
        * This job will currently only automatically deploy STP, OcrImport, and NightlyDbUpdates ---- ITS still need test as of 1/28/2016
        * IncomingTransmissionProcessor may still be deployed using the release scripts on FswMulti1


* [**FswEcommProductManagementApi**](http://gitlab.fsw.com/the-a-team/product-management-api)
 * Stage deploys to **FswEcPmStg**
 * Production deploys to **FswEcPm1**
 * [build_ecomm_proudct_management_api](http://fswjenkins01:8080/job/build_ecomm_product_management_api/) Will build a deployable package version of the Api.
 * [deploy_ecomm_product_management_api](http://fswjenkins01:8080/job/deploy_ecomm_product_management_api/) Takes the pervious package version and deploys to specified environment.
     * On deployment, it will try to automatically set a schedule for both Hydration and Popularity. Use a GET on the following to see that they are set, or not.
         * https://ecomm-product-mgmt-api.stg-fsw.com:8457/api/ProductManagement/interval/Hydrator
         * https://ecomm-product-mgmt-api.stg-fsw.com:8457/api/ProductManagement/interval/Popularity
     * Should they not be set, they can be set by adding the following.
         * ?intervalInMinutes=60&runDate=2016-02-22T14:31&overrideInterval=true
     * **NOTE**: After Hydration has started, it is a good idea to watch the logs and ensure it completes at least once. There can be issues with 'out of memory' exceptions.


* [**FswEcommPageManagementApi**](http://gitlab.fsw.com/the-a-team/page-management-api)
 * Stage deploys to **FswEcPmStg**
 * Production deploys to **FswEcPm1**
 * [build_ecomm_page_management_api](http://fswjenkins01:8080/job/build_ecomm_page_mgmt_api/) Will build a deployable package version of the Api.
 * [deploy_ecomm_page_management_api](http://fswjenkins01:8080/job/deploy_ecomm_page_management_api/) Takes the pervious package version and deploys to specified environment.
     * On deployment, it will try to automatically set a schedule for both RefreshIndex and Popularity. Use a GET on the following to see that they are set, or not.
         * https://ecomm-product-mgmt-api.stg-fsw.com:9457/api/PageManagement/interval/RefreshIndex
         * https://ecomm-product-mgmt-api.stg-fsw.com:9457/api/PageManagement/interval/Popularity
     * Should they not be set, they can be set by adding the following.
         * ?intervalInMinutes=60&runDate=2016-02-22T14:31&overrideInterval=true


* [**FswEcommElasticSearch**](http://gitlab.fsw.com/the-a-team/page-management-api)
 * Dev deploys to **FswEcEsDev1**,**FswEcEsDev2**, and **FswEcEsDev3**
 * Stage deploys to **FswEcEsStg1**,**FswEcEsStg2**, and **FswEcEsStg3**
 * Production deploys to **FswEcEsProd1**,**FswEcEsProd2**, and **FswEcEsProd3**
 * [deploy_ecomm_elasticsearch](http://fswjenkins01:8080/job/deploy_ecomm_elasticsearch/) Deploys the fsw.elasticsearch repo along with index mapping changes from ecomm-elasticsearch-indexmappings
     * This includes setting up the cluster for elasticsearch itself


* [**FswEcommImageApi(ImageCopy)**](http://gitlab.fsw.com/the-a-team/image-service)
 * This is also a non-deployable for most apps but there is an api located in the same repo for the imagecopy(imageApi).
 * [build_ecomm_page_management_api](http://fswjenkins01:8080/job/build_ecomm_page_management_api/) Will build a deployable package version of the Api.
 * [build_ecomm_image_service](http://fswjenkins01:8080/job/build_ecomm_image_service/) Will build a deployable package version of the service.
 * [deploy_ecomm_imagecopy](http://fswjenkins01:8080/job/deploy_ecomm_imagecopy/)
 * Dev deploys to **FswEcImgApiStg**
 * Stage deploys to **FswEcImgApiStg**
 * Production deploys to **FswEcImageApi1**   


* [**FswEcommSiteMapApi**](http://gitlab.fsw.com/the-a-team/sitemap)
 * The image service is also a non-deployable for most apps but there is an api located in the same repo for the sitemap api.
 * [build_ecomm_sitemap](http://fswjenkins01:8080/job/build_ecomm_sitemap/) Will build a deployable package version of the service.
 * [deploy_ecomm_sitemap](http://fswjenkins01:8080/job/deploy_ecomm_sitemap/)
 * Dev deploys to **FswEcSiteMapDev**
 * Stage deploys to **FswEcSiteMapStg**
 * Production deploys to **FswEcSiteMap1**

### **Core Components & Applications**

 * [**Ansible**](http://fswjenkins01:8080/computer/)
  * FswAnsibleMaster01 - v1.9-beta (10.0.49.6)
  * FswAnsibleMaster03 - v1.9.2 (10.0.49.7)
  * FSWAnsibleMasterProd (10.0.50.85)
 * [**Jenkins**](http://fswjenkins01:8080/)
 * **SQL** - Main FSW DB
  * Dev - fswdev3
  * Stage - fswstg3
  * Prod - fswdb
 * **Mongo**
  * Dev - FSWDEVMongo:30000,FSWDEVMongo:40000,FSWDEVMongo:50000
  * Stage - FSWStgMongo:30000,FSWStgMongo:40000,FSWStgMongo:50000
  * Prod - FSWmongo01.foodservicewarehouse.com:30000,FSWmongo02.foodservicewarehouse.com,FSWmongo03.foodservicewarehouse.com
 * **Accellos**
 * [**GitLab**](http://gitlab.fsw.com/)
  * To access the GitLab server via ssh, you will need the fswadmin public and
  private key. [Public Key](http://gitlab.fsw.com/tfs/library/raw/master/ssh/fswadmin_ssh.pub) / [Private Key](http://gitlab.fsw.com/tfs/library/raw/master/ssh/fswadmin_ssh)
  * To ssh into GitLab, use the following command:
    ```bash
    ssh fswadmin@gitlab.fsw.com -i path/to/fswadmin_ssh
    ```
  * The GitLab server is hosted as a VM.  Moving the repositories should be done by moving the VM.
  * If moving the server VM is not possible, it is possible to clone any desired repositories and then push them to a new host.
 * [**ProGet**](http://proget.fsw.com/)
 * [**Gator**](http://gator.fsw.com:9000/)

### **Non-Deployables**
None of the following are deployed, but they do use a Jenkins job to build a useable packaged. Packages are pushed up to ProGet.
* **eComm.ProductService**
 * [build_ecomm_product_service](http://fswjenkins01:8080/job/build_ecomm_product_service/)
* **eComm.PageService**
 * [build_ecomm_page_service](http://fswjenkins01:8080/job/build_ecomm_page_service/)
* **eComm.SchedulerService**
 * [build_ecomm_scheduler_service](http://fswjenkins01:8080/job/build_ecomm_scheduler_service/)
* **eComm.RedirectService**
* **eComm.ImageService**
* **eComm.CartService**
* **eComm.LeadAggregationService**
