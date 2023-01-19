### Домашнее задание №25 (LDAP)
1. Написан [Vagrantfile](https://github.com/uNkindy/Otus_Unit_25_LDAP/blob/main/Vagrantfile) с 2 ВМ host1 и host2, входящие в один домен test.local;
2. Написан [playbook](https://github.com/uNkindy/Otus_Unit_25_LDAP/blob/main/playbook.yml), устанавливающий FreeIPA server на host1 при помощи установленной ansible роли;
- в начале устанавливаются и обновляются необходимые для работы FreeIPA пакеты;
- устанавливается FreeIPA сервер c DNS;
- добаввляются 2 новых юзера user1 и user2 при помощи модуля ansible;
- проверяем доступность веб-интерфейса FreeIPA, убеждаемся в добавлении новых пользователей.
```console
[root@devops Otus_Unit_25_LDAP]# curl localhost:8080
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="https://host1.test.local/ipa/ui">here</a>.</p>
</body></html>
```
```console
[root@host1 vagrant]# kinit admin
Password for admin@TEST.LOCAL: 
[root@host1 vagrant]# ipa user-find
---------------
3 users matched
---------------
  User login: admin
  Last name: Administrator
  Home directory: /home/admin
  Login shell: /bin/bash
  Principal alias: admin@TEST.LOCAL
  UID: 1057200000
  GID: 1057200000
  Account disabled: False

  User login: user1
  First name: user1
  Last name: user1
  Home directory: /home/user1
  Login shell: /bin/sh
  Principal name: user1@TEST.LOCAL
  Principal alias: user1@TEST.LOCAL
  Email address: user1@test.local
  UID: 1001
  GID: 100
  Account disabled: False

  User login: user2
  First name: user2
  Last name: user2
  Home directory: /home/user2
  Login shell: /bin/sh
  Principal name: user2@TEST.LOCAL
  Principal alias: user2@TEST.LOCAL
  Email address: user2@test.local
  UID: 1002
  GID: 101
  Account disabled: False
----------------------------
Number of entries returned 3
----------------------------
```
1. Далее playbook устанавливает необходимые пакеты для FreeIPA client на host2, и добавляет host2 в домен. Проверим это:
```console
[root@host2 vagrant]# kinit admin
Password for admin@TEST.LOCAL: 
kinit: Password incorrect while getting initial credentials
[root@host2 vagrant]# ipa ping
-------------------------------------------
IPA server version 4.6.8. API version 2.237
-------------------------------------------
```