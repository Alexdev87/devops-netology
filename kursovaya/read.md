
Курсовая работа по итогам модуля "DevOps и системное администрирование"

##  задача 1   Создайте виртуальную машину Linux

Ответ:
```bash
root@ubuntuserv:/home/adm1/my-vagrant-project# vagrant ssh
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-91-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

 System information disabled due to load higher than 1.0


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
Last login: Tue Mar 15 18:10:44 2022 from 10.0.2.2
vagrant@server1:~$
```
##  задача 2 Установите ufw и разрешите к этой машине сессии на порты 22 и 443, при этом трафик на интерфейсе localhost (lo) должен ходить свободно на все порты.
Ответ 
```bash
root@server1:/home/vagrant# sudo ufw status
Status: inactive
root@server1:/home/vagrant# sudo ufw allow 22
Rules updated
Rules updated (v6)
root@server1:/home/vagrant# sudo ufw allow 443
Rules updated
Rules updated (v6)
root@server1:/home/vagrant# sudo ufw enable
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup
root@server1:/home/vagrant# sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
22                         ALLOW       Anywhere
443                        ALLOW       Anywhere
22 (v6)                    ALLOW       Anywhere (v6)
443 (v6)                   ALLOW       Anywhere (v6)
```

## Задача 3 Установите hashicorp vault 
Ответ
```bash
git clone https://github.com/invernizzi/vagrant-scp.git

Добавление прав папке  chmod +x vagrant-scp

переходим в каталог где находится файл vault и переносим в ВМ 

scp -P 2222 vault vagrant@127.0.0.1:.

sudo cp vault /usr/local/bin/

root@server1:/home/vagrant# vault -h
Usage: vault <command> [args]

Common commands:
    read        Read data and retrieves secrets
    write       Write data, configuration, and secrets
    delete      Delete secrets and configuration
    list        List data or secrets
    login       Authenticate locally
    agent       Start a Vault agent
    server      Start a Vault server
    status      Print seal and HA status
    unwrap      Unwrap a wrapped secret

Other commands:
    audit          Interact with audit devices
    auth           Interact with auth methods
    debug          Runs the debug command
    kv             Interact with Vault's Key-Value storage
    lease          Interact with leases
    monitor        Stream log messages from a Vault server
    namespace      Interact with namespaces
    operator       Perform operator-specific tasks
    path-help      Retrieve API help for paths
    plugin         Interact with Vault plugins and catalog
    policy         Interact with policies
    print          Prints runtime configurations
    secrets        Interact with secrets engines
    ssh            Initiate an SSH session
    token          Interact with tokens

root@server1:/home/vagrant# vault --version
Vault v1.5.9 (cgo)

```

