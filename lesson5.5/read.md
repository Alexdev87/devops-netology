Домашнее задание к занятию "5.5. Оркестрация кластером Docker контейнеров на примере Docker Swarm."

##  задача 1

Ответ:
```bash
•	В чём отличие режимов работы сервисов в Docker Swarm кластере: replication и global?

В режиме replicated приложение запускается в том количестве экземпляров, какое укажет пользователь. При этом на отдельной ноде может быть как несколько экземпляров приложения, так и не быть совсем.
В режиме global приложение запускается обязательно на каждой ноде и в единственном экземпляре.

•	Какой алгоритм выбора лидера используется в Docker Swarm кластере?
Raft.
1.	Протокол решает проблему согласованности: чтобы все manager ноды имели одинаковое представление о состоянии кластера
2.	Для отказоустойчивой работы должно быть не менее трёх manager нод.
3.	Количество нод обязательно должно быть нечётным, но лучше не более 7 (это рекомендация из документации Docker).
4.	Среди manager нод выбирается лидер, его задача гарантировать согласованность.
5.	Лидер отправляет keepalive пакеты с заданной периодичностью в пределах 150-300мс. Если пакеты не пришли, менеджеры начинают выборы нового лидера.
6.	Если кластер разбит, нечётное количество нод должно гарантировать, что кластер останется консистентным, т.к. факт изменения состояния считается совершенным, если его отразило большинство нод. Если разбить кластер пополам, нечётное число гарантирует что в какой-то части кластера будеть большинство нод.

•	Что такое Overlay Network?
L2 VPN сеть для связи демонов Docker между собой. В основе используется технология vxlan

```


##  задача 2
Ответ 2
```bash
root@ubuntuserv:/home/adm1/src/terraform# ssh centos@178.154.229.100
Enter passphrase for key '/root/.ssh/id_rsa':
[centos@node01 ~]$ sudo -i
[root@node01 ~]# docker node ls
ID                            HOSTNAME             STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
6ghfjwdfjgn1ut2md36wnqztl *   node01.netology.yc   Ready     Active         Reachable        20.10.13
j0c9v8kk1cjk31wjg5wkd24re     node02.netology.yc   Ready     Active         Leader           20.10.13
5goll6mr316sx2km12oatbdee     node03.netology.yc   Ready     Active         Reachable        20.10.13
te390u216nvdo3ks27bhjo30l     node04.netology.yc   Ready     Active                          20.10.13
xbpl9d2vkvl7oidurkr4crxo7     node05.netology.yc   Ready     Active                          20.10.13
qi8wcofskx56rutpow8a0pwmk     node06.netology.yc   Ready     Active                          20.10.13

```

## Задача  3
```bash
[root@node01 ~]# docker service ls
ID             NAME                                MODE         REPLICAS   IMAGE                                          PORTS
ck63v74r1s4e   swarm_monitoring_alertmanager       replicated   1/1        stefanprodan/swarmprom-alertmanager:v0.14.0
cug25smqjpub   swarm_monitoring_caddy              replicated   1/1        stefanprodan/caddy:latest                      *:3000->3000/tcp, *:9090->9090/tcp, *:9093-9094->9093-9094/tcp
kb37yujmftud   swarm_monitoring_cadvisor           global       6/6        google/cadvisor:latest
ehjm5jyog06a   swarm_monitoring_dockerd-exporter   global       6/6        stefanprodan/caddy:latest
7pt6g93hu8d4   swarm_monitoring_grafana            replicated   1/1        stefanprodan/swarmprom-grafana:5.3.4
m05x6ywlkr3y   swarm_monitoring_node-exporter      global       6/6        stefanprodan/swarmprom-node-exporter:v0.16.0
qag2c9njy1ag   swarm_monitoring_prometheus         replicated   1/1        stefanprodan/swarmprom-prometheus:v2.5.0
gvyl41a0p78w   swarm_monitoring_unsee              replicated   1/1        cloudflare/unsee:v0.8.0

```

