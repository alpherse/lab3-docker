# ИТ/ЛР3/КОНТЕЙНЕРИЗАЦИЯ

## Задача 1

![](assets/task1/t1_1.png)

![](assets/task1/t1_2.png)

[Docker hub](https://hub.docker.com/r/alpherse/custom-nginx)

## Задача 2

![](assets/task2/t2_1.png)

![](assets/task2/t2_2.png)

![](assets/task2/t2_3.png)

![](assets/task2/t2_4.png)

## Задача 3

![](assets/task3/t3_1.png)

**Объяснение: терминал подключился к потокам процесса контейнера (nginx, который просто ждал запросов - поэтому ничего не было). делая ctrl+c, отправляется сигнал 2, который вызывает завершение процесса. сам nginx является главным процессом контейнера, поэтому вместе с ним оффнулся и контейнер**

![](assets/task3/t3_2.png)

![](assets/task3/t3_3.png)

![](assets/task3/t3_4.png)

**Суть проблемы: несовпадение портов. docker продолжает перенаправлять запросы с порта 8080 системы на порт 80 контейнера, но после изменения конфигурации nginx слушает порт 81, поэтому запросы не обрабатываются и соединение сбрасывается**

### Доп. задание

![](assets/task3/t3_5.png)

![](assets/task3/t3_6.png)

**Для изменения проброса портов без пересоздания контейнера были отредактированы два файла конфигурации docker:**

- hostconfig.json: в PortBindings изменен порт контейнера с 80/tcp на 81/tcp (порт хоста 127.0.0.1:8080 остался прежним)

- config.v2.json: в ExposedPorts изменен порт с 80/tcp на 81/tcp

![](assets/task3/t3_7.png)

![](assets/task3/t3_8.png)

## Задача 4

![](assets/task4/t4_1.png)

![](assets/task4/t4_2.png)

![](assets/task4/t4_3.png)

## Задача 5

![](assets/task5/t5_1.png)

**Объяснение: был запущен compose.yaml, так как это приоритетное имя файла конфигурации docker compose. а docker-compose.yaml поддерживается для обратной совместимости**

![](assets/task5/t5_2.png)

[compose.yaml](assets/task5/compose.yaml)

![](assets/task5/t5_3.png)

![](assets/task5/t5_4.png)

![](assets/task5/t5_5.png)

![](assets/task5/t5_6.png)

**Суть предупреждения: после удаления compose.yaml контейнер portainer остался запущенным, хотя его сервис больше не описан в конфигурации. для его удаления использован флаг --remove-orphans**