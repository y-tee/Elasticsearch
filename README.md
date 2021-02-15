# Elasticsearch
All things elasticsearch

#### Setting up docker

##### ELK Docker: 
elk docker set-up : https://www.youtube.com/watch?v=PWUuyDrqvt0

##### Working with opendistro ES-kibana docker network
the sample `docker-compose.yml` file in the documentation does not work, refer to [this](https://stackoverflow.com/questions/62072910/kibana-opendistro-cant-connect-to-elasticsearch-open-distro-container-on-docker) \
but do not replace `kibana.yml` file as stated. The guy changed `elasticsearch.hosts` from `https://localhost:9200` to `https://odfe-node1:9200` which is causing main problems in kibana ui:all icons are clickable but only show the ES server stats


#### Checks
```
GET _cluster/health?pretty
```

Indices check desc
```
GET /_cat/indices?bytes=b&s=store.size:desc&v
```
Nodes and usage check
```
GET /_cat/nodes?v
```
Indices alias
```
GET /_cat/aliases
```

#### Queries
1. Get a field, sorted desc
```
GET /<index name>/_search
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

2. Query json in arrays in nested field [link](https://www.monterail.com/blog/how-to-index-objects-elasticsearch)
```
GET <index name>/_search
{
  "query": {
    "nested": {
        "path": "<array key>",
        "query":{
        "bool": {
          "filter": [
            {
              "match": {
                "<array key>.<key wanted in array>": <value>
              }
            }
          ]
        }
      }
    }
  }  
}
```

3. Query based on date
```
GET <index_name>/_search
{
  "query": {
    "bool": {
      "must":[ 
              {
                "range": {
                  "updatedOn": {
                    "gte": "2021-02-13T00:00:06.487000",
                    "lte": "2021-02-14T00:00:06.487000"
                  }
                }
              }
      ]
    }
  },
  "size": 10
}
```
