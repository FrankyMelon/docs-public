Для создания инстанса JupyterHub, перейдите в раздел «ML Platform». Нажмите «Добавить инстанс».

При нажатии на кнопку в окне откроется конфигуратор виртуальной машины, состоящий из нескольких этапов, в результате определяющий параметры создаваемой ВМ.

На всех этапах конфигуратор информирует о стоимости создаваемого инстанса, дополнительных возможностях, а также позволяет обратиться в поддержку в случае возникновения вопросов.

В процессе установки :

| Параметр | Описание |
| --- | --- |
| Имя инстанса | Отображаемое имя инстанса. Также задает hostname в ОС. |
| Тип виртуальной машины | Предустановленная конфигурация ВМ (CPU и RAM). |
| Зона доступности	| Выбор датацентра, где будет запущен инстанс. |
| Размер диска | Задает размер диска ВМ в GB. |
| Тип диска	| Тип создаваемого диска инстанса, [подробнее](https://mcs.mail.ru/docs/base/iaas/vm-volumes/volume-sla). |
| Операционная система | Образ операционной системы (версия, редакция). |
| Сеть | Создание ВМ во внешней (ext-net) или в приватной сети. |
| Адрес подсети | Появляется при выборе опции «Создать новую сеть». Задает CIDR новой подсети. |
| Выбор доменного имени | Появляется при выборе приватной сети. Задает DNS имя инстанса, [подробнее](https://mcs.mail.ru/docs/networks/vnet/networks/private-dns). |
| Ключ виртуальной машины | Появляется при выборе приватной сети. Используется для расшифровки пароля администратора. |
| Использовать конфигурационный диск | Включение данной опции настраивает сеть в операционной системе при создании ВМ в ext-net или приватной сети без DHCP сервера. |
| Настройки firewall | Выбор доступных группы безопасности, включающей в себя разрешающие правила прохождения трафика. |
| Назначить внешний IP | Появляется при выборе приватной сети. Назначает плавающий IP. |

На следующем шаге настраивается виртуальная сеть. Можно выбрать существующую сеть или создать новую (подробнее можно прочитать в статье «[Создание и удаление сетей](https://mcs.mail.ru/help/ru_RU/networks/create-net)». Также заметим в скобках, что тип сети «shadowport» может быть выбран только для конфигурации ВМ «shadowport».

На следующем шаге настраивается план автоматического резервного копирования ВМ. После чего следует перейти на этап создания кнопкой «Добавить виртуальную машину».

Виртуальная машина будет создана в течение 10-15 минут. В данный период разворачивается операционная система на диск инстанса, а также работают системные инструменты, обеспечивающие настройку виртуальной машины в соответствии с указанными параметрами.

<warn>

Не закрывайте окно создания нового инстанса.

По окончании настройки инстанса откроется страница с характеристиками сервера и инструкцией по подключению к нему.

</warn>