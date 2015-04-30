# Configuration Package

**TBD: These notes are still a work in progress.**

To add/update/etc. configuration settings in the FSW Configuration project, follow the steps below.

1. Create the script to add/update/etc. configuration settings (DB tables `config.ConfigurationKey`, `config.ConfigurationValue`).

2. Be sure that the script passes the QA process as defined by your development team.

3. Send the script to @jvandyke by adding it to the Asana project for SQL scripts:
[Change Log: SQL](https://app.asana.com/0/30603980759983/30603980759983)

4. Make the changes to the Configuration solution in the GitLab Configuration repository.
	- If needed, clone the repository from: http://gitlab.fsw.com/tfs/Configuration.git
	- Create a topic branch.
	- Make the change to the topic branch.
	- Push the topic branch to origin on GitLab.
	- Create a merge request from the topic branch to master: http://gitlab.fsw.com/tfs/Configuration/merge_requests

5. (**TBD: Will this next step automatically run upon merge to master?**) **After** @jvandyke runs the script, **after** the merge request is approved, and **after** the Configuration code is merged to master in the GitLab Configuration repository, run the Jenkins project to deploy the latest package to ProGet:
http://fswjenkins01:8080/view/Builds/job/build_fsw_configuration/
	- Click: `Build With Parameters`
	- Set `Create_Packages` to `YES`
	- Set `branch` to `refs/heads/master`
	- Click: `Build`!
	
6. Get the version number of the updated Configuration package from ProGet:
http://proget.fsw.com/feeds/Default/Configuration
	- This page will automatically redirect to the Configuration package page with the latest version number.
	- The version number will be in the format: `1.0.xxxx.yyyyy`
	- The `Last Updated` date and time should be the same date and time when the Jenkins project was run.

7. Create a topic branch in the main FswGit repository as usual for doing normal development work.

8. In the FswGit topic branch, in the Fsw4.0 solution, update the Configuration package version in each project that uses the added/updated configuration settings:
	- The project file to edit is `packages.config`.
	- Change the setting element for `package id="Configuration"` to the following: `<package id="Configuration" version="1.0.xxx.yyyyy" targetFramework="net45" />`
	where `1.0.xxxx.yyyyy` is the new version number of the Configuration package.

9. Be sure that the solution successfully builds with the added/updated configuration settings as referenced.

10. Commit the development work along with the Configuration package version changes, and submit a merge request as usual for doing development work.  Include @mmcgregor as a required reviewer.

