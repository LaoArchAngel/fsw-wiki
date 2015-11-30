# Current Deployment Procedures
## Fsw4.0 Repository
### **Larger Sites**

* **Fsw.com**
* **FswAdmin.com**

Build Jobs (Create packages from here):
* [Fsw.com Build Job](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution/)
* [FswAdmin.com Build Job](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_fsw_solution/)

Promotion Jobs (Promote packages across all environments, including production, from here):
* [Fsw.com Promotions](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/package_fsw-com_choco_only/)
* [FswAdmin.com Promotions](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/package_fswadmin-com_choco_only/)

### **Smaller Sites**

* **IppBuy.com**
* **FswOrderup.com**
* **PartnerPortal**
* **Reporting**

Build and Deploy Job (To STAGE Only):
* [IppBuy, FswOrderup, PartnerPortal, Reporting build job](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_deploy_fsw40/)
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

Build and Deploy Job (To STAGE Only):
* [Windows Services build job](http://fswjenkins01:8080/view/Fsw4.0%20Deployment%20Jobs/job/build_publish_deploy_fsw40/)
 * These windows services currently deployed to production via Powershell Scripts on FswMulti1




