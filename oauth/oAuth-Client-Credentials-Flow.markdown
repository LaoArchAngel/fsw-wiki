## Usage Scenario

The oAuth flow best suited to server-to-server communication is called the `Client Credentials` flow and has been documented in the sequence diagram below.

When a server app needs to call an some Api, but no *Resource Owner* (user) is involved, the *OpenID Connect* flow no longer makes sense since OpenID Connect is centered around the user as the *Resource Owner*.  By contrast, in a server-to-server scenario, the client application **is** the *Resource Owner*.  For this reason, the delegated authorization provided by *OpenID Connect* is not required.

An important item of note:  During server-to-server communication, when required, user information must be provided as part of the Api contract because it will not be implicitly passed as part of the request context via `token_id`.

---------------------------------------------------------------

The below sequence diagram was generated w/ [Web Sequence Diagrams](https://www.websequencediagrams.com/), using the following [source text](http://gitlab.fsw.com/snippets/11).

![oAuth_Client_Credentials_Flow](http://gitlab.fsw.com/tfs/library/uploads/2e8af38f321c3c4ba45cc146f1d97a39/oAuth_Client_Credentials_Flow.png)
