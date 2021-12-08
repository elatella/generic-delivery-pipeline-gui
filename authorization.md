# Authorization concept

The authorization concept is currently one of the bigger unsolved problems:
How can it be ensured that a user has the same authorizations as on the build server?
* restricted to certain groups or pipelines
* restricted to certain actions

Ideally, the build server would be accessed with the logged in user. 
But this approach doesn't seem feasible, as it would require to know the users credentials on the build server.
Most of them support Token based and Basic-HTTP authentication.

Another approach is to filter the data retrieved from the build server.
For this to work, the permissions of the user on the build server must be known.
How does the GUI get this information?
* read em from the underlying dps.
* read em from a configuration file placed in the VCS

