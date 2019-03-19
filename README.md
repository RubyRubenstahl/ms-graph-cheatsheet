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

### List the files and folders in the root level of a drive
url: `https://graph.microsoft.com/beta/drives/{drivId}/root/children`

### Get a listing of items in a document library General folder of a drive
url: `https://graph.microsoft.com/beta/groups/{groupId | teamId}/drive/root:/General`

### Enumerate the files and folders in a folder
url: `https://graph.microsoft.com/beta/groups/{groupId}/drive/items/{itemId}/children`
[source](https://docs.microsoft.com/en-us/graph/api/driveitem-list-children?view=graph-rest-1.0)
* The item id can come from either a previous call to a `/children` endpoint or from the `drive/root:/[path]` endpoint.

### Create a new folder
POST /drives/{drive-id}/items/{parent-item-id}/children
POST /groups/{group-id}/drive/items/{parent-item-id}/children
POST /me/drive/items/{parent-item-id}/children
POST /sites/{site-id}/drive/items/{parent-item-id}/children
POST /users/{user-id}/drive/items/{parent-item-id}/children
