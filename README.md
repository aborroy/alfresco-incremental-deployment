alfresco-incremental-deployment
===============================

This project provides a set of Docker Compose templates to deploy Alfresco Repository 7.2 adding services incrementally.

* [repo](repo) deploys ACS without searching capabilities and without events
* [repo-search](repo-search) deploys ACS with searching capabilities (only metadata) and without events
* [repo-search-content](repo-search-content) deploys ACS with searching capabilities (metadata and content) and without events
* [repo-search-content-events](repo-search-content-events) deploys ACS with searching capabilities (metadata and content) and with events

## repo

**Running**

```bash
$ cd repo
$ docker-compose up
```

**Services available**

* http://localhost:8080/alfresco - Alfresco Repository
* http://localhost:8080/api-explorer - Alfresco REST API

## repo-search

**Running**

```bash
$ cd repo-search
$ docker-compose up
```

**Services available**

* http://localhost:8080/alfresco - Alfresco Repository
* http://localhost:8080/api-explorer - Alfresco REST API
* http://localhost:8983/solr - Solr Web UI Admin Console (using HTTP header `X-Alfresco-Search-Secret=secret`)

## repo-search-content

**Running**

```bash
$ cd repo-search-content
$ docker-compose up
```

**Services available**

* http://localhost:8080/alfresco - Alfresco Repository
* http://localhost:8080/api-explorer - Alfresco REST API
* http://localhost:8983/solr - Solr Web UI Admin Console (using HTTP header `X-Alfresco-Search-Secret=secret`)
* http://localhost:8090 - Transformation Service


## repo-search-content-events

**Running**

```bash
$ cd repo-search-content-events
$ docker-compose up
```

**Services available**

* http://localhost:8080/alfresco - Alfresco Repository
* http://localhost:8080/api-explorer - Alfresco REST API
* http://localhost:8983/solr - Solr Web UI Admin Console (using HTTP header `X-Alfresco-Search-Secret=secret`)
* http://localhost:8090 - Transformation Service
* http://localhost:8161 - ActiveMQ Web Console


## Testing

1) Navigation

```bash
$ curl --location --request \
GET 'http://localhost:8080/alfresco/api/-default-/public/alfresco/versions/1/nodes/-my-' \
--header 'Authorization: Basic YWRtaW46YWRtaW4='
```

2) Search by metadata

```bash
$ curl --location --request \
POST 'http://localhost:8080/alfresco/api/-default-/public/search/versions/1/search' \
--header 'Authorization: Basic YWRtaW46YWRtaW4=' \
--header 'Content-Type: application/json' \
--data-raw '{
  "query": {
    "query": "cm:name:'\''Project Contract.pdf'\''"
  }
}'
```

3) Search by content

```bash
$ curl --location --request \
POST 'http://localhost:8080/alfresco/api/-default-/public/search/versions/1/search' \
--header 'Authorization: Basic YWRtaW46YWRtaW4=' \
--header 'Content-Type: application/json' \
--data-raw '{
  "query": {
    "query": "Moresby"
  }
}'
```

| deployment           | 1 | 2 | 3 |
|----------------------|---|---|---|
| repo                 | v | x | x |
| repo-search          | v | v | x |
| repo-search-content  | v | v | v |


## Default credentials

admin/admin
