# Current Deployment Procedures
## Fsw4.0 Repository
### **Websites**

* **Fsw.com**
 * [Fsw.com Build, Package, and Deploy - SNAPSHOT](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution_snapshots/)
 * [Fsw.com Build and Package - RELEASE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution/)
       * [Fsw.com Promotions - DEPLOY TO STAGE & PRODUCTION](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/package_fsw-com_choco_only/)


* **FswAdmin.com**
 * [Fsw.com Build, Package, and Deploy - SNAPSHOT](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution_snapshots/)
 * [FswAdmin.com Build and Package - RELEASE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution/)
       * [FswAdmin.com Promotions - DEPLOY TO STAGE & PRODUCTION](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/package_fswadmin-com_choco_only/)


#### **Other websites:**
* **IppBuy.com**
* **FswOrderup.com**
* **PartnerPortal**
* **Reporting**

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

 * [Build and Deploy Windows Services - DEPLOY TO STAGE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_deploy_fsw40/)
      * These windows services currently deployed to production via Powershell Scripts on FswMulti1

### **Console Applications and Other**

* **OcrImport**
* **NightlyDbUpdates**
* **ScheduledTransmissionProcessor**
* **KountIncoming**

 * [Build and Deploy Console Apps - STAGE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_deploy_fsw40/)
 * [Build and Publish Console Apps To FswMulti1 - PRODUCTION](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_fsw40_prod/)
        * These applications currently deployed to production via Powershell Scripts on FswMulti1