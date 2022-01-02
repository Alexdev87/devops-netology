Пункт 8 - по рекомендации коллег 
root@DESKTOP-2SCAN4P:/home/admin1# ls -lha
total 40K
drwxr-xr-x 4 admin1 admin1 4.0K Dec 27 20:55 .
drwxr-xr-x 3 root   root   4.0K Nov  2 23:07 ..
-rw------- 1 admin1 admin1 2.1K Dec 29 21:53 .bash_history
-rw-r--r-- 1 admin1 admin1  220 Nov  2 23:07 .bash_logout
-rw-r--r-- 1 admin1 admin1 3.7K Nov  2 23:07 .bashrc
drwx------ 2 admin1 admin1 4.0K Nov 23 22:01 .cache
-rw-r--r-- 1 root   root      0 Nov 23 20:53 .hushlogin
drwxr-xr-x 2 admin1 admin1 4.0K Nov  2 23:07 .landscape
-rw------- 1 admin1 admin1  140 Dec 27 20:55 .lesshst
-rw-r--r-- 1 admin1 admin1    0 Nov 23 20:38 .motd_shown
-rw-r--r-- 1 admin1 admin1  807 Nov  2 23:07 .profile
-rw-r--r-- 1 admin1 admin1    0 Nov  2 23:08 .sudo_as_admin_successful
-rw------- 1 admin1 admin1  901 Nov  7 13:05 .viminfo
(dir && ls —ppp) Тут выводится состав директории и ls с неправильными параметрами дает ошибку.
root@DESKTOP-2SCAN4P:/home/admin1# dir && ls —ppp
ls: cannot access '—ppp': No such file or directory
ответ команды dir && ls —ppp назначается дискриптору 3, далее переводим на ввод 1, ввод проверяем являеться ошибкой или нет
root@DESKTOP-2SCAN4P:/home/admin1# (dir && ls —ppp) 3>&1 1>&2 2>&3
ls: cannot access '—ppp': No such file or directory

Пункт 12  - по рекомендации коллег 
Необходимо дописать в конфигурационный файл Vargant 

config.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
      echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
      echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
    SHELL
  end

