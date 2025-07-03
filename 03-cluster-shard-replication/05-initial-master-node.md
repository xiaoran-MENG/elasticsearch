
## Cluster 

```yaml
services:
 es01:
   image: docker.elastic.co/elasticsearch/elasticsearch:9.0.2
   environment:
   - node.name=es01
   - cluster.name=my-cluster 
   - xpack.security.enabled=false
   - xpack.security.http.ssl.enabled=false
   - cluster.initial_master_nodes=es01
   - "ES_JAVA_OPTS=-Xms512m -Xmx512m"     
 es02:
   image: docker.elastic.co/elasticsearch/elasticsearch:9.0.2
   environment:
   - node.name=es02
   - cluster.name=my-cluster
   - xpack.security.enabled=false
   - xpack.security.http.ssl.enabled=false 
   - cluster.initial_master_nodes=es01
   - discovery.seed_hosts=es01
   - "ES_JAVA_OPTS=-Xms512m -Xmx512m"   
 es03:
   image: docker.elastic.co/elasticsearch/elasticsearch:9.0.2
   environment:
   - node.name=es03
   - cluster.name=my-cluster
   - xpack.security.enabled=false
   - xpack.security.http.ssl.enabled=false
   - cluster.initial_master_nodes=es01
   - discovery.seed_hosts=es01
   - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
 kibana:
   image: docker.elastic.co/kibana/kibana:9.0.2
   ports:
   - 5601:5601
   environment:
   - ELASTICSEARCH_HOSTS=["http://es01:9200","http://es02:9200","http://es03:9200"]
```

## Demo

```
# we have 3 nodes. es01 would be the master
GET /_cat/nodes?v

# bring es01 down and see what happens

# get node detailed information
GET /_nodes
```