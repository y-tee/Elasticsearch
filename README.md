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
