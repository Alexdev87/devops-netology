їїїїїїїї їїїїїїї ї їїїїїїї 6.2 "SQL"

## їїїїїї 1
їїїїїїїїї docker їїїїїїїїї їїїїїїї PostgreSQL (їїїїїї 12) c 2 volume, ї їїїїїїї їїїїї їїїїїїїїїїїї їїїїїї її ї їїїїїї.
їїїїїїїїї їїїїїїїїїїїї їїїїїїї їїї docker-compose їїїїїїїї.

їїїїї:
```bash
docker run  --name pg-docker -e POSTGRES_PASSWORD=netology  -p 5432:5432 -v vol1:/var/lib/postgresql/data -v vol2:/var/lib/postgresql postgres:12
```


##  їїїїїї 2
ї	їїїїїїїї їїїїїїїїїїїї test-admin-user ї її test_db
ї	ї її test_db їїїїїїїї їїїїїїї orders ї clients (їїeїїїїїїїїї їїїїїї їїїї)
ї	їїїїїїїїїїїї їїїїїїїїїї її їїї їїїїїїїї їїїїїїїїїїїї test-admin-user її їїїїїїї її test_db
ї	їїїїїїїї їїїїїїїїїїїї test-simple-user
ї	їїїїїїїїїїїї їїїїїїїїїїїї test-simple-user їїїїї її SELECT/INSERT/UPDATE/DELETE їїїїїї їїїїїї її test_db
їїїїїїї orders:
ї	id (serial primary key)
ї	їїїїїїїїїїїї (string)
ї	їїїї (integer)
їїїїїїї clients:
ї	id (serial primary key)
ї	їїїїїїї (string)
ї	їїїїїї їїїїїїїїїї (string, index)
ї	їїїїї (foreign key orders)
їїїїїїїїї:
ї	їїїїїїїї їїїїїї її їїїїї їїїїїїїїїї їїїїїїї їїїї,
ї	їїїїїїїї їїїїїї (describe)
ї	SQL-їїїїїї їїї їїїїїї їїїїїї їїїїїїїїїїїїї ї їїїїїїї їїї їїїїїїїїї test_db
ї	їїїїїї їїїїїїїїїїїїї ї їїїїїїї їїї їїїїїїїїї test_db

їїїїї 2
```bash
test_db=# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges
-----------+----------+----------+------------+------------+-----------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 test_db   | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
(4 rows)

test_db=# \dt
          List of relations
 Schema |  Name   | Type  |  Owner
--------+---------+-------+----------
 public | clients | table | postgres
 public | orders  | table | postgres
(2 rows)

test_db=# \du
                                       List of roles
    Role name     |                         Attributes                         | Member of
------------------+------------------------------------------------------------+-----------
 postgres         | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 test-admin-user  | Superuser, No inheritance                                  | {}
 test-simple-user | No inheritance                                             | {}


test_db=# select * from information_schema.table_privileges where grantee in ('test-admin-user','test-simple-user');
 grantor  |     grantee      | table_catalog | table_schema | table_name | privilege_type | is_grantable | with_hierarchy
----------+------------------+---------------+--------------+------------+----------------+--------------+----------------
 postgres | test-simple-user | test_db       | public       | clients    | INSERT         | NO           | NO
 postgres | test-simple-user | test_db       | public       | clients    | SELECT         | NO           | YES
 postgres | test-simple-user | test_db       | public       | clients    | UPDATE         | NO           | NO
 postgres | test-simple-user | test_db       | public       | clients    | DELETE         | NO           | NO
 postgres | test-simple-user | test_db       | public       | orders     | INSERT         | NO           | NO
 postgres | test-simple-user | test_db       | public       | orders     | SELECT         | NO           | YES
 postgres | test-simple-user | test_db       | public       | orders     | UPDATE         | NO           | NO
 postgres | test-simple-user | test_db       | public       | orders     | DELETE         | NO           | NO
(8 rows)

```

##   3
![](https://github.com/Alexdev87/devops-netology/blob/main/media/3.png)


##   4
![Иллюстрация к проекту](https://github.com/Alexdev87/devops-netology/blob/main/media/4.png)


##   5

![Иллюстрация к проекту](https://github.com/Alexdev87/devops-netology/blob/main/media/5.png)



##   6
![Иллюстрация к проекту](https://github.com/Alexdev87/devops-netology/blob/main/media/6.png)





