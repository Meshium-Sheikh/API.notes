## Error codes & their meanings
---
```ruby
200: Everything went okay, and the result has been returned (if any).
301: The server is redirecting you to a different endpoint. This can happen when a company switches domain names or changes an endpoint name.
400: The server thinks you made a bad request. This happens when you send incorrect data or make other client-side errors.
401: The server thinks you're not authenticated. Many APIs require login credentials, so this happens when the correct credentials are not sent.
403: The resource you're trying to access is forbidden. You don’t have the right permissions to see it.
404: The resource you tried to access wasn’t found on the server.
503: The server is not ready to handle the request.
404: Can't find the resource
```
- codes starting with 4 : client-side errors
- codes starting with 5 : server-side issues

## json
---
```ruby
The json library provides two essential functions:

json.dumps(): Converts a Python object into a JSON string.
json.loads(): Converts a JSON string into a Python object.
Using dumps(), we can format JSON data for better readability:
``
