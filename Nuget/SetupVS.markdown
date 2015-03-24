# FSW Nuget Feed Setup
FSW has its own nuget feed that we use to deploy and share our own internal
packages. The FSW 4.0 solution, and most other current solutions, already have
this set up for deployment.  However, when it comes to local development, there
are a few steps you will want to take in order to add or update FSW packages.

## Location of the FSW Nuget Feed
Currently, FSW packages are split between the FSW share and
[Proget](Nuget/fsw-proget). The FSW share path is:

`\\Fswfs\fsw\Development\Software\nugetFeed`

At this location you will find a large store of .nupkg files.  These are
different versions of our packages.

Please read the instruction in the [Fsw Proget](Nuget/fsw-proget) page for setup additional
setup instructions.

## Visual Studio 2013 Setup
To make Visual Studio search the FSW package feed for packages, follow these
steps:

1. Go to **Tools > Nuget Package Manager > Package Manager Settings**.  This
should open an **Options** window open to the **Nuget Package Manager** section.
2. In the list on the left, select **Package Sources**.
3. In the main pane you should see one or two sources.  One will be the official
nuget feed, _nuget.org_.  If your or someone else had added the FSW package feed
, that should also be visible, although less likely.  If you only see
_nuget.org_, follow the instructions under **Add New Source**.  Otherwise,
follow instructions under **Update Existing Source**.

### Add New Source

1. Click the _Add_ button on the top-right of the dialog box.
2. Make sure that the new, empty source is selected.
3. At the bottom, set the **Name:** field to FSW.
4. Set the **Source:** field to the Location of the FSW Nuget Feed.
5. Click OK.

### Update Existing Source

1. Select the existing FSW source.
2. At the bottom, set the **Source:** field to the Location of the FSW Nuget Feed.
3. Click OK.

## Verifying Setup

To make sure that the setup for Visual Studio was succesful, follow these
instructions:

1. Open a solution in Visual Studio 2013.
2. Go to **Tools > Nuget Package Manager > Manage Nuget Packages for
Solution...**
3. On the left, expand the **Online** section.
4. Underneath **Online**, you should see four options.
  * All
  * nuget.org
  * FSW
  * Microsoft and .NET
5. If you see the **FSW** section in the step above, setup is complete.
