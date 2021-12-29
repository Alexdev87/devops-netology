1. Какого типа команда cd? Попробуйте объяснить, почему она именно такого типа; опишите ход своих мыслей, если считаете что она могла бы быть другого типа
- Это команда оболочки         type cd cd is a shell builtin
- почему она именно такого типа - предназначение команды менять каталог по запросу без дополнительных аргументов

2.  grep something файл в котором ищем информацию -c 
@can usually be rewritten like something along the lines of

    	something | grep -c .   # Notice that . is better than '..*'@

3. ps -f 1
UID        PID  PPID  C STIME TTY      STAT   TIME CMD
root         1     0  0 20:22 ?        Sl     0:00 /init

pstree -p
init(1)─┬─init(10)───init(11)───bash(12)─┬─man(23)───pager(33)
        │                                └─pstree(98)
        └─{init}(9)

4. ls не существующего каталога 2 > tmux

5. создаем и заполняем файл echo file_stdin.txt

1
wewe
wew

cat file_stdin.txt > file_stdout

6.
root@DESKTOP-2SCAN4P:/# tty
/dev/pts/0
root@DESKTOP-2SCAN4P:/# echo Hello from pts0 to tty0 >/dev/tty0

7. root@DESKTOP-2SCAN4P:/dev# bash 5>&1  - перенаправить 5 на тот же адрес, что и stdout
root@DESKTOP-2SCAN4P:/dev# echo netology > /proc/$$/fd/5
netology

8. 



9. Выведет переменные среды 
 cat /proc/$$/environ
HOSTTYPE=x86_64LANG=C.UTF-8PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/lib/wsl/lib:/mnt/c/Program Files/WindowsApps/CanonicalGroupLimited.UbuntuonWindows_2004.2021.825.0_x64__79rhkp1fndgsc:/mnt/c/Program Files (x86)/VMware/VMware Workstation/bin/:/mnt/c/WINDOWS/system32:/mnt/c/WINDOWS:/mnt/c/WINDOWS/System32/Wbem:/mnt/c/WINDOWS/System32/WindowsPowerShell/v1.0/:/mnt/c/WINDOWS/System32/OpenSSH/:/mnt/c/Program Files/Microsoft SQL Server/Client SDK/ODBC/130/Tools/Binn/:/mnt/c/Program Files (x86)/Microsoft SQL Server/130/Tools/Binn/:/mnt/c/Program Files/Microsoft SQL Server/130/Tools/Binn/:/mnt/c/Program Files/Microsoft SQL Server/130/DTS/Binn/:/mnt/c/Program Files/Git/cmd:/mnt/c/HashiCorp/Vagrant/bin:/mnt/c/ProgramData/chocolatey/bin:/mnt/c/Users/admin/AppData/Roaming/Python/Python310/Scripts:/mnt/c/Users/admin/AppData/Local/Programs/Python/Python310/:/mnt/c/Users/admin/AppData/Local/Microsoft/WindowsApps:/mnt/c/Program Files/Oracle/VirtualBoxTERM=xterm-256colorWSLENV=WSL_INTEROP=/run/WSL/11_interopNAME=DESKTOP-2SCAN4PHOME=/home/admin1USER=admin1LOGNAME=admin1SHELL=/bin/bashWSL_DISTRO_NAME=Ubuntu

еще можно командой printenv

10. There is a numerical subdirectory for each running process; the subdirectory is named  by  the  process
              ID.  Each /proc/[pid] subdirectory contains the pseudo-files and directories described below.

              The  files  inside  each  /proc/[pid]  directory are normally owned by the effective user and effective
              group ID of the process.  However, as a security measure,  the  ownership  is  made  root:root  if  the
              process's "dumpable" attribute is set to a value other than 1.

              Before Linux 4.11, root:root meant the "global" root user ID and group ID (i.e., UID 0 and GID 0 in the
              initial user namespace).  Since Linux 4.11, if the process is in a noninitial user namespace that has a
              valid  mapping for user (group) ID 0 inside the namespace, then the user (group) ownership of the files
              under /proc/[pid] is instead made the same as the root user (group) ID of the  namespace.   This  means
              that inside a container, things work as expected for the container "root" user.


/proc/[pid]/exe
              Under  Linux 2.2 and later, this file is a symbolic link containing the actual pathname of the executed
              command.  This symbolic link can be dereferenced normally; attempting to open it  will  open  the  exe‐
              cutable.   You  can  even type /proc/[pid]/exe to run another copy of the same executable that is being
              run by process [pid].  If the pathname has been unlinked, the symbolic link  will  contain  the  string
              '(deleted)'  appended  to the original pathname.  In a multithreaded process, the contents of this sym‐
              bolic link are not  available  if  the  main  thread  has  already  terminated  (typically  by  calling
              pthread_exit(3)).

              Permission  to dereference or read (readlink(2)) this symbolic link is governed by a ptrace access mode
              PTRACE_MODE_READ_FSCREDS check; see ptrace(2).

              Under Linux 2.0 and earlier, /proc/[pid]/exe is a pointer to the binary which was executed, and appears
              as a symbolic link.  A readlink(2) call on this file under Linux 2.0 returns a string in the format:

                  [device]:inode

              For example, [0301]:1502 would be inode 1502 on device major 03 (IDE, MFM, etc. drives) minor 01 (first
              partition on the first drive).

              find(1) with the -inum option can be used to locate the file.

11. sse4_2 

12.

13. необходимо установить sudo apt install reptyr
root@DESKTOP-2SCAN4P:/home/admin1# ps -f
UID        PID  PPID  C STIME TTY          TIME CMD
root       101    90  0 21:14 pts/0    00:00:00 sudo su
root       102   101  0 21:14 pts/0    00:00:00 su
root       103   102  0 21:14 pts/0    00:00:00 bash
root       110   103  0 21:14 pts/0    00:00:00 ps -f
root@DESKTOP-2SCAN4P:/home/admin1# reptyr 101
[-] Process 102 (su) shares 101's process group. Unable to attach.
(This most commonly means that 101 has suprocesses).
Unable to attach to pid 101: Invalid argument
root@DESKTOP-2SCAN4P:/home/admin1# reptyr 103
[-] Timed out waiting for child stop.

[1]+  Stopped                 sudo su
 [!] Unable to set terminal attributes: Input/output error

14. tee  - считывание со стандартного ввода и запись в стандартный вывод и файлы
