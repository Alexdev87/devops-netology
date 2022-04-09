Домашнее задание к занятию "6.5. Elasticsearch"

##  задача 1

Ответ:
```bash
•	текст Dockerfile манифеста

FROM centos:7

RUN yum -y install wget perl-Digest-SHA
COPY elasticsearch-7.17.0-linux-x86_64.tar.gz .
RUN tar -xzf elasticsearch-7.17.0-linux-x86_64.tar.gz && \
    rm elasticsearch-7.17.0-linux-x86_64.tar.gz

RUN adduser elasticsearch && chown -R elasticsearch /elasticsearch-7.17.0 && chown -R elasticsearch /var/lib

CMD ["./bin/elasticsearch"]

USER elasticsearch
WORKDIR elasticsearch-7.17.0
COPY elasticsearch.yml ./config/
EXPOSE 9200

•	ссылку на образ в репозитории dockerhub
docker push alexdev877/elast:tagname

•	ответ elasticsearch на запрос пути / в json виде

root@ubuntuserv:/home/adm1/1# curl http://localhost:9200
{
  "name" : "netology_test",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "aPA8b0D_Q62isLXfALNSSg",
  "version" : {
    "number" : "7.17.0",
    "build_flavor" : "default",
    "build_type" : "tar",
    "build_hash" : "bee86328705acaa9a6daede7140defd4d9ec56bd",
    "build_date" : "2022-01-28T08:36:04.875279988Z",
    "build_snapshot" : false,
    "lucene_version" : "8.11.1",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}

```


##  задача 2

Ответ:
```bash
Получите список индексов и их статусов, используя API и приведите в ответе на задание.

root@ubuntuserv:/home/adm1/1# curl -X PUT "localhost:9200/index-1?pretty" -H 'Content-Type: application/json' -d'
> {
>   "settings": {
>     "index": {
>      "number_of_shards": 1,
>      "number_of_replicas": 0
>     }
>   }
> }
> '
{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : "index-1"
}

root@ubuntuserv:/home/adm1/1# curl -X PUT "localhost:9200/index-2?pretty" -H 'Content-Type: application/json' -d'
> {
>   "settings": {
>     "index": {
>      "number_of_shards": 2,
>      "number_of_replicas": 1
>     }
>   }
> }
> '
{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : "index-2"
}

root@ubuntuserv:/home/adm1/1# curl -X PUT "localhost:9200/index-3?pretty" -H 'Content-Type: application/json' -d'
> {
>   "settings": {
>     "index": {
>      "number_of_shards": 4,
>      "number_of_replicas": 2
>     }
>   }
> }
> '
{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : "index-3"
}

root@ubuntuserv:/home/adm1/1# curl -X GET http://localhost:9200/_cat/indices
green  open .geoip_databases 9eGr_UGES4-xVZQXlDpDsQ 1 0 40 0 38mb 38mb
green  open index-1          RVvqUzwBTIu9P-XbpB9WXA 1 0  0 0 226b 226b
yellow open index-2          ECfJpzJ7QEGCnAs__6q00A 2 1  0 0 452b 452b
yellow open index-3          e8j_HeRhS3Cbd5W8XhJauA 4 2  0 0 904b 904b

Получите состояние кластера elasticsearch, используя API.

root@ubuntuserv:/home/adm1/1# curl -X GET "localhost:9200/_cat/shards?pretty&v=true"
index            shard prirep state      docs store ip         node
index-2          1     p      STARTED       0  226b 172.17.0.2 netology_test
index-2          1     r      UNASSIGNED
index-2          0     p      STARTED       0  226b 172.17.0.2 netology_test
index-2          0     r      UNASSIGNED
index-1          0     p      STARTED       0  226b 172.17.0.2 netology_test
index-3          3     p      STARTED       0  226b 172.17.0.2 netology_test
index-3          3     r      UNASSIGNED
index-3          3     r      UNASSIGNED
index-3          2     p      STARTED       0  226b 172.17.0.2 netology_test
index-3          2     r      UNASSIGNED
index-3          2     r      UNASSIGNED
index-3          1     p      STARTED       0  226b 172.17.0.2 netology_test
index-3          1     r      UNASSIGNED
index-3          1     r      UNASSIGNED
index-3          0     p      STARTED       0  226b 172.17.0.2 netology_test
index-3          0     r      UNASSIGNED
index-3          0     r      UNASSIGNED
.geoip_databases 0     p      STARTED      40  38mb 172.17.0.2 netology_test

root@ubuntuserv:/home/adm1/1# curl -X GET "localhost:9200/_cluster/health?pretty"
{
  "cluster_name" : "elasticsearch",
  "status" : "yellow",
  "timed_out" : false,
  "number_of_nodes" : 1,
  "number_of_data_nodes" : 1,
  "active_primary_shards" : 8,
  "active_shards" : 8,
  "relocating_shards" : 0,
  "initializing_shards" : 0,
  "unassigned_shards" : 10,
  "delayed_unassigned_shards" : 0,
  "number_of_pending_tasks" : 0,
  "number_of_in_flight_fetch" : 0,
  "task_max_waiting_in_queue_millis" : 0,
  "active_shards_percent_as_number" : 44.44444444444444
}

Как вы думаете, почему часть индексов и кластер находится в состоянии yellow?

Потому что, часть индексов содержит реплики которые должны быть на другой ноде, кластер состоит из одной ноды, количество активных шард в данный момент 44,4%

Удалите все индексы.
root@ubuntuserv:/home/adm1/1# curl -X DELETE "localhost:9200/index-1?pretty"
{
  "acknowledged" : true
}
root@ubuntuserv:/home/adm1/1# curl -X DELETE "localhost:9200/index-2?pretty"
{
  "acknowledged" : true
}
root@ubuntuserv:/home/adm1/1# curl -X DELETE "localhost:9200/index-3?pretty"
{
  "acknowledged" : true
}
                  
```

