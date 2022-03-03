�������� ������� � ������� 6.2 "SQL"

## ������ 1
��������� docker ��������� ������� PostgreSQL (������ 12) c 2 volume, � ������� ����� ������������ ������ �� � ������.
��������� ������������ ������� ��� docker-compose ��������.

�����:
```bash
docker run  --name pg-docker -e POSTGRES_PASSWORD=netology  -p 5432:5432 -v vol1:/var/lib/postgresql/data -v vol2:/var/lib/postgresql postgres:12
```


##  ������ 2
�	�������� ������������ test-admin-user � �� test_db
�	� �� test_db �������� ������� orders � clients (��e��������� ������ ����)
�	������������ ���������� �� ��� �������� ������������ test-admin-user �� ������� �� test_db
�	�������� ������������ test-simple-user
�	������������ ������������ test-simple-user ����� �� SELECT/INSERT/UPDATE/DELETE ������ ������ �� test_db
������� orders:
�	id (serial primary key)
�	������������ (string)
�	���� (integer)
������� clients:
�	id (serial primary key)
�	������� (string)
�	������ ���������� (string, index)
�	����� (foreign key orders)
���������:
�	�������� ������ �� ����� ���������� ������� ����,
�	�������� ������ (describe)
�	SQL-������ ��� ������ ������ ������������� � ������� ��� ��������� test_db
�	������ ������������� � ������� ��� ��������� test_db

����� 2
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
![����������� � �������](https://github.com/Alexdev87/devops-netology/blob/main/media/4.png)


##   5

![����������� � �������](https://github.com/Alexdev87/devops-netology/blob/main/media/5.png)



##   6
![����������� � �������](https://github.com/Alexdev87/devops-netology/blob/main/media/6.png)





