There is many standards being used by big companies and lot of specification. This document only cover how error handling, pagination is defined by some big company.
## Error Handling

### General Practices
- Always return a JSON response.
- Always return a 4xx or 5xx status code.
- Always return a message field in the response.
### Google
* Use standard HTTP status codes.
* Use a JSON response body.
* Use a message field in the response body.
```json
{
  "error": {
    "code": 404,
    "message": "Not Found"
  }
}
```
### Microsoft
* Use standard HTTP status codes.
* Use a JSON response body.
* Use a message field in the response body.
* Use a code field in the response body.
```json
{
  "error": {
    "code": "BadArgument",
    "message": "The provided database 'foo' has an invalid username.",
    "target": "query",
    "details": [
      {
        "code": "301",
        "target": "$search",
        "message": "$search query option not supported"
      }
    ]
  }
}
```
### Meta
* Use standard HTTP status codes.
* Use a JSON response body.
* Use a message field in the response body.
```json
{
  "error": {
    "message": "Error message",
    "type": "OAuthException",
    "code": 190,
    "error_subcode": 460,
    "fbtrace_id": "AXWAv0tnFxu"
  }
}
```

## Pagination

### General Practices
- Use a limit and offset query parameter for pagination.
- For cursor-based pagination, use a cursor query parameter.
- Always include object that explain position in the pagination.
### Google
* Use a limit and offset query parameter.
```json
{
  "data": [
    {
      "id": "1",
      "name": "Alice"
    },
    {
      "id": "2",
      "name": "Bob"
    }
  ],
  "paging": {
    "next": "https://example.com/api/v1/users?limit=2&offset=2"
  }
}
```
### Microsoft
OData-based pagination.
* Parameters: $top, $skip, $count
* Example: `https://services.odata.org/v4/TripPinServiceRW/People?$top=2
```json
{
  "@odata.context": "https://services.odata.org/v4/TripPinServiceRW/$metadata#People",
  "value": [
    {
      "UserName": "russellwhyte",
      "FirstName": "Russell",
      "LastName": "Whyte"
    },
    {
      "UserName": "scottketchum",
      "FirstName": "Scott",
      "LastName": "Ketchum"
    }
  ],
  "@odata.nextLink": "https://services.odata.org/v4/TripPinServiceRW/People?$skip=2"
}
```
Link header-based pagination.
* Link example `Link: <https://example.com/api/v1/users?limit=2&offset=2>; rel="next"``
* Example response
```json
{
  "data": [
    {
      "id": "1",
      "name": "Alice"
    },
    {
      "id": "2",
      "name": "Bob"
    }
  ]
}
```