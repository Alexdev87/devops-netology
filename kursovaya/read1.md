Доработка "Курсовая работа по итогам модуля "DevOps и системное администрирование"

##  1

Ответ: При создании сертификата вручную такой состав файлов и серийный номер сертификата
```bash
"serial_number": "63:68:d0:ec:6d:7f:3f:87:6f:be:6b:25:a3:50:56:46:e9:a5:c1:a0"

root@server1:~# ls -lha
total 80K
drwx------  6 root root 4.0K Mar 24 16:33 .
drwxr-xr-x 21 root root 4.0K Mar 15 18:08 ..
-rw-------  1 root root 3.6K Mar 24 16:21 .bash_history
-rw-r--r--  1 root root 3.1K Dec  5  2019 .bashrc
-rwxr-xr-x  1 root root 1.2K Mar 24 16:31 CA_cert.crt
drwxr-xr-x  3 root root 4.0K Mar 15 18:17 .cache
-rw-r--r--  1 root root 1.3K Mar 24 16:33 intermediate.cert.pem
drwxr-xr-x  3 root root 4.0K Mar 15 18:38 .local
-rw-r--r--  1 root root  924 Mar 24 16:32 pki_intermediate.csr
-rw-r--r--  1 root root  161 Dec  5  2019 .profile
-rw-r--r--  1 root root   66 Mar 20 15:37 .selected_editor
-rwxr-xr-x  1 root root  406 Mar 20 15:29 sert.sh
drwxr-xr-x  3 root root 4.0K Dec 19 19:42 snap
drwx------  2 root root 4.0K Mar 15 18:08 .ssh
-rw-r--r--  1 root root 6.0K Mar 24 16:40 test.example.com.crt
-rw-r--r--  1 root root 1.7K Mar 24 16:41 test.example.com.crt.key
-rw-r--r--  1 root root 2.6K Mar 24 16:41 test.example.com.crt.pem
-rw-------  1 root root    4 Mar 24 06:04 .vault-token
-rw-------  1 root root 1.3K Mar 24 16:24 .viminfo

```

##  2
Ответ 2 При создании сертификата функцией cron такой состав файлов и серийный номер сертификата
```bash
"serial_number": "6e:6c:f0:14:75:2f:51:c4:bf:b4:36:74:51:8e:1f:32:bd:4e:57:60"

root@server1:~# ls -lha
total 84K
drwx------  6 root root 4.0K Mar 24 16:52 .
drwxr-xr-x 21 root root 4.0K Mar 15 18:08 ..
-rw-------  1 root root 3.6K Mar 24 16:21 .bash_history
-rw-r--r--  1 root root 3.1K Dec  5  2019 .bashrc
-rwxr-xr-x  1 root root 1.2K Mar 24 16:31 CA_cert.crt
drwxr-xr-x  3 root root 4.0K Mar 15 18:17 .cache
-rw-r--r--  1 root root 1.3K Mar 24 16:33 intermediate.cert.pem
drwxr-xr-x  3 root root 4.0K Mar 15 18:38 .local
-rw-r--r--  1 root root  924 Mar 24 16:32 pki_intermediate.csr
-rw-r--r--  1 root root  161 Dec  5  2019 .profile
-rw-r--r--  1 root root   66 Mar 20 15:37 .selected_editor
-rwxr-xr-x  1 root root  364 Mar 24 16:52 sert.sh
drwxr-xr-x  3 root root 4.0K Dec 19 19:42 snap
drwx------  2 root root 4.0K Mar 15 18:08 .ssh
-rw-r--r--  1 root root 6.0K Mar 24 16:57 test.example.com.crt
-rw-r--r--  1 root root 1.7K Mar 24 16:57 test.example.com.crt.key
-rw-r--r--  1 root root 2.6K Mar 24 16:57 test.example.com.crt.pem
-rw-------  1 root root    4 Mar 24 06:04 .vault-token
-rw-------  1 root root 8.0K Mar 24 16:52 .viminfo

```

## 3
Ответ 3 Сам cron
```bash
root@server1:~# crontab -l
# Edit this file to introduce tasks to be run by cron.
#
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
#
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').
#
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
#
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
#
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
#
# For more information see the manual pages of crontab(5) and cron(8)
#
# m h  dom mon dow   command

* * * * * /root/sert.sh

```

