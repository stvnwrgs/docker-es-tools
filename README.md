# docker-es-tools

## docker-optimize-index
```
docker run \
    --name es-tools \
    -e ELASTICSEARCH=$ELASTICSEARCH_ENDPOINT \
    pindar/es-tools \
    /elasticsearch-optimize-index.sh
```

## remove-old-indices

### Usage:
```
elasticsearch-remove-old-indices.sh

Compares the current list of indices to a configured value and deletes any
indices surpassing that value. Sort is lexicographical; the first n of a 'sort
-r' list are kept, all others are deleted.


USAGE: ./elasticsearch-remove-old-indices.sh [OPTIONS]

OPTIONS:
  -h    Show this message
  -i    Indices to keep (default: 14)
  -e    Elasticsearch URL (default: http://localhost:9200)
  -g    Consistent index name (default: logstash)
  -o    Output actions to a specified file
  -r    instead of single execution, repeat the command every x seconds

EXAMPLES:

  ./elasticsearch-remove-old-indices.sh

    Connect to http://localhost:9200 and get a list of indices matching
    'logstash'. Keep the top lexicographical 14 indices, delete any others.

  ./elasticsearch-remove-old-indices.sh -e "http://es.example.com:9200" \
  -i 28 -g my-logs -o /mnt/es/logfile.log -r 60

    Connect to http://es.example.com:9200 and get a list of indices matching
    'my-logs'. Keep the top 28 indices, delete any others. When using a custom
    index naming scheme be sure that a 'sort -r' places the indices you want to
    keep at the top of the list. Output index deletes to /mnt/es/logfile.log.
```
### docker

```
docker run \
    --name es-tools \
    pindar/es-tools \
    /elasticsearch-remove-old-indices.sh -e "$ELASTICSEARCH_ENDPOINT" -i 3 -r 60
```