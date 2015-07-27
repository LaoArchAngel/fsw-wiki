## Usage Scenario

We expect *OpenID Connect* to support the majority of our authentication/authorization workflows.  *OpenID Connect* standardizes how user info is provided and retrieved, and how the data is structured and organized.  It extends the oAuth `authorization code` flow by introducing new tokens and standardizing some auth and user endpoints.  

The purpose of these extensions is to allow the *Resource Owner's* (the user's) profile information be provided to the client during the typical `authorization code` oAuth workflow.  This is necessary because the oAuth spec was intentionally created to ensure that there is no unintended leakage of information about the user to the client (ensuring the client can never get a hold of the user's credentials).  This limitation is restricting for clients because user profile information is often necessary in order for clients to meaningfully identify or cater to their users.  

In the of applications built by FSW, it would be expected that our clients (the applications we build) know about the user given that FSW is also the identity provider and oAuth server.

---------------------------------------------------------------

The below sequence diagram was generated w/ [Web Sequence Diagrams](https://www.websequencediagrams.com/), using the following [source text](http://gitlab.fsw.com/snippets/9).

![OpenID_Connect_Profile_Flow](http://gitlab.fsw.com/tfs/library/uploads/f93bb545dc6b1b252113523ee6f1eac8/OpenID_Connect_Profile_Flow.png)
