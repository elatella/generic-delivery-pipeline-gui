# Authorization concept

The authorization concept is currently one of the bigger unsolved problems:
How can it be ensured that a user has the same authorizations as on the build server?

* restricted to certain groups or pipelines
* restricted to certain actions

Ideally, the build server would be accessed with the logged-in user. 
But this approach doesn't seem feasible, as it would require to know the users credentials on the build server.
Most of them support token based and basic-HTTP authentication.

Another approach is to filter the data retrieved from the build server.
For this to work, the permissions of the user on the build server must be known.
How does the GUI get this information?

* read em from the build server
  * which of them offer such a feature?
* read em from a configuration file placed in the VCS
* further ideas (TODO)

## Read users/permissions by API call

### GitLab

`/api/v4/groups/{{groupId}}/members`
`/api/v4/projects/{{projectId}}/members`
Returns a list of `username`s including their numeric `access_level`

### Github

`api.github.com/orgs/{{organizationName}}/members`
Returns a list of organization `members` with their `login` and `type`
`api.github.com/repos/{{organizationName}}/{{repoName}}/contributors` 
Returns a list of `contributors` with their `login` and `type`
`api.github.com/users/{{userName}}/repos`
Returns a list of `repos` which the user is owner of
Not too useful, as far...
