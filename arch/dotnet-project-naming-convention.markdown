Assemblies should be properly named as follows:
* WinForm       - <fsw|pride><projectname>_Winform
* Console       - <fsw|pride><projectname>_Console
* Win service   - <fsw|pride><projectname>_Service
* Class Library - <fsw|pride><projectname>_Library
* Web Site      - <fsw|pride><projectname>_Site
* Web Service   - <fsw|pride><projectname>_WS
* Http Handler  - <fsw|pride><projectname>_Handler

…where <fsw|pride> is the company the code belongs to, and <projectName> is the base level namespace of all the contained classes.  For example:
* Fsw.Distribution.Core.API_Library.csproj     (contains Fsw.Distribution.Core.API classes and, possibly private implementation)
* Fsw.Distribution.Core_Library.csproj         (contains all Fsw.Distribution.Core classes except those contained in more specific projects/assemblies)