Домашнее задание к занятию "09.02 CI\CD"

##  задача 1
Знакомоство с SonarQube
Ответ:
```bash
Подготовка к выполнению

    Выполняем docker pull sonarqube:8.7-community
    Выполняем docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9000:9000 sonarqube:8.7-community
    Ждём запуск, смотрим логи через docker logs -f sonarqube
    Проверяем готовность сервиса через браузер
    Заходим под admin\admin, меняем пароль на свой

В целом, в этой статье описаны все варианты установки, включая и docker, но так как нам он нужен разово, то достаточно того набора действий, который я указал выше.
Основная часть

    Создаём новый проект, название произвольное
    Скачиваем пакет sonar-scanner, который нам предлагает скачать сам sonarqube
    Делаем так, чтобы binary был доступен через вызов в shell (или меняем переменную PATH или любой другой удобный вам способ)
    Проверяем sonar-scanner --version
    Запускаем анализатор против кода из директории example с дополнительным ключом -Dsonar.coverage.exclusions=fail.py
    Смотрим результат в интерфейсе
    Исправляем ошибки, которые он выявил(включая warnings)
    Запускаем анализатор повторно - проверяем, что QG пройдены успешно
    Делаем скриншот успешного прохождения анализа, прикладываем к решению ДЗ
```
##
![](https://github.com/Alexdev87/devops-netology/tree/main/lesson9.2/sonarqube.png1)
```

##  задача 2
Знакомство с Nexus
Ответ 2
```bash
Подготовка к выполнению

    Выполняем docker pull sonatype/nexus3
    Выполняем docker run -d -p 8081:8081 --name nexus sonatype/nexus3
    Ждём запуск, смотрим логи через docker logs -f nexus
    Проверяем готовность сервиса через бразуер
    Узнаём пароль от admin через docker exec -it nexus /bin/bash
    Подключаемся под админом, меняем пароль, сохраняем анонимный доступ

Основная часть

    В репозиторий maven-public загружаем артефакт с GAV параметрами:
        groupId: netology
        artifactId: java
        version: 8_282
        classifier: distrib
        type: tar.gz
    В него же загружаем такой же артефакт, но с version: 8_102
    Проверяем, что все файлы загрузились успешно
    В ответе присылаем файл maven-metadata.xml для этого артефекта
```
##
![maven-metadata.xml](https://github.com/Alexdev87/devops-netology/tree/main/lesson9.2/maven-metadata.xml)

## Задача  3
Знакомство с Maven
Ответ 2
```bash
Подготовка к выполнению

    Скачиваем дистрибутив с maven
    Разархивируем, делаем так, чтобы binary был доступен через вызов в shell (или меняем переменную PATH или любой другой удобный вам способ)
    Проверяем mvn --version
    Забираем директорию mvn с pom

Основная часть

    Меняем в pom.xml блок с зависимостями под наш артефакт из первого пункта задания для Nexus (java с версией 8_282)
    Запускаем команду mvn package в директории с pom.xml, ожидаем успешного окончания
    Проверяем директорию ~/.m2/repository/, находим наш артефакт
    В ответе присылаем исправленный файл pom.xml
```
##
![pom.xml](https://github.com/Alexdev87/devops-netology/tree/main/lesson9.2/pom.xml)







