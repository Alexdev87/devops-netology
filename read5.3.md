Задача 1
Ответ https://hub.docker.com/r/alexdev877/netology

Задача 2
Сценарий:
•	Высоконагруженное монолитное java веб-приложение;
физический сервер(а), в условии указанно что приложение монолитное, можно сделать вывод, что в микросерверах не реализуемо без изменения кода, и так как высоконагруженное -  то необходим физический доступ к ресурсами, без наслоения дополнительными гипервизорами и  ВМ.
•	Nodejs веб-приложение;
это веб приложение, для таких приложений думаю должно быть достаточно докера, противопоказаний для контейнерной реализации нет.
•	Мобильное приложение c версиями для Android и iOS;
Виртуальные машины -  Android и iOS в докере не имеет GUI, а для тестирования необходимо графическая оболочка.
•	Шина данных на базе Apache Kafka;
Может использоваться контейнерная технология если потеря данных при потере контейнера не является критичной, если есть критичность лучше ВМ.
•	Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana;
Можно использовать на Docker – т.к данные приложения не хранят у себя данные, а лишь предоставляют отчеты и графики.
•	Мониторинг-стек на базе Prometheus и Grafana;
Можно использовать на Docker – т.к данные приложения не хранят у себя данные, а лишь предоставляют отчеты и графики.
•	MongoDB, как основное хранилище данных для java-приложения;
В зависимости от критичности данных можно сделать выбор между ВМ и Docker, так как это БД, я же все таки предложил ВМ.
•	Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry.
Необходимо использовать ВМ в качестве сервера.

Задача 3 

root@ubuntuserv:/home/adm1# docker pull debian
Using default tag: latest
latest: Pulling from library/debian
0c6b8ff8c37e: Pull complete
Digest: sha256:fb45fd4e25abe55a656ca69a7bef70e62099b8bb42a279a5e0ea4ae1ab410e0d
Status: Downloaded newer image for debian:latest
docker.io/library/debian:latest
root@ubuntuserv:/home/adm1# docker run -dit -P --name centos-test -v ~/data:/data centos
5adac82cd9038185f83f88bf1ef8661b1f32d4c3031a36f3bfde7a6d60749aea
root@ubuntuserv:/home/adm1# docker run -dit -P --name debian-test -v ~/data:/data debian
be9e2e672e512373d2043f140f051c5c02b3e5dfd64e22f8dc77094b29a86073
root@ubuntuserv:/home/adm1# docker attach 5ada
[root@5adac82cd903 /]# touch /data/test
[root@5adac82cd903 /]# exit
exit
root@ubuntuserv:/home/adm1# ls /root/data
test
root@ubuntuserv:/home/adm1# docker attach be9e
root@be9e2e672e51:/# ls /data
123.txt  test
root@be9e2e672e51:/# exit

