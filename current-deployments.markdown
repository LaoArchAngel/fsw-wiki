# Current Deployment Procedures
## Fsw4.0 Repository
### **Larger Sites**

* **Fsw.com**
 * [Fsw.com Build and Package Job](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution/)
 * [Fsw.com Promotions - STAGE & PRODUCTION](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/package_fsw-com_choco_only/)


* **FswAdmin.com**
 * [FswAdmin.com Build and Package Job](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution/)
 * [FswAdmin.com Promotions - STAGE & PRODUCTION](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/package_fswadmin-com_choco_only/)


### **Smaller Sites**

* **IppBuy.com**
* **FswOrderup.com**
* **PartnerPortal**
* **Reporting**

 * [Build and Deploy sites - STAGE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_deploy_fsw40/)
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

 * [Build and Deploy Windows Services - STAGE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_deploy_fsw40/)
      * These windows services currently deployed to production via Powershell Scripts on FswMulti1

### **Console Applications and Other**

* **OcrImport**
* **NightlyDbUpdates**
* **ScheduledTransmissionProcessor**
* **KountIncoming**

 * [Build and Deploy Console Apps - STAGE](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_deploy_fsw40/)
 * [Build and Publish To FswMulti1 - PRODUCTION](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_fsw40_prod/)
        * These applications currently deployed to production via Powershell Scripts on FswMulti1