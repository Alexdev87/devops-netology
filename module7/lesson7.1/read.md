Домашнее задание к занятию "7.1. Инфраструктура как код"

##  задача 1

Ответ:
```bash
   1.	Ответить на четыре вопроса представленных в разделе "Легенда".
Какой тип инфраструктуры будем использовать для этого проекта: изменяемый или не изменяемый?

- Неизменяемый.

Будет ли центральный сервер для управления инфраструктурой?

- Нет. Управление будет с любой машины через Terraform/Ansible и Git для отслеживания версиозности.

Будут ли агенты на серверах?

- Нет. Используем agentless Ansible.

Будут ли использованы средства для управления конфигурацией или инициализации ресурсов?

- Да. Terraform/Ansible.

    2.	Какие инструменты из уже используемых вы хотели бы использовать для нового проекта?

- Terraform, Ansible, Packer, Docker, Kubernetes

    3.  Хотите ли рассмотреть возможность внедрения новых инструментов для этого проекта?

Возможно остатки Сloud Formation изменить на свои серверные ресурсы или облачные провайдеры.
```

##  задача 2
Ответ 2
```bash
root@ubuntuserv:/home/adm1# terraform --version
Terraform v1.1.6
on linux_amd64

```

## Задача  3
Ответ 3
```bash
Для поготовке к решению задачи использовал статьи

- https://opensource.com/article/20/6/homebrew-linux
- https://opensource.com/article/20/11/tfenv

root@ubuntuserv:/home/adm1# terraform --version
Terraform v1.1.6
on linux_amd64
adm1@ubuntuserv:~$ tfenv list
* 0.12.29 (set by /home/linuxbrew/.linuxbrew/Cellar/tfenv/2.2.3/version)
adm1@ubuntuserv:~$ tfenv use 0.12.29
Switching default version to v0.12.29
Switching completed
adm1@ubuntuserv:~$ terraform --version
Terraform v0.12.29

Your version of Terraform is out of date! The latest version
is 1.1.7. You can update by downloading from https://www.terraform.io/downloads.html

```








