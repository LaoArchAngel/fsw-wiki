## FSW ProGet
ProGet is a package management server that enables us to set up feeds for Nuget, Chocolatey, NPM, and Bower. We will be using at least the first two of these feeds. The Nuget feed also includes a symbol and source server, so we can publish packages with symbols and source code, allowing us to step into code from packages we consume from the feed.

### Web Interface
ProGet has a web interface available at [proget.fsw.com](http://proget.fsw.com). This interface will allow you to browse, search, and add both stable and prerelease versions of packages. 

### Feeds
The ProGet service contains the following feeds:

* [Default](http://proget.fsw.com/feeds/Default) (Nuget) 
* Chocolatey coming soon.
* NPM, Bower under evaluation.

### Visual Studio 2013 Setup
To make Visual Studio search the ProGet Nuget feed for packages, follow these
steps:

1. Go to **Tools > Nuget Package Manager > Package Manager Settings**.  This
should open an **Options** window open to the **Nuget Package Manager** section.
2. In the list on the left, select **Package Sources**.
3. In the main pane you should see one or two sources.  One will be the official
nuget feed, _nuget.org_.  If your or someone else had added the FSW ProGet package feed
, that should also be visible, although less likely.  If you only see
_nuget.org_, follow the instructions under **Add New Source**.  Otherwise,
follow instructions under **Update Existing Source**.

##### Add New Source

1. Click the _Add_ button on the top-right of the dialog box.
2. Make sure that the new, empty source is selected.
3. At the bottom, set the **Name:** field to `FSW ProGet`.
4. Set the **Source:** field to `http://proget.fsw.com/nuget/Default`.
5. Click OK.

##### Update Existing Source

1. Select the existing FSW source.
3. At the bottom, set the **Source:** field to `http://proget.fsw.com/nuget/Default`.
4. Click OK.

### Verifying Setup

To make sure that the setup for Visual Studio was successful, follow these
instructions:

1. Open a solution in Visual Studio 2013.
2. Go to **Tools > Nuget Package Manager > Manage Nuget Packages for
Solution...**
3. On the left, expand the **Online** section.
4. Underneath **Online**, you should see four or five options.
  * All
  * nuget.org
  * FSW ProGet
  * FSW (if you still have the original Nuget share configured)
  * Microsoft and .NET
5. If you see the **FSW ProGet** section in the step above, setup is complete.


### Publishing Packages Manually
There are several ways to publish a package. The web interface does a good job of describing them. Just visit the appropriate feed and click "Add Package" to see your options. You should not need to do this, however -- packages should be published through automated processes.

### Publishing Packages Automatically
Generally, packages will be published through an automated job, probably in Jenkins. The steps will be something like this:

* `nuget pack -Build -Properties Configuration=Release (csproj file location) -Symbols` - This will generate two packages: one with sources/symbols and one without. The one with symbols will have a filename ending in `.symbols.nupkg`.
* `nuget push (symbol package name) (API Key) -Source http://proget.fsw.com/nuget/Default` - This pushes the package with symbols to the Nuget feed called *Default* on the ProGet server.
* `move /Y *.nupkg (Original Nuget file share)` - Because some people are still using the old file share based Nuget feed, for the time being we should still put packages there. Assuming ProGet meets our needs, this will eventually be phased out.

The [Package Nuget Package](http://fswjenkins01:8080/job/package_nuget_package/configure) job can be called as a build step of your jobs to do this for you, or you can use it as an example to write your own build steps to publish your packages.