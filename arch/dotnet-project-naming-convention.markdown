Assemblies should be properly named as follows:
* WinForm       - <projectname >_Winform
* Console       - <projectname >_Console
* Win service   - <projectname >_Service
* Class Library - <projectname >_Library
* Web Site      - <projectname >_Site
* Web Service   - <projectname >_WS
* Http Handler  - <projectname >_Handler

…where <projectName> is the base level namespace of all the contained classes.  For example:
* Distribution.Core.API_Library.csproj     (contains Distribution.Core.API classes and, possibly private implementation)
* Distribution.Core_Library.csproj         (contains all Distribution.Core classes except those contained in more specific projects/assemblies)