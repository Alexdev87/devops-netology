# Домашнее задание к занятию "4.2. Использование Python для решения типовых DevOps задач"

## Обязательная задача 1

Есть скрипт:
```bash
#!/usr/bin/env python3
a = 1
b = '2'
c = a + b

```

| Переменная  | Значение |
| ------------- | ------------- |
| `Какое значение будет присвоено переменной c?`  | Выдаст ошибку число и строку нельзя складывать TypeError: unsupported operand type(s) for +: 'int' and 'str'   | 
| `Как получить для переменной c значение 12?`  | c= str(a) + b или c = (a + int(b)) * int(b) * int(b)   | 
| `Как получить для переменной c значение 3?`  | >>> a = 1 >>> b = 2 >>> c = a + b >>> print(c) 3 | 


## Обязательная задача 2
Мы устроились на работу в компанию, где раньше уже был DevOps Engineer. Он написал скрипт, позволяющий узнать, какие файлы модифицированы в репозитории, относительно локальных изменений. Этим скриптом недовольно начальство, потому что в его выводе есть не все изменённые файлы, а также непонятен полный путь к директории, где они находятся. Как можно доработать скрипт ниже, чтобы он исполнял требования вашего руководителя?
```bash
#!/usr/bin/env python3

import os

bash_command = ["cd ~/netology/sysadm-homeworks", "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
is_change = False
for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:   ', '')
        print(prepare_result)
        break

```

### Ваш скрипт:
```bash
#!/usr/bin/env python3

import os

cmd = os.getcwd()
bash_command = ["cd "+cmd, "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:   ', '')
        print(cmd+" "+prepare_result)

```

### Вывод скрипта при запуске при тестировании:
```bash
root@ubuntuserv:/home/adm1/gitrep/devops-netology# python3 lesson2.py
/home/adm1/gitrep/devops-netology 123.md 

```
## Обязательная задача 3
Доработать скрипт выше так, чтобы он мог проверять не только локальный репозиторий в текущей директории, а также умел воспринимать путь к репозиторию, который мы передаём как входной параметр. Мы точно знаем, что начальство коварное и будет проверять работу этого скрипта в директориях, которые не являются локальными репозиториями.

### Ваш скрипт:
```bash
#!/usr/bin/env python3

import os
import sys


cmd = os.getcwd()

if len(sys.argv)>=2:
    cmd = sys.argv[1]
bash_command = ["cd "+cmd, "git status 2>&1"]
result_os = os.popen(' && '.join(bash_command)).read()
for result in result_os.split('\n'):
    if result.find('fatal') != -1:
        print(cmd+" git ne naiden")
    if result.find('modify') != -1:
        prepare_result = result.replace('\modify:   ', '')
        print(prepare_result)
 Вывод скрипта при запуске при 

```

### Вывод скрипта при запуске при тестировании:
```bash
root@ubuntuserv:/home/adm1/pyton# python3 lesson3.py
/home/adm1/pyton git ne naiden

root@ubuntuserv:/home/adm1/gitrep/devops-netology# python3 lesson3.py
/home/adm1/gitrep/devops-netology 123.md 

```
## Обязательная задача 4
Наша команда разрабатывает несколько веб-сервисов, доступных по http. Мы точно знаем, что на их стенде нет никакой балансировки, кластеризации, за DNS прячется конкретный IP сервера, где установлен сервис. Проблема в том, что отдел, занимающийся нашей инфраструктурой очень часто меняет нам сервера, поэтому IP меняются примерно раз в неделю, при этом сервисы сохраняют за собой DNS имена. Это бы совсем никого не беспокоило, если бы несколько раз сервера не уезжали в такой сегмент сети нашей компании, который недоступен для разработчиков. Мы хотим написать скрипт, который опрашивает веб-сервисы, получает их IP, выводит информацию в стандартный вывод в виде: <URL сервиса> - <его IP>. Также, должна быть реализована возможность проверки текущего IP сервиса c его IP из предыдущей проверки. Если проверка будет провалена - оповестить об этом в стандартный вывод сообщением: [ERROR] <URL сервиса> IP mismatch: <старый IP> <Новый IP>. Будем считать, что наша разработка реализовала сервисы: drive.google.com, mail.google.com, google.com.

### Ваш скрипт:
```bash
#!/usr/bin/env python3

import socket
import time

servers = {"drive.google.com": "", "mail.google.com": "", "google.com": ""}
while True:
    for url, ip in servers.items():
        ip_addr = socket.gethostbyname(url)
        if ip == "":
            servers[url] = ip_addr
            print("{} - {}".format(url, ip_addr))
        elif ip != ip_addr:
            print("[ERROR] {} IP mismatch: {} -> {}".format(url, ip, ip_addr))
            servers[url] = ip_addr
    time.sleep(1)

```

### Вывод скрипта при запуске при тестировании:
```bash
root@ubuntuserv:/home/adm1/gitrep/devops-netology# python3 lesson4.py
drive.google.com - 173.194.73.194
mail.google.com - 74.125.131.83
google.com - 173.194.222.138
[ERROR] google.com IP mismatch: 173.194.222.138 -> 173.194.222.113
[ERROR] mail.google.com IP mismatch: 74.125.131.83 -> 74.125.131.18
[ERROR] google.com IP mismatch: 173.194.222.113 -> 173.194.222.138
[ERROR] mail.google.com IP mismatch: 74.125.131.18 -> 74.125.131.19
[ERROR] google.com IP mismatch: 173.194.222.138 -> 173.194.222.100
[ERROR] mail.google.com IP mismatch: 74.125.131.19 -> 74.125.131.17
[ERROR] google.com IP mismatch: 173.194.222.100 -> 173.194.222.102
[ERROR] mail.google.com IP mismatch: 74.125.131.17 -> 74.125.131.18
[ERROR] google.com IP mismatch: 173.194.222.102 -> 173.194.222.101
```



