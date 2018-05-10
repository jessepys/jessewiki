## Install elastic search

### Pull images

```
docker pull docker.elastic.co/elasticsearch/elasticsearch:6.2.4
docker pull docker.elastic.co/kibana/kibana:6.2.4
```

### Create file elastic_kibana.yml:

```
version: '2'
services:

  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:5.2.2
    environment:
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    mem_limit: 1g
    volumes:
      - esdata1:/usr/share/elasticsearch/data
    ports:
      - 9200:9200

  kibana:
    image: docker.elastic.co/kibana/kibana:5.2.2
    links:
      - elasticsearch
    ports:
      - 5601:5601

volumes:
  esdata1:
    driver: local
```
### Start up

```
  docker-compse -f elastic_kibana.yml up
```

### Access kibaba:

```
http://localhost:5601/app/kibana#/management?_g=()
```