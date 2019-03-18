# ms-graph-cheatsheet
A cheatsheet of useful info for MS graph. 


## Teams

###  Creating teams
When a team is created, the id is returned in the "Location" header of the HTTP response. It's encoded along with some other info. It can be easily extracted with a regular expression.
```JS
  function extractTeamId(result) {
    const locationHeader = result.headers.location;
    const pattern = /\/teams\(\'([0-9a-z\-]*)/
    const match = locationHeader.match(pattern);
    return match[1] ? match[1] : null;
  }
 ```

### Get the sharepoint site for a team
url: `https://graph.microsoft.com/[v1.0 | beta]/groups/{group-id}/sites/root`


## Sharepoint

### Getting the drive id for a Sharepoint document foloder
url: `https://graph.microsoft.com/beta/groups/{groupId}/drive/root`


### Get a listing of items in a document library General folder
url: `https://graph.microsoft.com/beta/groups/{groupId | teamId}/drive/root:/General`

### Get the children of a drive folder
url: `https://graph.microsoft.com/beta/groups/{groupId}/drive/items/{itemId}/children`
[source](https://docs.microsoft.com/en-us/graph/api/driveitem-list-children?view=graph-rest-1.0)
* The item id can come from either a previous call to a `/children` endpoint or from the `drive/root:/[path]` endpoint.
