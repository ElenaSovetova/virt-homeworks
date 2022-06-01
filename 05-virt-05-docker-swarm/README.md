# Домашнее задание к занятию "5.5. Оркестрация кластером Docker контейнеров на примере Docker Swarm"

## Как сдавать задания

Обязательными к выполнению являются задачи без указания звездочки. Их выполнение необходимо для получения зачета и диплома о профессиональной переподготовке.

Задачи со звездочкой (*) являются дополнительными задачами и/или задачами повышенной сложности. Они не являются обязательными к выполнению, но помогут вам глубже понять тему.

Домашнее задание выполните в файле readme.md в github репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.

Любые вопросы по решению задач задавайте в чате учебной группы.

---

## Задача 1

Дайте письменые ответы на следующие вопросы:

- В чём отличие режимов работы сервисов в Docker Swarm кластере: replication и global?
---
* replication - настраиваемое распространение микросервиса на докер ноды ,

* global - распространение микросервиса на ВСЕ ноды
---

- Какой алгоритм выбора лидера используется в Docker Swarm кластере?
---
* RAFT. Изначально, первая же нода в кластере докер становится лидером, но кластер считается неконсистентным. А при достижении консистентности(3 и более ноды менеджеры) происходит постоянное голосование за лидерство по алгоритму поддержания распределенного консенсуса или The Raft Consensus Algorithm. По-простому: голосование через случайные таймауты.
---
- Что такое Overlay Network?
---
* Cеть "поверх" сетей хоста, создается по-умолчанию в докер кластере для безопасного взаимодействия(обмена данными) между контейнерами. По-умолчанию создается ingress -обрабатывает трафик управления и данных, связанный со службами
---
## Задача 2

Создать ваш первый Docker Swarm кластер в Яндекс.Облаке

Для получения зачета, вам необходимо предоставить скриншот из терминала (консоли), с выводом команды:
```
docker node ls
```
```html
[root@node01 ~]# docker node ls
ID                            HOSTNAME             STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
k6atexgllko9sbsjenrvpsrho *   node01.netology.yc   Ready     Active         Leader           20.10.13
tvfe7umiabl5dawnxm8aovqx2     node02.netology.yc   Ready     Active         Reachable        20.10.13
zjy62ib4yrwcgduhuwphloazv     node03.netology.yc   Ready     Active         Reachable        20.10.13
8z64o78felxg8a4wfr1hrgfuh     node04.netology.yc   Ready     Active                          20.10.13
fmhc4pw1zalz6ybb9exfs6q7y     node05.netology.yc   Ready     Active                          20.10.13
yc7e3yq412mnd1qu5259dzgdm     node06.netology.yc   Ready     Active                          20.10.13
```

## Задача 3

Создать ваш первый, готовый к боевой эксплуатации кластер мониторинга, состоящий из стека микросервисов.

Для получения зачета, вам необходимо предоставить скриншот из терминала (консоли), с выводом команды:
```
docker service ls
```
```html
[root@node01 ~]# docker service ls
ID             NAME                                MODE         REPLICAS   IMAGE                                          PORTS
wrh11a52tgl2   swarm_monitoring_alertmanager       replicated   1/1        stefanprodan/swarmprom-alertmanager:v0.14.0
tzbxn1avelw1   swarm_monitoring_caddy              replicated   1/1        stefanprodan/caddy:latest                      *:3000->3000/tcp, *:9090->9090/tcp, *:9093-9094->9093-9094/tcp
1gzfuoovmp0k   swarm_monitoring_cadvisor           global       6/6        google/cadvisor:latest
lxj066r113y6   swarm_monitoring_dockerd-exporter   global       6/6        stefanprodan/caddy:latest
s16ymp7bnz80   swarm_monitoring_grafana            replicated   1/1        stefanprodan/swarmprom-grafana:5.3.4
zjakk7hwlq4q   swarm_monitoring_node-exporter      global       6/6        stefanprodan/swarmprom-node-exporter:v0.16.0
v5li4y7jr4ij   swarm_monitoring_prometheus         replicated   1/1        stefanprodan/swarmprom-prometheus:v2.5.0
q7ftohl2okf8   swarm_monitoring_unsee              replicated   1/1        cloudflare/unsee:v0.8.0
```

## Задача 4 (*)

Выполнить на лидере Docker Swarm кластера команду (указанную ниже) и дать письменное описание её функционала, что она делает и зачем она нужна:
```
# см.документацию: https://docs.docker.com/engine/swarm/swarm_manager_locking/
docker swarm update --autolock=true
```

