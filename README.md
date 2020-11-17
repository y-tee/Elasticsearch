# Elasticsearch
All things elasticsearch

#### Queries
1. Get a field, sorted desc
```
POST /<index name>/_search
{
  "_source": "<field name>",
  "sort":[
      {
        "<field name>": {
      "order": "desc"
      }
    }
  ]
}
```
