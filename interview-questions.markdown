## Interviews for Developers
Our interviews will include a phone screen, in-person questions and whiteboard, then a coding test.  We will standardize the possible list of questions, then ask questions targeting areas that candidates claim to or appear to be strong in, going as deep in those areas as possible.
Scoring Sheet for these questions here:
https://docs.google.com/spreadsheets/d/1-Kcg4NiBNKuEr54gzTNB6tCLShVmT4_zcg3ZkAVXqvI/edit?usp=sharing

### Question Areas
* [Cultural Fit](questions_cultural_fit)
* [Aptitude/Passion](questions_aptitude_passion)
* [OOP](questions_oop)
* [JS/UI](questions_js)
* [.NET/C#](questions_net)
* [Web](questions_web)

### Coding Test
Details of how to conduct the coding test here: [Coding Test](coding_test)

### Sample question and answer:

#### Q: If you are building a form on a site, such as a form that takes a user’s address, do you think validation should happen on the client or the server side?

#### A: Both.

Client-side because it means a more responsive user experience and less chatter over the wire
* A good answer here indicates decent UI or usability skills
* If client-side is not mentioned, they may not have much web or JS experience

Server-side because code should never trust that a client has validated input (security).  Some validation also requires complex validation like asserting that a city matches a zip code, which is impractical to do client-side.
* A good answer here indicates solid coding fundamentals and at least rudimentary focus on security.
* If server-side is not mentioned, they may be more of a JS/HTML developer than a full-stack

#### Follow-Ups:
* Ask them “Why?” if they don’t give much explanation
* If they only give one, ask if they see a downside to only focusing on that type.  That should guide them towards thinking about both.
