# OR Requests

```
{
  "query": {
    "bool": {
      "should": [
        {
          "match": {
            "data.src": "xxx"
          }
        },
        {
          "match": {
            "data.src": "yyy"
          }
        }
      ]
    }
  }
}
```