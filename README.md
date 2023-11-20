# Домашнее задание к занятию "`Zabbix`" - `Максимов Андрей Дмитриевич`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания


---

### Задание 1
![image](https://github.com/duha2060/zabbix/assets/80347708/ebb0b038-5916-4e3e-84af-39bf78b4e803)

1. Установка репозитория Zabbix
```
# wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
# dpkg -i zabbix-release_6.0-4+debian11_all.deb
# apt update
```
2. Установка Zabbix сервера, веб-интерфейса
```
# apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts
```
3. Создание пользователя базы данных
```
# su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"'
# su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'123456789\'';"'
```
4. Импорт схемы
```
# zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
```
5. Настройка базы данных для Zabbix сервера
Редактируем файл /etc/zabbix/zabbix_server.conf
```
# sed -i 's/# DBPassword=/DBPassword=123456789/g' /etc/zabbix/zabbix_server.conf
```
6. Запуск и автозапуск
```
# systemctl restart zabbix-server apache2
# systemctl enable zabbix-server apache2
```

---

### Задание 2
![image](https://github.com/duha2060/zabbix/assets/80347708/6976f572-2bf7-4235-915b-ef7ba1462ddc)
![image](https://github.com/duha2060/zabbix/assets/80347708/7327b568-3c3b-48d9-931d-ea7ee043c46d)
![image](https://github.com/duha2060/zabbix/assets/80347708/97901cf9-59a3-41f8-abf7-435a94af7c18)

1. Установка репозитория Zabbix
```
# rpm -Uvh https://repo.zabbix.com/zabbix/6.4/rhel/7/x86_64/zabbix-release-6.4-1.el7.noarch.rpm
# yum clean all
```
2. Установка Zabbix сервера, веб-интерфейса
```
# yum install zabbix-agent
```
6. Запуск и автозапуск
```
# systemctl restart zabbix-agent
# systemctl enable zabbix-agent
```
---