## Задача  4  Cоздайте центр сертификации по инструкции (ссылка) и выпустите сертификат для использования его в настройке веб-сервера nginx (срок жизни сертификата - месяц).
Ответ
```bash
root@server1:/home/vagrant# vault server -dev -dev-root-token-id root
==> Vault server configuration:

             Api Address: http://127.0.0.1:8200
                     Cgo: disabled
         Cluster Address: https://127.0.0.1:8201
              Go Version: go1.17.5
              Listener 1: tcp (addr: "127.0.0.1:8200", cluster address: "127.0.0.1:8201", max_request_duration: "1m30s", max_request_size: "33554432", tls: "disabled")
               Log Level: info
                   Mlock: supported: true, enabled: false
           Recovery Mode: false
                 Storage: inmem
                 Version: Vault v1.9.3
             Version Sha: 7dbdd57243a0d8d9d9e07cd01eb657369f8e1b8a
Unseal Key: 1n/zFMbxBsp/oH2gylC+EqGMOGQNDDnWjs0YtP4gOys=
Root Token: root

root@server1:/home/vagrant# export VAULT_ADDR='http://127.0.0.1:8200'
root@server1:/home/vagrant# export VAULT_TOKEN=root

root@server1:/home/vagrant# vault status
Key             Value
---             -----
Seal Type       shamir
Initialized     true
Sealed          false
Total Shares    1
Threshold       1
Version         1.5.9
Cluster Name    vault-cluster-05159c7f
Cluster ID      f1706b4a-80bd-53cd-99e8-1d84cf2fbbd3
HA Enabled      false

```
## Задача  4 часть2 Создание Root CA и Intermediate CA
Ответ
```bash
root@server1:~# vault secrets enable pki
Success! Enabled the pki secrets engine at: pki/

root@server1:~# vault secrets tune -max-lease-ttl=8760h pki
Success! Tuned the secrets engine at: pki/

root@server1:~# vault write -field=certificate pki/root/generate/internal common_name="example.com" ttl=87600h > CA_cert.crt

root@server1:~# vault write pki/config/urls issuing_certificates="http://127.0.0.1:8200/v1/pki/ca" crl_distribution_points="http://127.0.0.1:8200/v1/pki/crl"
Success! Data written to: pki/config/urls

root@server1:~# vault secrets enable -path=pki_int pki
Success! Enabled the pki secrets engine at: pki_int/

root@server1:~# vault secrets tune -max-lease-ttl=8760h pki_int
Success! Tuned the secrets engine at: pki_int/

root@server1:~# apt install jq

root@server1:~# vault write -format=json pki_int/intermediate/generate/internal common_name="example.com Intermediate Authority" | jq -r '.data.csr' > pki_intermediate.csr

root@server1:~# vault write -format=json pki/root/sign-intermediate csr=@pki_intermediate.csr format=pem_bundle ttl="8760h" | jq -r '.data.certificate' > intermediate.cert.pem

root@server1:~# vault write pki_int/intermediate/set-signed certificate=@intermediate.cert.pem
Success! Data written to: pki_int/intermediate/set-signed

root@server1:~# vault write pki_int/roles/example-dot-com allowed_domains="example.com" allow_subdomains=true max_ttl="4380h"
Success! Data written to: pki_int/roles/example-dot-com

root@server1:~# vault list pki_int/roles/
Keys
----
example-dot-com

```
## Задача 5  Установите корневой сертификат созданного центра сертификации в доверенные в хостовой системе.
![](https://github.com/Alexdev87/devops-netology/blob/main/kursovaya/rootcert.png)

## Задача  6.	Установите nginx.
Ответ
```bash
root@server1:~# apt install nginx

root@server1:~# systemctl status nginx
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2022-03-15 10:15:15 UTC; 11s ago
       Docs: man:nginx(8)
   Main PID: 14592 (nginx)
      Tasks: 3 (limit: 1071)
     Memory: 4.4M
     CGroup: /system.slice/nginx.service
             ├─14592 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
             ├─14593 nginx: worker process
             └─14594 nginx: worker process

Dec 07 10:15:15 server1 systemd[1]: Starting A high performance web server and a reverse proxy server...
Dec 07 10:15:15 server1 systemd[1]: Started A high performance web server and a reverse proxy server.

root@server1:~# nano /etc/hosts
127.0.0.1       localhost
127.0.1.1       server1.vm      server
127.0.0.1       test.example.com

 The following lines are desirable for IPv6 capable hosts
::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

## Задача  7 По инструкции (ссылка) настройте nginx на https, используя ранее подготовленный сертификат:
Ответ
```bash
root@server1:~# vault write -format=json pki_int/issue/example-dot-com common_name="test.example.com" ttl=720h > test.example.com.crt

root@server1:~# cat test.example.com.crt
....
serial_number       25:3c:38:ba:3b:14:59:e3:d9:6f:69:41:a1:40:f7:ee:0d:4b:a9:10

root@server1:~# cat test.example.com.crt | jq -r .data.certificate > test.example.com.crt.pem

root@server1:~# cat test.example.com.crt | jq -r .data.issuing_ca >> test.example.com.crt.pem

root@server1:~# cat test.example.com.crt | jq -r .data.private_key > test.example.com.crt.key

Настройка конфигурационного файла nano /etc/nginx/sites-enabled/default

        # SSL configuration
        #
          listen 443 ssl default_server;
          listen [::]:443 ssl default_server;
          ssl_certificate /root/test.example.com.crt.pem;
          ssl_certificate_key /root/test.example.com.crt.key;

root@server1:/home/vagrant# nginx -t
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful

```

## Задача  8 Откройте в браузере на хосте https адрес страницы, которую обслуживает сервер nginx.

![](https://github.com/Alexdev87/devops-netology/blob/main/kursovaya/startpage.png)

## Задача  9 	Создайте скрипт, который будет генерировать новый сертификат в vault:
•	генерируем новый сертификат так, чтобы не переписывать конфиг nginx;
•	перезапускаем nginx для применения нового сертификата.

Ответ
```bash
root@server1:~# nano sert.sh
#!/bin/bash
vault write -format=json pki_int/issue/example-dot-com common_name="test.example.com" ttl=720h > /root/test.example.com.crt
cat /root/test.example.com.crt | jq -r .data.certificate > /root/test.example.com.crt.pem
cat /root/test.example.com.crt | jq -r .data.issuing_ca >> /root/test.example.com.crt.pem
cat /root/test.example.com.crt | jq -r .data.private_key > /root/test.example.com.crt.key

systemctl reload nginx

root@server1:~# chmod ugo+x sert.sh
```
## Задача  10 Поместите скрипт в crontab, чтобы сертификат обновлялся какого-то числа каждого месяца в удобное для вас время.

Ответ
```bash
root@server1:~# sudo systemctl enable cron
Synchronizing state of cron.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable cron
root@server1:~# crontab -e

Настройку сделал так - каждый месяц, 2-го числа, в 9-00 

00 9 2 * * /home/ubuntu/sert.sh

```