## Задача  3

Ответ:
```bash
Создайте директорию {путь до корневой директории с elasticsearch в образе}/snapshots
docker exec -u root -it elastic11 bash
[root@7edac655caa1 elasticsearch-7.17.0]# mkdir ./snapshots
[root@7edac655caa1 elasticsearch-7.17.0]# chown elasticsearch:elasticsearch /elasticsearch-7.17.0/snapshots

Используя API зарегистрируйте данную директорию как snapshot repository c именем netology_backup

# echo path.repo: [ "/elasticsearch-7.17.0/snapshots" ] >> "/elasticsearch-7.17.0/config/elasticsearch.yml"

root@ubuntuserv:/home/adm1/1# curl -X PUT "localhost:9200/_snapshot/netology_backup?pretty" -H 'Content-Type: application/json' -d'
{
  "type": "fs",
  "settings": {
    "location": "/elasticsearch-7.17.0/snapshots",
    "compress": true
  }
}'
{
  "acknowledged" : true

Создайте индекс test с 0 реплик и 1 шардом и приведите в ответе список индексов

root@ubuntuserv:/home/adm1/1# curl -X PUT "localhost:9200/test?pretty" -H 'Content-Type: application/json' -d'
> {
>   "settings": {
>     "number_of_shards": 1,
>     "number_of_replicas": 0
>   }
> }
> '
{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : "test"
}

root@ubuntuserv:/home/adm1/1# curl 'localhost:9200/_cat/indices?v'
health status index            uuid                   pri rep docs.count docs.deleted store.size pri.store.size
green  open   .geoip_databases s05UnS7AR3O14sxaojcRbA   1   0         40            0     37.8mb         37.8mb
green  open   test             sYKTC0UQTlmcfPWQG-olvg   1   0          0            0       226b           226b

Создайте snapshot состояния кластера elasticsearch

root@ubuntuserv:/home/adm1/1# curl -X PUT "localhost:9200/_snapshot/netology_backup/snapshot_1?wait_for_completion=true&pretty"
{
  "snapshot" : {
    "snapshot" : "snapshot_1",
    "uuid" : "iEUpUaPZQW-fbgycGh0FfQ",
    "repository" : "netology_backup",
    "version_id" : 7170099,
    "version" : "7.17.0",
    "indices" : [
      "test",
      ".geoip_databases"
    ],
    "data_streams" : [ ],
    "include_global_state" : true,
    "state" : "SUCCESS",
    "start_time" : "2022-04-09T11:07:51.009Z",
    "start_time_in_millis" : 1649502471009,
    "end_time" : "2022-04-09T11:07:52.865Z",
    "end_time_in_millis" : 1649502472865,
    "duration_in_millis" : 1856,
    "failures" : [ ],
    "shards" : {
      "total" : 2,
      "failed" : 0,
      "successful" : 2
    },
    "feature_states" : [
      {
        "feature_name" : "geoip",
        "indices" : [
          ".geoip_databases"
        ]
      }
    ]
  }
}

Приведите в ответе список файлов в директории со snapshotами.

root@ubuntuserv:/home/adm1/1# docker exec -it elastic11 ls -l /elasticsearch-7.17.0/snapshots
total 28
-rw-r--r-- 1 elasticsearch elasticsearch  844 Apr  9 11:07 index-0
-rw-r--r-- 1 elasticsearch elasticsearch    8 Apr  9 11:07 index.latest
drwxr-xr-x 4 elasticsearch elasticsearch 4096 Apr  9 11:07 indices
-rw-r--r-- 1 elasticsearch elasticsearch 9528 Apr  9 11:07 meta-iEUpUaPZQW-fbgycGh0FfQ.dat
-rw-r--r-- 1 elasticsearch elasticsearch  349 Apr  9 11:07 snap-iEUpUaPZQW-fbgycGh0FfQ.dat

Удалите индекс test и создайте индекс test-2. Приведите в ответе список индексов.

root@ubuntuserv:/home/adm1/1# curl -X DELETE "localhost:9200/test?pretty"
{
  "acknowledged" : true
}

root@ubuntuserv:/home/adm1/1# curl -X PUT "localhost:9200/test-2?pretty" -H 'Content-Type: application/json' -d'
> {
>   "settings": {
>     "number_of_shards": 1,
>     "number_of_replicas": 0
>   }
> }
> '
{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : "test-2"
}

root@ubuntuserv:/home/adm1/1# curl 'localhost:9200/_cat/indices?pretty'
green open test-2           TW2S2W2ZRnGQb4wl7fh0IQ 1 0  0 0   226b   226b
green open .geoip_databases s05UnS7AR3O14sxaojcRbA 1 0 40 0 37.8mb 37.8mb

Восстановите состояние кластера elasticsearch из snapshot, созданного ранее.

root@ubuntuserv:/home/adm1/1# curl -X POST "localhost:9200/_snapshot/netology_backup/snapshot_1/_restore?pretty" -H 'Content-Type: application/json' -d'
> {
>   "indices": "*",
>   "include_global_state": true
> }
> '
{
  "accepted" : true
}

Приведите в ответе запрос к API восстановления и итоговый список индексов.

root@ubuntuserv:/home/adm1/1# curl 'localhost:9200/_cat/indices?pretty'
green open test-2           TW2S2W2ZRnGQb4wl7fh0IQ 1 0  0 0   226b   226b
green open .geoip_databases D29FOyOKTBqSgRqnjHSLzw 1 0 40 0 37.8mb 37.8mb
green open test             7eWAdO2yTkiXMVL319SOKQ 1 0  0 0   226b   226b


```


