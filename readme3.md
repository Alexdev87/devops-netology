Ответы на вопросы к Домашнее задание к занятию "3.1. Работа в терминале, лекция 1"
5.RAM:384mb
CPU:1 cpu
HDD:80gb
video:8mb

6.Добавляем комманды в файл VagrantFile:
  v.memory = 1024
  v.cpus = 2

8.HISTFILESIZE - максимальное число строк в файле истории для сохранения
строка 846
Ignoreboth это сокращение для 2х директив ignorespace and ignoredups
 ignorespace - не сохранять команды начинающиеся с пробела, 
 ignoredups - не сохранять команду, если такая уже имеется в истории

9.  {} - список который может состоять из цифр, букв, строчек, необходимо для выполнения  цикличного выполнение команд с подстановкой в виде списока.
10. touch test{1....100000} , 300000 - скорее всего препышает установленный лимит
11. Что делает конструкция [[ -d /tmp ]]  Простая команда представляет собой последовательность необязательных назначений переменных, за которыми следуют слова, разделенные пробелами, и перенаправления, и завершается оператором управления. Первое слово определяет команду, которая должна быть выполнена, и
передается в качестве нулевого аргумента. Остальные слова передаются в качестве аргументов вызываемой команде.

Данной командой ищем наличие каталога tmp и передаем значение 0 если нет и 1 если есть каталог
 
12. root@DESKTOP-2SCAN4P:/# mkdir /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# cp /bin/bash /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /usr/bin/bash
bash is /bin/bash
root@DESKTOP-2SCAN4P:/# PATH=/tmp/new_path_dir/:$PATH
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /tmp/new_path_dir/bash
bash is /usr/bin/bash
bash is /bin/bash

13. at - команда запускается в указанное время (в параметре)
batch - запускается когда уровень загрузки системы снизится ниже 1.512. root@DESKTOP-2SCAN4P:/# mkdir /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# cp /bin/bash /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /usr/bin/bash
bash is /bin/bash
root@DESKTOP-2SCAN4P:/# PATH=/tmp/new_path_dir/:$PATH
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /tmp/new_path_dir/bash
bash is /usr/bin/bash
bash is /bin/bash

13. at - команда запускается в указанное время (в параметре)
batch - запускается когда уровень загрузки системы снизится ниже 1.512. root@DESKTOP-2SCAN4P:/# mkdir /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# cp /bin/bash /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /usr/bin/bash
bash is /bin/bash
root@DESKTOP-2SCAN4P:/# PATH=/tmp/new_path_dir/:$PATH
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /tmp/new_path_dir/bash
bash is /usr/bin/bash
bash is /bin/bash

13. at - команда запускается в указанное время (в параметре)
batch - запускается когда уровень загрузки системы снизится ниже 1.512. root@DESKTOP-2SCAN4P:/# mkdir /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# cp /bin/bash /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /usr/bin/bash
bash is /bin/bash
root@DESKTOP-2SCAN4P:/# PATH=/tmp/new_path_dir/:$PATH
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /tmp/new_path_dir/bash
bash is /usr/bin/bash
bash is /bin/bash

13. at - команда запускается в указанное время (в параметре)
batch - запускается когда уровень загрузки системы снизится ниже 1.512. root@DESKTOP-2SCAN4P:/# mkdir /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# cp /bin/bash /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /usr/bin/bash
bash is /bin/bash
root@DESKTOP-2SCAN4P:/# PATH=/tmp/new_path_dir/:$PATH
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /tmp/new_path_dir/bash
bash is /usr/bin/bash
bash is /bin/bash

13. at - команда запускается в указанное время (в параметре)
batch - запускается когда уровень загрузки системы снизится ниже 1.512. root@DESKTOP-2SCAN4P:/# mkdir /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# cp /bin/bash /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /usr/bin/bash
bash is /bin/bash
root@DESKTOP-2SCAN4P:/# PATH=/tmp/new_path_dir/:$PATH
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /tmp/new_path_dir/bash
bash is /usr/bin/bash
bash is /bin/bash

13. at - команда запускается в указанное время (в параметре)
batch - запускается когда уровень загрузки системы снизится ниже 1.512. root@DESKTOP-2SCAN4P:/# mkdir /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# cp /bin/bash /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /usr/bin/bash
bash is /bin/bash
root@DESKTOP-2SCAN4P:/# PATH=/tmp/new_path_dir/:$PATH
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /tmp/new_path_dir/bash
bash is /usr/bin/bash
bash is /bin/bash

13. at - команда запускается в указанное время (в параметре)
batch - запускается когда уровень загрузки системы снизится ниже 1.512. root@DESKTOP-2SCAN4P:/# mkdir /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# cp /bin/bash /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /usr/bin/bash
bash is /bin/bash
root@DESKTOP-2SCAN4P:/# PATH=/tmp/new_path_dir/:$PATH
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /tmp/new_path_dir/bash
bash is /usr/bin/bash
bash is /bin/bash

13. at - команда запускается в указанное время (в параметре)
batch - запускается когда уровень загрузки системы снизится ниже 1.512. root@DESKTOP-2SCAN4P:/# mkdir /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# cp /bin/bash /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /usr/bin/bash
bash is /bin/bash
root@DESKTOP-2SCAN4P:/# PATH=/tmp/new_path_dir/:$PATH
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /tmp/new_path_dir/bash
bash is /usr/bin/bash
bash is /bin/bash

13. at - команда запускается в указанное время (в параметре)
batch - запускается когда уровень загрузки системы снизится ниже 1.512. root@DESKTOP-2SCAN4P:/# mkdir /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# cp /bin/bash /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /usr/bin/bash
bash is /bin/bash
root@DESKTOP-2SCAN4P:/# PATH=/tmp/new_path_dir/:$PATH
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /tmp/new_path_dir/bash
bash is /usr/bin/bash
bash is /bin/bash

13. at - команда запускается в указанное время (в параметре)
batch - запускается когда уровень загрузки системы снизится ниже 1.512. root@DESKTOP-2SCAN4P:/# mkdir /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# cp /bin/bash /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /usr/bin/bash
bash is /bin/bash
root@DESKTOP-2SCAN4P:/# PATH=/tmp/new_path_dir/:$PATH
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /tmp/new_path_dir/bash
bash is /usr/bin/bash
bash is /bin/bash

13. at - команда запускается в указанное время (в параметре)
batch - запускается когда уровень загрузки системы снизится ниже 1.512. root@DESKTOP-2SCAN4P:/# mkdir /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# cp /bin/bash /tmp/new_path_dir/
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /usr/bin/bash
bash is /bin/bash
root@DESKTOP-2SCAN4P:/# PATH=/tmp/new_path_dir/:$PATH
root@DESKTOP-2SCAN4P:/# type -a bash
bash is /tmp/new_path_dir/bash
bash is /usr/bin/bash
bash is /bin/bash

13. at - команда запускается в указанное время (в параметре)
batch - запускается когда уровень загрузки системы снизится ниже 1.5
