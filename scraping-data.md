GET
POST
PUT 
DELETE
---
STEP 1
---
- Got API FROM crunchbase via  rapidAPI
- modified
- creating a new file unnecessary if you don't post the file to github 
what we get 
``` python ruby
import http.client

conn = http.client.HTTPSConnection("crunchbase-api.p.rapidapi.com")

headers = {
    'x-rapidapi-key': "31abfc5dd4msh2c40bc08418c543p1b05b8jsnf9cf5a1a66ca",
    'x-rapidapi-host': "crunchbase-api.p.rapidapi.com",
    'Content-Type': "application/json"
}

conn.request("GET", "/v1/health-check", headers=headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```
what to make of it
``` python ruby
import requests

url = "https://crunchbase-api.p.rapidapi.com/v1/health-check"

headers = {
    "x-rapidapi-key": os.getenv("RAPIDAPI_KEY"),  # from your .env
    "x-rapidapi-host": "crunchbase-api.p.rapidapi.com"
}

response = requests.get(url, headers=headers)
print(response.status_code)
print(response.json())
```
