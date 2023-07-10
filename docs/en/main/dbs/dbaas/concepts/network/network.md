## Использование балансировщика нагрузки

Для каждого кластера PG/MySQL создается TCP-балансировщик, который имеет 3 порта. Они указывают на:

- мастер;
- синхронную реплику;
- асинхронную реплику.

## Настройка файервола

Вы можете настроить группы безопасности (файервола) как при [создании](../../instructions/create/) инстанса БД, так и после его развертывания через [раздел](/en/networks/vnet/operations/secgroups) **Виртуальные сети** → **Настройки firewall**.